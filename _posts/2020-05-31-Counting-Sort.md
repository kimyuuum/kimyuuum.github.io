---
layout:	post
title:	"Sort - Counting Sort"
date:	2020-05-31 02:15:00
category: [computerscience]




---



## [Sort] Counting Sort

<br/>

<br/>



**선형 시간에 정렬하기 위해 사용한다.** 

<br/>

정렬하고자 하는 원소들의 값이 O(N)을 넘지 않는 경우 가능하다. 원소 간의 비교 정렬이 아니고, 크기가 한정되어있는 데이터일 경우 사용한다.

ex) arr[1...n]이 k를 넘지 않는 자연수여야 한다. 그래야 원소를 훑고, 각각 몇번 나타났는지 확인 가능하다.



#### Time Complexity 

+ O(N+K)   K : 배열에서 가장 큰 값.
+ 각 숫자가 나온 횟수를 세는 시간 O(N)
+ 다시 숫자를 원래 배열에 채워 넣는 시간 O(N)
+ 총 K번 반복 O(K)

#### Space Complexity

+  O(N+K)

+ 정렬을 위한 배열의 길이 O(N) , 계수를 위한 배열의 길이 O(K)

  

<br/>

#### FLOW

1. 각 값마다 몇개가 있는지 counting한다.
2. 위에서 만든 배열의 누적 합을 구하여, 배열에 저장한다.
3. 값을 하나씩 주고, 1씩 빼준다.

+ 숫자 크기에 시간 복잡도가 매우 큰 영향을 받는다.

  

<br/>

---------------------

<br/>

``` c++

  #include <iostream>
  #include <vector>
  using namespace std;
  const int MAX = 100;
  vector<int> v = {5, 5, 3, 4, 5, 1, 0, 4, 1, 3, 0, 2, 4, 2, 3, 0};
  int res[MAX];
  int c[10];

  int main() {
    for (int i = 0; i < v.size(); i++) {
      c[v[i]]++;
    }

    for (int i = 1; i < 10; i++) {
      c[i] += c[i - 1];
    }

    for (int i = v.size() - 1; i >= 0; i--) {
      int idx = c[v[i]];
      res[idx] = v[i];
      c[v[i]]--;
    }

    for (int i = 0; i < v.size(); i++) {
      cout << res[i] << " ";
    }
    return 0;
  }

```

<br/><br/>