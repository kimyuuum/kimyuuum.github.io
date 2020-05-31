---
layout:	post
title:	"Prim Algorithm"
date:	2020-05-31 12:29:00
category: [computerscience]


---



## [Algorithm] Prim Algorithm

<br/>

<br/>

#### Kruskal과의 차이

: 프림 알고리즘은 한 정점을 기점으로 확장한다. (kruskal은 간선의 가중치 중심)

<br/>

#### Time Complexity

+ pq에 간선은 각각 1번씩 삽입/삭제된다. 
+ O(ElogE) / Insert : O(logE) , Delete : O(logE)

<br/>

#### Flow

1. 하나의 정점을 선택하여 최소 신장 트리에 추가한다.

2. 최소 신장 트리에 포함된 정점과 최소 신장 트리에 포함되지 않은 정점을 연결하는 간선 중, 비용이 가장 작은것을 최소 신장 트리에 추가한다.

   ⇒ 해당 간선의 최소 신장 트리에 포함되지 않은 정점도 추가한다.

3. 간선이 V-1개가 될 때까지 2를 반복한다.

<br/>

---------------

<br/>

#### Implementation

: 프림 알고리즘은 Heap으로 구현해야 Time Complexity가 효율적이다.

1. 하나의 정점을 선택해서 MST에 추가하고, 정점과 연결된 모든 간선을 heap에 push한다.
2. min heap에서 가장 가중치가 낮은 간선을 pop한다.
3. 1. 만약 간선이 MST에 포함된 두 정점 간의 간선인 경우, continue;
   2. 간선 **u는 MST에 포함되고, v는 포함되지 않은 경우 이를 연결하는 간선과, v를 MST에 포함**시킨다.
4. 간선이 V-1개가 될 때까지 반복한다.

<br/>

```cpp
	
	priority_queue<pair<int,pair<int,int>>, 
                 vector<pair<int,pair<int,int>>>,
                 greater<pair<int,pair<int,int>>>> pq;

  int vec, e;

  vector<pair<int,int>> adj[MAX]; //cost , vertex
  bool checked[MAX];

  void Prim(){
    int cnt = 0;
    for(int i=0; i<adj[1].size(); i++){
      pq.push(make_pair(adj[1][i].first,make_pair(1,adj[1][i].second)));
    }
    checked[1] = true;

    while(1){
      int cost = pq.top().first;
      int v = pq.top().second.second;
      pq.pop();

      if(checked[v]){
        continue;
      }

      checked[v] = true;
      cnt++;
      if(cnt == v-1)
        break;

      for(int i=0; i<adj[v].size(); i++){
        int node = adj[v][i].second;
        if(checked[node]){
          continue;
        }
        pq.push(make_pair(adj[v][i].first,make_pair(v,adj[v][i].second)));
      }
    }

  }


```



<br/>

<br/>