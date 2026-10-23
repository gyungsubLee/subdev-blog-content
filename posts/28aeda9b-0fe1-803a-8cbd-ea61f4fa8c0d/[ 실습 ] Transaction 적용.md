---
order: 1
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 28aeda9b-0fe1-803a-8cbd-ea61f4fa8c0d
title: "[ 실습 ] Transaction 적용"
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 226eda9b-0fe1-802b-a035-c3a886768c4d
    title: Nest.js
  - id: 260eda9b-0fe1-801b-836b-c2e229a88ff9
    title: 한 번에 끝내는 NestJS 패키지 - Part 1. 기초
  - id: 274eda9b-0fe1-8023-ba05-d84527f93ae0
    title: DB ( SQL, TypeORM, QueryBuilder, Transaction, Migration )
  - id: 28aeda9b-0fe1-803a-8cbd-ea61f4fa8c0d
    title: "[ 실습 ] Transaction 적용"
excerpt: 목차 - Transaction 적용 - 1. NestJS에서의 트랜잭션 처리 - 2. Create 함수에 Transaction 적용 - 3. Update 함수에 Transaction 적용 - 4. 공통된 Transaction 패턴 → Interceptor 계층으로 분리 Transaction 적용 --- 1. NestJS에
cover: null
icon: null
notionProperties: {}
schema_version: 1
parent_id: 274eda9b-0fe1-8023-ba05-d84527f93ae0
created: 2025-10-12T04:58:54.621Z
updated: 2025-10-21T04:41:03.681Z
legacy_path: Main/Nest.js-c3a886768c4d/한 번에 끝내는 NestJS 패키지 - Part 1. 기초-c2e229a88ff9/DB ( SQL, TypeORM, QueryBuilder, Transaction,-d84527f93ae0/[ 실습 ] Transaction 적용-ea61f4fa8c0d/index.md
legacy_category: Nest.js
source_url: https://beautiful-college-c84.notion.site/28aeda9b0fe1803a8cbdea61f4fa8c0d
---
> 
> 
> <a id="28aeda9b0fe180d6872fc302fd594de9"></a>
> 
> <strong>목차</strong>
> 
> - [Transaction 적용](#28aeda9b0fe18000a064c532a0577e51)
> - [ 1. NestJS에서의 트랜잭션 처리](#28beda9b0fe1801bbd4fffdaf5476f43)
> - [ 2. Create 함수에 Transaction 적용](#28aeda9b0fe18064a187fcdae6c122d1)
> - [ 3. Update 함수에  Transaction 적용](#28aeda9b0fe180fba7f0e5f1314cc025)
> - [ 4.  공통된 Transaction 패턴 → Interceptor 계층으로 분리](#28aeda9b0fe18028bccee4f433b93746)

<a id="28aeda9b0fe18000a064c532a0577e51"></a>

## Transaction 적용

---

<a id="28beda9b0fe1801bbd4fffdaf5476f43"></a>

###  1&#46; NestJS에서의 트랜잭션 처리

<details>
<summary>1&#46;  DataSource 불러오기</summary>

<a id="28beda9b0fe18083a292c225a716a7cf"></a>

```typescript
import { DataSource, ... } from 'typeorm';

@Injectable()
export class MovieService {
		constructor(
			
			@InjectRepository(Movie)
			private readonly movieRepository: Repository<Movie>,
			
			 ...
			 
			 private readonly dataSource: DataSource,  // typeorm에서 가져오기 때문에, 따로 InjectRepository 선언이 필요하지 않다. 
		) {}
}
```

</details>

<details>
<summary>2&#46; 트랜잭션 처리</summary>

<a id="28beda9b0fe1807ea58af37b5299f5d9"></a>

```typescript
async Method(dto: DTO) {
		const qr = this.dataSource.createQueryRunner();
		
		await qr.connect();
		await qr.startTransaction();
		
		try {
		
				// 비지니스 로직
				
				await qr.commitTransaction();
		} catch(e) {
				await qr.rollbackTransaction();
				throw e;
		} finally {
				await qr.release();
		}
}
```

</details>

<a id="28aeda9b0fe18064a187fcdae6c122d1"></a>

###  2&#46; Create 함수에 Transaction 적용

<details>
<summary>&#91; 코드 &#93; <code>movieService&#46;create()</code></summary>

<a id="28aeda9b0fe180c19544f2814e2cc089"></a>

```typescript
async create(dto: CreateMovieDto) {
		const qr = this.dataSource.createQueryRunner();
		
		await qr.connect();
		await qr.startTransaction();
		
		try {
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
				
				await qr.commitTransaction();
		} catch(e) {
				await qr.rollbackTransaction();
				throw e;
		} finally {
				await qr.release();
		}
}
```

</details>

<a id="28aeda9b0fe180fba7f0e5f1314cc025"></a>

###  3&#46; Update 함수에  Transaction 적용

<details>
<summary>&#91; 코드 &#93; <code>movieService&#46;update()</code></summary>

<a id="28beda9b0fe1800ab8b0d77794dd0dc7"></a>

```typescript
async update(id: number, updateMovieDto: UpdateMovieDto) {

		const qr = this.dataSource.createQueryRunner();
		
		await qr.connect();
		await qr.startTransaction();
		
		try {
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
		      
    		await qr.commitTransaction();
		} catch(e) {
				await qr.rollbackTransaction();
				throw e;
		} finally {
				await qr.release();
		}
}
```

</details>

<a id="28aeda9b0fe18028bccee4f433b93746"></a>

###  4&#46;  공통된 Transaction 패턴 → Interceptor 계층으로 분리

<details>
<summary>1&#46;  인터셉터 생성</summary>

- <strong>&#91; 코드 &#93; </strong><strong><code>TransactionInterceptor</code></strong>
    <a id="28beda9b0fe18024b5d4c84f5a5aa11b"></a>

    ```typescript
    import {
      CallHandler,
      ExecutionContext,
      Injectable,
      NestInterceptor,
    } from '@nestjs/common';
    import { catchError, Observable, tap } from 'rxjs';
    import { DataSource } from 'typeorm';

    @Injectable()
    export class TransactionInterceptor implements NestInterceptor {
      constructor(private readonly dataSource: DataSource) {}

      async intercept(
        context: ExecutionContext,
        next: CallHandler<any>,
      ): Promise<Observable<any>> {
        const req = context.switchToHttp().getRequest();

        const qr = this.dataSource.createQueryRunner();

        await qr.connect();
        await qr.startTransaction();

        req.queryRunner = qr; // req에 queryRunner를 붙임 (서비스가 사용 가능)

        return next.handle().pipe(
          catchError(async (e) => {
            await qr.rollbackTransaction();
            await qr.release();
            throw e;
          }),
          tap(async () => {
            await qr.commitTransaction();
            await qr.release();
          }),
        );
      }
    }
    ```

</details>

<details>
<summary>2&#46; 글로벌 스코프로 해당 인터셉터 등록</summary>

<a id="28beda9b0fe180ea9242cefed23e8b04"></a>

```typescript
@Module({
	...
		providers: [
	    {
	      provide: APP_INTERCEPTOR,
	      useClass: TransactionInterceptor,
	    },
	    
	    ...
    ],
})
export class AppModule implements NestModule { ... }
```

<details>
<summary>&#91; 전체 코드 &#93; AppModule</summary>

<a id="28beda9b0fe180cab796dca945d1460a"></a>

```typescript
import {
  MiddlewareConsumer,
  Module,
  NestModule,
  RequestMethod,
} from '@nestjs/common';
import { TypeOrmModule } from '@nestjs/typeorm';
import { User } from './user/entities/user.entity';
import { AuthModule } from './auth/auth.module';
import { UserModule } from './user/user.module';
import { ConfigModule, ConfigService } from '@nestjs/config';
import { SnakeNamingStrategy } from 'typeorm-naming-strategies';
import * as Joi from 'joi';
import { BearerTokenMiddleware } from './auth/middlware/bearer-token.middleware';
import { APP_FILTER, APP_GUARD, APP_INTERCEPTOR } from '@nestjs/core';
import { AuthGuard } from './auth/guard/auth.guard';
import { RBACGuard } from './auth/guard/rbac.guard';
import { ResponseTimeInterceptor } from './common/interceptor/response-time.interceptor';
import { CacheInterceptor } from './common/interceptor/cache.interceptor';
import { TransactionInterceptor } from './common/interceptor/transaction.interceptor';
import { DirectorModule } from './director/director.module';
import { GenreModule } from './genre/genre.module';
import { MovieModule } from './movie/movie.module';
import { Movie } from './movie/entities/movie.entity';
import { MovieDetail } from './movie/entities/movie-datail.entity';
import { Genre } from './genre/entities/genre.entity';
import { Director } from './director/entities/director.entity';
import { ForbiddenExceptionFilter } from './common/filter/forbidden.filter';
import { QueryFailedExceptionFilter } from './common/filter/query-failed.filter';
import { AllExceptionsFilter } from './common/filter/http-exception.filter';
import { CommonResponseInterceptor } from './common/interceptor/common-response.interceptor';

@Module({
  imports: [
    ConfigModule.forRoot({
      isGlobal: true,
      validationSchema: Joi.object({
        ENV: Joi.string().valid('dev', 'prod').required(),
        DB_TYPE: Joi.string().valid('postgres').required(),
        DB_HOST: Joi.string().required(),
        DB_USERNAME: Joi.string().required(),
        DB_PASSWORD: Joi.string().required(),
        DB_DATABASE: Joi.string().required(),
        HASH_ROUNDS: Joi.number().required(),
        ACCESS_TOKEN_SECRET: Joi.string().required(),
        REFRESH_TOKEN_SECRET: Joi.string().required(),
      }),
    }),
    TypeOrmModule.forRootAsync({
      inject: [ConfigService],
      useFactory: (cfg: ConfigService) => ({
        type: cfg.get<string>('DB_TYPE') as 'postgres',
        host: cfg.get<string>('DB_HOST'),
        port: cfg.get<number>('DB_PORT'),
        username: cfg.get<string>('DB_USERNAME'),
        password: cfg.get<string>('DB_PASSWORD'),
        database: cfg.get<string>('DB_DATABASE'),
        entities: [User, Movie, MovieDetail, Genre, Director],
        synchronize: cfg.get<string>('DB_TYPE') === 'prod' ? false : true, // 운영에서는 반드시 false
        logging: true,
        namingStrategy: new SnakeNamingStrategy(),
      }),
    }),
    AuthModule,
    UserModule,
    DirectorModule,
    GenreModule,
    MovieModule,
  ],
  providers: [
    // AuthGuard -> RBACGuard
    {
      provide: APP_GUARD,
      useClass: AuthGuard,
    },
    {
      provide: APP_GUARD,
      useClass: RBACGuard,
    },
    {
      provide: APP_INTERCEPTOR,
      useClass: ResponseTimeInterceptor,
    },
    {
      provide: APP_INTERCEPTOR,
      useClass: CommonResponseInterceptor,
    },
    {
      provide: APP_INTERCEPTOR,
      useClass: TransactionInterceptor,
    },
    {
      provide: APP_FILTER,
      useClass: ForbiddenExceptionFilter,
    },
    {
      provide: APP_FILTER,
      useClass: AllExceptionsFilter,
    },
    {
      provide: APP_FILTER,
      useClass: QueryFailedExceptionFilter,
    },
  ],
})
export class AppModule implements NestModule {
  configure(consumer: MiddlewareConsumer) {
    consumer
      .apply(BearerTokenMiddleware)
      .exclude(
        { path: '/auth/register/user', method: RequestMethod.POST },
        { path: '/auth/register/admin', method: RequestMethod.POST },
        { path: '/auth/login', method: RequestMethod.POST },
      )
      .forRoutes('*'); // 모든 라우터 계층에 적용
  }
}
```

</details>

</details>

<details>
<summary>3&#46; 비지니스 로직(Service 레이어)에서 사용</summary>

<a id="28beda9b0fe180e7afede3c0ec94f8d2"></a>

```typescript
// controller.ts 
// interceptor 붙인 queryRunner를 service 계층으로 넘김
@Post()
async create(@Req() req, @Body() dto: CreateDto) {
  return this.myService.create(req.queryRunner, dto);
}
```

<a id="28beda9b0fe1802ead28da0b141952f2"></a>

```typescript
// service.ts
@Injectable()
export class MyService {
  async create(qr: QueryRunner, dto: CreateDto) {
    const manager = qr.manager;  // interceptor에서 받아온 매니저로 DB 조작

		// 받아온 매니저로 조작하기 때문에 transaction 내에서 동자함 
    const entity = manager.create(MyEntity, dto);
    await manager.save(entity); 
    
    return entity;
  }
}
```

</details>

<details>
<summary>3&#46;2 <strong><u>커스텀 데코레이터</u></strong>(<strong><code>&#64;QueryRunner</code></strong><strong><u>)</u></strong>로 불러와 비지니스 로직(Service 레이어)에 사용</summary>

<a id="293eda9b0fe1806b9e60c91a53d2c293"></a>

```typescript
// src/common/decorator/query-runner.decorator.ts
import { createParamDecorator, ExecutionContext, InternalServerErrorException } from "@nestjs/common";

export const QueryRunner = createParamDecorator(
    (data: any, context: ExecutionContext) => {
        const request = context.switchToHttp().getRequest();

        if(!request || !request.queryRunner){
            throw new InternalServerErrorException('Query Runner 객체를 찾을 수 없습니다!')
        }

        return request.queryRunner;
    }
);
```

<a id="28beda9b0fe180868c2ce7b75ad4d989"></a>

```typescript
import { QueryRunner } from 'src/common/decorator/query-runner.decorator';
import { QueryRunner as QR } from 'typeorm';

...

@Controller('movie')
@UseInterceptors(ClassSerializerInterceptor)
export class MovieController {

  @UseInterceptors(TransactionInterceptor)
  postMovie(
    @Body() body: CreateMovieDto,
    @QueryRunner() queryRunner: QR,
    @UserId() userId: number,
  ) {
    return this.movieService.create(
      body,
      userId,
      queryRunner,
    );
  }
  
  ...
```

</details>
