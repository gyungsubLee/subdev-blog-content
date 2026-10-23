---
order: 4
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 28aeda9b-0fe1-802c-a272-d7808f953ccf
title: "[ 실습 ] Query Builder CRUD"
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 226eda9b-0fe1-802b-a035-c3a886768c4d
    title: Nest.js
  - id: 260eda9b-0fe1-801b-836b-c2e229a88ff9
    title: 한 번에 끝내는 NestJS 패키지 - Part 1. 기초
  - id: 274eda9b-0fe1-8023-ba05-d84527f93ae0
    title: DB ( SQL, TypeORM, QueryBuilder, Transaction, Migration )
  - id: 28aeda9b-0fe1-802c-a272-d7808f953ccf
    title: "[ 실습 ] Query Builder CRUD"
excerpt: "목차 - Query Builder CRUD 실습 - 비교: Query Builder vs Repository.method Query Builder CRUD 실습 --- ✏️ 개념: 페이지 [ 전체 코드 ] MovieService 이전 TypeORM Repository 사용 - [ 코드 ] MovieService types"
cover: null
icon: null
notionProperties: {}
schema_version: 1
parent_id: 274eda9b-0fe1-8023-ba05-d84527f93ae0
created: 2025-10-12T04:58:28.675Z
updated: 2025-10-12T14:27:03.991Z
legacy_path: Main/Nest.js-c3a886768c4d/한 번에 끝내는 NestJS 패키지 - Part 1. 기초-c2e229a88ff9/DB ( SQL, TypeORM, QueryBuilder, Transaction,-d84527f93ae0/[ 실습 ] Query Builder CRUD-d7808f953ccf/index.md
legacy_category: Nest.js
source_url: https://beautiful-college-c84.notion.site/28aeda9b0fe1802ca272d7808f953ccf
---
> 
> 
> <a id="28aeda9b0fe181b39ee9d1b61a218779"></a>
> 
> <strong>목차</strong>
> 
> - [Query Builder CRUD 실습](#28aeda9b0fe181eb8a1cebee4742c966)
> - [비교: Query Builder  vs  Repository.method](#28aeda9b0fe180b69e7cf026f839e1c8)

<a id="28aeda9b0fe181eb8a1cebee4742c966"></a>

## <code>Query Builder</code> CRUD 실습

---

> ✏️ 
> 
> <a id="28aeda9b0fe180b68404d93ae34ccfd5"></a>
> 
> <strong>개념</strong>&#58; <a href="#/post/289eda9b-0fe1-80b0-baf8-c0d2a60a1ffd">페이지</a> 

<details>
<summary><strong>&#91;  전체 코드 &#93; MovieService</strong></summary>

<details>
<summary>이전 TypeORM Repository 사용</summary>

- <strong>&#91; 코드 &#93; MovieService</strong>
    <a id="28aeda9b0fe1801a8831cd9d2eee3317"></a>

    ```typescript
    import { Injectable, NotFoundException } from '@nestjs/common';
    import { CreateMovieDto } from './dto/create-movie.dto';
    import { UpdateMovieDto } from './dto/update-movie.dto';
    import { InjectRepository } from '@nestjs/typeorm';
    import { Movie } from './entities/movie.entity';
    import { DataSource, In, Like, Repository } from 'typeorm';
    import { MovieDetail } from './entities/movie-datail.entity';
    import { Director } from 'src/director/entities/director.entity';
    import { Genre } from 'src/genre/entities/genre.entity';
    import { User } from 'src/user/entities/user.entity';

    @Injectable()
    export class MovieService {
      constructor(
        @InjectRepository(Movie)
        private readonly movieRepository: Repository<Movie>,
        @InjectRepository(MovieDetail)
        private readonly movieDetailRepository: Repository<MovieDetail>,
        @InjectRepository(Director)
        private readonly directorRepository: Repository<Director>,
        @InjectRepository(Genre)
        private readonly genreRepository: Repository<Genre>,
        private readonly dataSource: DataSource,
      ) {}

      async findAll(title?: string) {
        // title 이 없는 경우
        if (!title) {
          return [
            await this.movieRepository.find({
              relations: ['director', 'genres'],
            }),
            await this.movieRepository.count(),
          ];
        }

        // title이 있는 경우
        return this.movieRepository.findAndCount({
          where: {
            title: Like(`%${title}%`),
          },
          relations: ['director', 'genres'],
        });
      }

      async findOne(id: number) {
        const movie = await this.movieRepository.findOne({
          where: {
            id,
          },
          relations: ['detail', 'director', 'genres'],
        });

        if (!movie) {
          throw new NotFoundException('존재하지 않는 영화입니다.');
        }

        return movie;
      }

      async create(createMovieDto: CreateMovieDto, creator: User) {
        // 1. Director 검증
        const director = await this.directorRepository.findOne({
          where: { id: createMovieDto.directorId },
        });

        if (!director) {
          throw new NotFoundException('존재하지 않는 Director 입니다.');
        }

        // 2. Genres 검증
        const genres = await this.genreRepository.findBy({
          id: In(createMovieDto.genreIds),
        });

        if (genres.length !== createMovieDto.genreIds.length) {
          throw new NotFoundException(
            `존재하지 않는 장르가 있습니다. ids: ${genres.map((genre) => genre.id).join(',')}`,
          );
        }

        // 3. Movie 생성
        const movie = this.movieRepository.create({
          title: createMovieDto.title,
          director,
          detail: { detail: createMovieDto.detail }, // cascade로 MovieDetail 자동 저장
          genres,
          creator,
        });

        // 4. 한 번의 save로 Movie + MovieDetail + ManyToMany genres 연결
        const savedMovie = await this.movieRepository.save(movie);

        return await this.movieRepository.findOne({
          where: { id: savedMovie.id },
          relations: ['detail', 'director', 'genres', 'creator'],
        });
      }

      async update(id: number, updateMovieDto: UpdateMovieDto) {
        const movie = await this.movieRepository.findOne({
          where: { id },
          relations: ['detail', 'genres', 'director'],
        });

        if (!movie) {
          throw new NotFoundException('존재하지 않는 영화입니다.');
        }

        const { detail, directorId, genreIds, ...movieRest } = updateMovieDto;

        // 1. Movie 필드 업데이트
        Object.assign(movie, movieRest);

        // 2. detail 업데이트
        if (detail) {
          movie.detail.detail = detail;
        }

        // 3. director 교체
        if (directorId) {
          const director = await this.directorRepository.findOne({
            where: { id: directorId },
          });

          if (!director) {
            throw new NotFoundException('존재하지 않는 감독입니다. ');
          }

          movie.director = director;
        }

        // 4. genres 교체
        if (genreIds) {
          const genres = await this.genreRepository.findBy({ id: In(genreIds) });

          if (genres.length !== updateMovieDto.genreIds?.length) {
            throw new NotFoundException(
              `존재하지 않는 장르가 있습니다. ids:  ${genres.map((genre) => genre.id).join(',')}`,
            );
          }

          movie.genres = genres;
        }

        await this.movieRepository.save(movie);

        return this.movieRepository.findOne({
          where: { id },
          relations: ['detail', 'director', 'genres'],
        });
      }

      async remove(id: number) {
        const movie = await this.movieRepository.findOne({
          where: { id },
        });

        if (!movie) {
          throw new NotFoundException('존재하지 않는 영화입니다.');
        }

        // detail은 cascade: true 설정으로 삭제 시 자동 삭제됨
        await this.movieRepository.delete(movie);

        return id;
      }
    }

    ```

</details>

<a id="28aeda9b0fe18038bc75de5d2b8c3c13"></a>

```typescript
import { Injectable, NotFoundException } from '@nestjs/common';
import { CreateMovieDto } from './dto/create-movie.dto';
import { UpdateMovieDto } from './dto/update-movie.dto';
import { InjectRepository } from '@nestjs/typeorm';
import { Movie } from './entities/movie.entity';
import { DataSource, In, Like, Repository } from 'typeorm';
import { MovieDetail } from './entities/movie-datail.entity';
import { Director } from 'src/director/entities/director.entity';
import { Genre } from 'src/genre/entities/genre.entity';
import { User } from 'src/user/entities/user.entity';

@Injectable()
export class MovieService {
  constructor(
    @InjectRepository(Movie)
    private readonly movieRepository: Repository<Movie>,
    @InjectRepository(MovieDetail)
    private readonly movieDetailRepository: Repository<MovieDetail>,
    @InjectRepository(Director)
    private readonly directorRepository: Repository<Director>,
    @InjectRepository(Genre)
    private readonly genreRepository: Repository<Genre>,
    private readonly dataSource: DataSource,
  ) {}

  async findAll(title?: string) {
    const qb = this.dataSource
      .getRepository(Movie)
      .createQueryBuilder('movie')
      .leftJoinAndSelect('movie.director', 'director')
      .leftJoinAndSelect('movie.genres', 'genres')
      .leftJoinAndSelect('movie.detail', 'detail');

    if (title) {
      qb.where('movie.title LIKE :title', { title: `%${title}%` });
    }

    const [movies, count] = await qb.getManyAndCount();
    return { movies, count };
  }

  async findOne(id: number) {
    const movie = await this.dataSource
      .getRepository(Movie)
      .createQueryBuilder('movie')
      .leftJoinAndSelect('movie.detail', 'detail')
      .leftJoinAndSelect('movie.director', 'director')
      .leftJoinAndSelect('movie.genres', 'genres')
      .leftJoinAndSelect('movie.creator', 'creator')
      .where('movie.id = :id', { id })
      .getOne();

    if (!movie) {
      throw new NotFoundException('존재하지 않는 영화입니다.');
    }

    return movie;
  }

  async create(createMovieDto: CreateMovieDto, creator: User) {
    // 1. Director 검증
    const director = await this.dataSource
      .getRepository(Director)
      .createQueryBuilder('director')
      .where('director.id = :id', { id: createMovieDto.directorId })
      .getOne();

    if (!director) {
      throw new NotFoundException('존재하지 않는 Director 입니다.');
    }

    // 2. Genres 검증

    const genres = await this.validateGenres(createMovieDto.genreIds);

    // 3. MovieDetail 생성
    const movieDetail = this.dataSource.getRepository(MovieDetail).create({
      detail: createMovieDto.detail,
    });
    const savedDetail = await this.dataSource
      .getRepository(MovieDetail)
      .save(movieDetail);

    // 4. Movie 생성
    const movie = this.dataSource.getRepository(Movie).create({
      title: createMovieDto.title,
      director,
      detail: savedDetail,
      genres,
      creator,
    });

    const savedMovie = await this.dataSource.getRepository(Movie).save(movie);

    // 4. 한 번의 save로 Movie + MovieDetail + ManyToMany genres 연결

    return this.dataSource
      .getRepository(Movie)
      .createQueryBuilder('movie')
      .leftJoinAndSelect('movie.detail', 'detail')
      .leftJoinAndSelect('movie.director', 'director')
      .leftJoinAndSelect('movie.genres', 'genres')
      .leftJoinAndSelect('movie.creator', 'creator')
      .where('movie.id = :id', { id: savedMovie.id })
      .getOne();
  }

  async update(id: number, updateMovieDto: UpdateMovieDto) {
    const movie = await this.dataSource
      .getRepository(Movie)
      .createQueryBuilder('movie')
      .leftJoinAndSelect('movie.detail', 'detail')
      .leftJoinAndSelect('movie.genres', 'genres')
      .leftJoinAndSelect('movie.director', 'director')
      .where('movie.id = :id', { id })
      .getOne();

    if (!movie) {
      throw new NotFoundException('존재하지 않는 영화입니다.');
    }

    const { detail, directorId, genreIds, ...movieRest } = updateMovieDto;

    // 1. Movie 필드 업데이트
    Object.assign(movie, movieRest);

    // 2. detail 업데이트
    if (detail) {
      movie.detail.detail = detail;
    }

    // 3. director 교체
    if (directorId) {
      const director = await this.dataSource
        .getRepository(Director)
        .createQueryBuilder('director')
        .where('director.id = :id', { id: directorId })
        .getOne();

      if (!director) {
        throw new NotFoundException('존재하지 않는 감독입니다. ');
      }

      movie.director = director;
    }

    // 4. genres 교체
    if (genreIds) {
      const genres = await this.validateGenres(genreIds);

      movie.genres = genres;
    }

    await this.dataSource.getRepository(Movie).save(movie);

    return this.dataSource
      .getRepository(Movie)
      .createQueryBuilder('movie')
      .leftJoinAndSelect('movie.detail', 'detail')
      .leftJoinAndSelect('movie.director', 'director')
      .leftJoinAndSelect('movie.genres', 'genres')
      .where('movie.id = :id', { id })
      .getOne();
  }

  async remove(id: number) {
    const movie = await this.dataSource
      .getRepository(Movie)
      .createQueryBuilder('movie')
      .where('movie.id = :id', { id })
      .getOne();

    if (!movie) {
      throw new NotFoundException('존재하지 않는 영화입니다.');
    }

    await this.dataSource.getRepository(Movie).delete({ id });

    return id;
  }

  private async validateGenres(ids: string[]): Promise<Genre[]> {
    const genres = await this.genreRepository
      .createQueryBuilder('genre')
      .where('genre.id IN (:...ids)', { ids })
      .getMany();

    if (genres.length !== ids.length) {
      const foundIds = genres.map((g) => g.id);
      const missingIds = ids
        .map((id) => Number(id))
        .filter((id) => !foundIds.includes(id));

      throw new NotFoundException(
        `존재하지 않는 장르가 있습니다. ids: ${missingIds.join(',')}`,
      );
    }

    return genres;
  }
}
```

</details>

<a id="28aeda9b0fe180b69e7cf026f839e1c8"></a>

### 비교&#58; <code>Query Builder</code>  vs  <code>Repository&#46;method</code>

<details>
<summary><code>findAll()</code></summary>

<a id="28aeda9b0fe180afb513f68462819dd0"></a>

```typescript
async findAll(title?: string) {
  const qb = this.dataSource
    .getRepository(Movie)
    .createQueryBuilder('movie')
    .leftJoinAndSelect('movie.director', 'director')
    .leftJoinAndSelect('movie.genres', 'genres')
    .leftJoinAndSelect('movie.detail', 'detail');

  if (title) {
    qb.where('movie.title LIKE :title', { title: `%${title}%` });
  }

  const [movies, count] = await qb.getManyAndCount();
  return { movies, count };
}
```

<a id="28aeda9b0fe1807d9539d22e3b3626f3"></a>

```typescript
async findAll(title?: string) {
  // title 이 없는 경우
  if (!title) {
    return [
      await this.movieRepository.find({
        relations: ['director', 'genres'],
      }),
      await this.movieRepository.count(),
    ];
  }

  // title이 있는 경우
  return this.movieRepository.findAndCount({
    where: {
      title: Like(`%${title}%`),
    },
    relations: ['director', 'genres'],
  });
}
```

</details>

<details>
<summary><code>findOne()</code></summary>

<a id="28aeda9b0fe1806585cbd32538c977b9"></a>

```typescript
async findOne(id: number) {
  const movie = await this.dataSource
    .getRepository(Movie)
    .createQueryBuilder('movie')
    .leftJoinAndSelect('movie.detail', 'detail')
    .leftJoinAndSelect('movie.director', 'director')
    .leftJoinAndSelect('movie.genres', 'genres')
    .leftJoinAndSelect('movie.creator', 'creator')
    .where('movie.id = :id', { id })
    .getOne();

  if (!movie) {
    throw new NotFoundException('존재하지 않는 영화입니다.');
  }

  return movie;
}
```

<a id="28aeda9b0fe180b5907cd9562c87dea2"></a>

```typescript
async findOne(id: number) {
  const movie = await this.movieRepository.findOne({
    where: {
      id,
    },
    relations: ['detail', 'director', 'genres'],
  });

  if (!movie) {
    throw new NotFoundException('존재하지 않는 영화입니다.');
  }

  return movie;
}
```

</details>

<details>
<summary><code>create()</code></summary>

<a id="28aeda9b0fe180fa8a70eeb1f0c9fea8"></a>

```typescript
async create(createMovieDto: CreateMovieDto, creator: User) {
  // 1. Director 검증
  const director = await this.dataSource
    .getRepository(Director)
    .createQueryBuilder('director')
    .where('director.id = :id', { id: createMovieDto.directorId })
    .getOne();

  if (!director) {
    throw new NotFoundException('존재하지 않는 Director 입니다.');
  }

  // 2. Genres 검증

  const genres = await this.validateGenres(createMovieDto.genreIds);

  // 3. MovieDetail 생성
  const movieDetail = this.dataSource.getRepository(MovieDetail).create({
    detail: createMovieDto.detail,
  });
  const savedDetail = await this.dataSource
    .getRepository(MovieDetail)
    .save(movieDetail);

  // 4. Movie 생성
  const movie = this.dataSource.getRepository(Movie).create({
    title: createMovieDto.title,
    director,
    detail: savedDetail,
    genres,
    creator,
  });

  const savedMovie = await this.dataSource.getRepository(Movie).save(movie);

  return this.dataSource
    .getRepository(Movie)
    .createQueryBuilder('movie')
    .leftJoinAndSelect('movie.detail', 'detail')
    .leftJoinAndSelect('movie.director', 'director')
    .leftJoinAndSelect('movie.genres', 'genres')
    .leftJoinAndSelect('movie.creator', 'creator')
    .where('movie.id = :id', { id: savedMovie.id })
    .getOne();
}

private async validateGenres(ids: string[]): Promise<Genre[]> {
  const genres = await this.genreRepository
    .createQueryBuilder('genre')
    .where('genre.id IN (:...ids)', { ids })
    .getMany();

  if (genres.length !== ids.length) {
    const foundIds = genres.map((g) => g.id);
    const missingIds = ids
      .map((id) => Number(id))
      .filter((id) => !foundIds.includes(id));

    throw new NotFoundException(
      `존재하지 않는 장르가 있습니다. ids: ${missingIds.join(',')}`,
    );
  }

  return genres;
}
```

<a id="28aeda9b0fe1807bbad1ca6709a81ad6"></a>

```typescript
async create(createMovieDto: CreateMovieDto, creator: User) {
  // 1. Director 검증
  const director = await this.directorRepository.findOne({
    where: { id: createMovieDto.directorId },
  });

  if (!director) {
    throw new NotFoundException('존재하지 않는 Director 입니다.');
  }

  // 2. Genres 검증
  const genres = await this.genreRepository.findBy({
    id: In(createMovieDto.genreIds),
  });

  if (genres.length !== createMovieDto.genreIds.length) {
    throw new NotFoundException(
      `존재하지 않는 장르가 있습니다. ids: ${genres.map((genre) => genre.id).join(',')}`,
    );
  }

  // 3. Movie 생성
  const movie = this.movieRepository.create({
    title: createMovieDto.title,
    director,
    detail: { detail: createMovieDto.detail }, // cascade로 MovieDetail 자동 저장
    genres,
    creator,
  });

  // 4. 한 번의 save로 Movie + MovieDetail + ManyToMany genres 연결
  const savedMovie = await this.movieRepository.save(movie);

  return await this.movieRepository.findOne({
    where: { id: savedMovie.id },
    relations: ['detail', 'director', 'genres', 'creator'],
  });
}
```

</details>

<details>
<summary><code>update()</code></summary>

<a id="28aeda9b0fe18075ba45e668262c4ecc"></a>

```typescript
async update(id: number, updateMovieDto: UpdateMovieDto) {
    const movie = await this.dataSource
      .getRepository(Movie)
      .createQueryBuilder('movie')
      .leftJoinAndSelect('movie.detail', 'detail')
      .leftJoinAndSelect('movie.genres', 'genres')
      .leftJoinAndSelect('movie.director', 'director')
      .where('movie.id = :id', { id })
      .getOne();

    if (!movie) {
      throw new NotFoundException('존재하지 않는 영화입니다.');
    }

    const { detail, directorId, genreIds, ...movieRest } = updateMovieDto;

    // 1. Movie 필드 업데이트
    Object.assign(movie, movieRest);

    // 2. detail 업데이트
    if (detail) {
      movie.detail.detail = detail;
    }

    // 3. director 교체
    if (directorId) {
      const director = await this.dataSource
        .getRepository(Director)
        .createQueryBuilder('director')
        .where('director.id = :id', { id: directorId })
        .getOne();

      if (!director) {
        throw new NotFoundException('존재하지 않는 감독입니다. ');
      }

      movie.director = director;
    }

    // 4. genres 교체
    if (genreIds) {
      const genres = await this.validateGenres(genreIds);

      movie.genres = genres;
    }

    await this.dataSource.getRepository(Movie).save(movie);

    return this.dataSource
      .getRepository(Movie)
      .createQueryBuilder('movie')
      .leftJoinAndSelect('movie.detail', 'detail')
      .leftJoinAndSelect('movie.director', 'director')
      .leftJoinAndSelect('movie.genres', 'genres')
      .where('movie.id = :id', { id })
      .getOne();
  }
```

<a id="28aeda9b0fe1809ebfcae0400613e488"></a>

```typescript
async update(id: number, updateMovieDto: UpdateMovieDto) {
  const movie = await this.movieRepository.findOne({
    where: { id },
    relations: ['detail', 'genres', 'director'],
  });

  if (!movie) {
    throw new NotFoundException('존재하지 않는 영화입니다.');
  }

  const { detail, directorId, genreIds, ...movieRest } = updateMovieDto;

  // 1. Movie 필드 업데이트
  Object.assign(movie, movieRest);

  // 2. detail 업데이트
  if (detail) {
    movie.detail.detail = detail;
  }

  // 3. director 교체
  if (directorId) {
    const director = await this.directorRepository.findOne({
      where: { id: directorId },
    });

    if (!director) {
      throw new NotFoundException('존재하지 않는 감독입니다. ');
    }

    movie.director = director;
  }

  // 4. genres 교체
  if (genreIds) {
    const genres = await this.genreRepository.findBy({ id: In(genreIds) });

    if (genres.length !== updateMovieDto.genreIds?.length) {
      throw new NotFoundException(
        `존재하지 않는 장르가 있습니다. ids:  ${genres.map((genre) => genre.id).join(',')}`,
      );
    }

    movie.genres = genres;
  }

  await this.movieRepository.save(movie);

  return this.movieRepository.findOne({
    where: { id },
    relations: ['detail', 'director', 'genres'],
  });
}
```

</details>

<details>
<summary><code>remove()</code></summary>

<a id="28aeda9b0fe180dd8ef9d016719ac756"></a>

```typescript
async remove(id: number) {
  const movie = await this.dataSource
    .getRepository(Movie)
    .createQueryBuilder('movie')
    .where('movie.id = :id', { id })
    .getOne();

  if (!movie) {
    throw new NotFoundException('존재하지 않는 영화입니다.');
  }

  await this.dataSource.getRepository(Movie).delete({ id });

  return id;
}
```

<a id="28aeda9b0fe180f9b4d2d813c61b408c"></a>

```typescript
async remove(id: number) {
  const movie = await this.movieRepository.findOne({
    where: { id },
  });

  if (!movie) {
    throw new NotFoundException('존재하지 않는 영화입니다.');
  }

  // detail은 cascade: true 설정으로 삭제 시 자동 삭제됨
  await this.movieRepository.delete(movie);

  return id;
}
```

</details>
