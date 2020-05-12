---
layout:	post
title:	"Dijkstra Algorithm"
date:	2020-05-11 03:25:00


---





## [Dijkstra Algorithm]

<br/>

**모든 간선 가중치가 음이 아닌 경우, 최단 경로를 구할 수 있다. 단일 시작점 최단 경로 알고리즘이다.** 



<br/>

<br/>

입력 그래프 G = (V,E)에서 간선들의 가중치가 모두 0 이상인 경우의 최단 경로 알고리즘이다.

``` c++
//pseudo code

Dijkstra(G,r){ // G = Graph, r = start node
	S = {}; // 정점의 집합
  for each u in V {
    d[u] = INF; //무한으로 초기화
  }
  d[r] = 0;
  while(S != V){
    u <- extractMin(V-S,d);
    S <- S union {u};
    for each v in L(u){ //L(u) : u로부터 연결된 정점들의 집합
      if(v in V-S && d[u] + w(u,v) < d[v]){
        d[v] = d[u] + w(u,v);
        prev[v] = u;
      }
    }
  }
}

extractMin(Q,d[]){
  집합 Q에서 d값이 가장 작은 u를 return한다.
}

```

<br/>

### Flow

1. start idx(r)를 집합 S의 첫 원소로 포함시킨다.

2. 정점 r에 연결된 집합 S의 바깥에 있는 정점을 살피고, 값을 기록한다.

3. 계산 최단거리가 가장 짧은 정점을 집합 S에 새롭게 포함시킨다. (a)

4. a에 연결된 정점들의 값이 INF -> 가중치를 더한 값으로 갱신된다.

   + 정점의 최단거리 값이 INF에서 바뀌는 것은, `최초로 시작 정점 r에서 이 정점에 이르는 경로가 발견` 될 때이다.

5. 이제 다음 최단거리 가중치를 가진 정점이 **target**이 된다.

6. 그 target ( b )를 S에 포함시킨다.

   => 정점의 최단거리가 INF가 아닌 수에서 갱신이 되는것은, `이미 경로는 발견되었지만 가중치의 값이 더 짧아졌을 때 이다.` 

<br/>

**Priority Queue(Heap)을 사용하여 구현 가능하다.** 

Time Complexity : O(Elog)V

Min Heap을 이용하면, 가장 적은 경로를 가진 정점이 나오도록 구현 가능하다.

<br/>

``` c++

#include <queue>
#include <vector>
using namespace std;

const int V = VERTEX;
const int E = EDGE;
const int INF = 987654321;

priority_queue<pair<int, int>, vector<pair<int, int>>, greater<pair<int, int>>>
    pq;
vector<pair<int,int>> v[E]; // 각 벡터간의 연결 요소 저장하기
int dist[V]; //최단거리 가중치 저장하기

int main(){
  int vertex,edge,k;
  cin>>vertex>>edge>>k;
  
  for(int i=1; i<=V; i++){
    if(i==K){ //출발점일 경우
      dist[i] = 0;
    }else{
      dist[i] = INF;
    }
  }
  
  for(int i=0; i<edge; i++){
    int a,b,cost;
    cin>>a>>b>>cost;
    v[a].push_back(make_pair(b,cost));
    //양방향 연결일 경우 아래 코드도 추가해준다.
    v[b].push_back(make_pair(a,cost));
  }
  
  pq.push(make_pair(0,K)); //출발점 먼저 pq에 push한다.
  
  while(!q.empty()){
    int cost = pq.top().first;
    int node = pq.top().second;
    pq.pop();
    
    if(dist[node] < cost){
      continue;
    }
    
    for(int i=0; i<v[node].size(); i++){
      int nextcost = v[node][i].second;
      int nextnode = v[node][i].first;
      
      if(nextcost < dist[nextnode]){
        dist[nextnode] = nextcost;
        pq.push(make_pair(nextcost,nextnode));
      }
    }
  }
  
  /*while문 수행 후, 갱신된 dist에는 출발점 k로부터 최단 경로의 가중치가 각각 저장되어있다.*/
}


```

<br/>

<br/>

