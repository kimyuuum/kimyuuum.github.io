---
layout:	post
title:	"Sort - Topology Sort"
date:	2020-05-31 01:58:00
category: [computerscience]


---



## [Sort] Topology Sort

<br/>

<br/>

**방향이 있는 그래프에서 정점들을 정렬하는 방법. 방향 그래프에서 간선으로 주어진 정점 간에 선후관계를 위배하지 않도록 나열하는 정렬이다.**



#### DAG ( Directed Acyclic Graph)

+ 만약 그래프 내에 사이클이 존재하는 경우에는, 올바른 위상정렬이 불가하다. 그러므로 사이클이 존재하지 않는 방향 그래프여야 한다.



#### Time Complexity 

+ O(V+E)

<br/>



#### FLOW

1. 가장 앞에 오는 원소는 자신보다 앞에 위치하는 원소가 없어야 한다. `Indegree == 0 `
2. 매 순간마다 들어오는 간선이 없는 정점을 제거하며 정렬한다.



> 정점과 간선을 지울 필요 없이 미리 indegree의 개수를 저장해두었다가, 매번 뻗어나가는 정점들의 indegree 값을 감소시킨다.
> indegree가 0인 정점을 구하기 위해 매번 확인하는 대신, 목록(Queue)을 따로 저장하고 있다가, 직전 제거 정점에서 연결 정점을 추가해준다.



<br/>

---------------------

<br/>

#### Sorting

+ 위상정렬은 visited 배열이 필요없다. **모든 정점은 Indegree가 0이 되는 순간이 딱 한번**씩밖에 없기 때문이다.
+ 그래프에 사이클이 존재하는 경우, 애초에 Indegree가 0이 될 수 없어 큐가 비어있다.

1. 맨 처음, 모든 간선을 읽으며 Indegree 배열을 채운다.

2. `if(indegree[idx] == 0)` then `q.push(idx)`

3. 큐의 front에 있는 정점을 가져와서 위상정렬 큐에 추가한다.

4. 해당 정점으로부터 연결된 모든 정점의 Indegree값을 1 감소시킨다.

   -> 연결된 정점의 Indegree가 0이 되면 q.push(idx);

5. 큐가 empty일때까지 3,4를 반복한다.



``` c++

  #include <iostream>
  #include <queue>
  #include <vector>
  using namespace std;
  const int V = 32001;
  vector<int> adj[V];
  queue<int> q;
  vector<int> res;
  int indegree[V];
  int n, m;

  int main() {
    cin >> n >> m;
    for (int i = 0; i < m; i++) {
      int a, b;
      cin >> a >> b;
      adj[a].push_back(b);
      indegree[b]++;
    }

    for (int i = 1; i <= n; i++) {
      if (indegree[i] == 0) {
        q.push(i);
      }
    }

    while (!q.empty()) {
      int node = q.front();
      res.push_back(node);
      q.pop();

      for (int i = 0; i < adj[node].size(); i++) {
        int nextnode = adj[node][i];
        indegree[nextnode]--;
        if (indegree[nextnode] == 0) {
          q.push(nextnode);
        }
      }
    }

    for (int i = 0; i < res.size(); i++) {
      cout << res[i] << " ";
    }

    return 0;
  }

```



<br/><br/>