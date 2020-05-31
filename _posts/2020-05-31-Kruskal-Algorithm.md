---
layout:	post
title:	"Kruskal Algorithm"
date:	2020-05-31 10:59:00
category: [computerscience]


---



## [Algorithm] Kruskal Algorithm

<br/>

<br/>

**greedy하게 최소 신장트리를 구성한다.**



#### Greedy?

+ 그 당시 순간에 최적의 선택을 하는것. 전체적인 관점으로 최종 결정이 최종이라는 보장은 없다.



#### Time Complexity 

+ O(ElogE) : 간선 E개를 퀵정렬같은 알고리즘으로 정렬할 경우

<br/>



#### 신장트리

+ 주어진 방향성이 없는 그래프의 subgraph들 중에서 `모든 정점`을 포함하는 트리.

조건 

1. 모든 정점을 포함한다.

2. 트리구조이다. ( 사이클이 없고, 연결된 그래프이다. 그래프의 정점이 V개일때, 간선은 V-1개이다 )

   **SubGraph** : 주어진 그래프에서 일부 정점과 간선만을 선택해서 만든 새로운 그래프.



`최소 신장 트리` : 간선의 합이 최소인 트리 ( 동일한 그래프에서 여러가지로 나타낼 수 있다.)

<br/>

---------------------

<br/>

#### FLOW

+ 입력 : 가중치 그래프 G = ( V , E )
+ 출력 : MST를 이루는 간선들의 집합.

1. 간선을 가중치의 오름차순으로 정렬한다.
2. 가장 가중치가 낮은 간선에 연결되어있는 u와 v가 같은 집합인지 확인한다.
   + 같은 집합이면 continue
   + 다른 집합이라면 union find를 활용해 같은 집합으로 만든다. 그리고 간선은 MST에 추가한다.
3. 집합에 속한 간선의 개수가 V-1개일때까지 2번을 반복한다.

<br/>

#### Union Find

: 추가하고자 하는 간선의 양 끝 값이 같은 집합인지 체크하기 위해 사용된다. Kruskal에서 Time Complexity를 O(ElogE)로 줄여준다.



**Disjoint Set**

: 서로 중복되지 않는 부분집합으로 나눠진 원소에 대해서, 정보를 저장하고 조작한다. 서로 공통 원소가 없다.

1. 분할된 부분집합을 합치면 원래의 전체집합이 된다.
2. 분할 부분집합끼리는 중복 원소가 없다.

<br/>

+ `make-set(x)` : x를 유일한 원소로 하는 집합을 한개 만든다. (초기화)

+ `find(x)` : x가 포함된 집합의 root 원소가 무엇인지 찾는다. ( 찾기)

+ `union(x,y)` : x가 포함된 집합과 y가 포함된 집합을 하나로 합친다.



```c++

	// make-set
  for(int i=1; i<=MAX; i++){
    root[i] = i;
  }

	//find
  int find(int x){
    if(root[x] == x){
      return x;
    }

    int parent = root[x];
    return root[x] = find(parent);  //path compression : parent들도 한번에 root로 갱신해준다.
  }
	
	//union
  void union(int x, int y){
    x = find(x);
    y = find(y);

    if( x!=y ){
      root[y] = x;
    }
  }


```

<br/><br/>