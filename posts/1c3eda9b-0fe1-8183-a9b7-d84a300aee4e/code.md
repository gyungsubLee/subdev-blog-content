---
order: 0
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 1c3eda9b-0fe1-8183-a9b7-d84a300aee4e
title: code
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 1c3eda9b-0fe1-81e5-a912-c23dfb0cbee3
    title: 알고리즘
  - id: 1c3eda9b-0fe1-81dc-9260-fa89456b4fa7
    title: "[인프런] 알고리즘-자바(초급)"
  - id: 1c3eda9b-0fe1-817b-b022-cacd442a920c
    title: 12. 토마토(BFS)
  - id: 1c3eda9b-0fe1-8183-a9b7-d84a300aee4e
    title: code
excerpt: java import java.lang.reflect.Array; import java.util.; public class Main { public int Solution(int n, ArrayList arr){ Collections.sort(arr); for(int i=0; i arr = new ArrayList<();
cover: null
icon: null
notionProperties: {}
schema_version: 1
parent_id: 1c3eda9b-0fe1-817b-b022-cacd442a920c
created: 2025-03-27T07:47:31.359Z
updated: 2025-03-27T07:47:31.359Z
legacy_path: Main/알고리즘-c23dfb0cbee3/[인프런] 알고리즘-자바(초급)-fa89456b4fa7/12. 토마토(BFS)-cacd442a920c/code-d84a300aee4e/index.md
legacy_category: 알고리즘
source_url: https://beautiful-college-c84.notion.site/1c3eda9b0fe18183a9b7d84a300aee4e
---
<a id="1c3eda9b0fe181edbe2df87dec252d70"></a>

```java
import java.lang.reflect.Array;
import java.util.*;





public class Main {
    public int Solution(int n, ArrayList<Time> arr){
        Collections.sort(arr);
        for(int i=0; i<arr.size(); i++){
            System.out.println(arr.get(i).time + " "+ arr.get(i).state);
        }
        int answer=0, cnt=0;
        for(Time ob : arr){
            if(ob.state=='s')  cnt++;
            else cnt--;
            answer=Math.max(answer, cnt);
        }
        return answer;
    }

    public static void main (String[] args){
        Main T = new Main();
        Scanner sc = new Scanner(System.in);
        int n=sc.nextInt();
        ArrayList<Time> arr = new ArrayList<>();
        for(int i=0; i<n; i++){
            int s=sc.nextInt();
            arr.add(new Time(s, 's'));
            int e=sc.nextInt();
            arr.add(new Time(e, 'e'));
        }
        System.out.println(T.Solution(n, arr));
    }
}
```
