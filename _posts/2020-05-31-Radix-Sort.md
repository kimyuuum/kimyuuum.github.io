---
layout:	post
title:	"Sort - Radix Sort"
date:	2020-05-31 02:09:00
category: [computerscience]



---



## [Sort] Radix Sort

<br/>

<br/>



**입력이 모두 K이하의 자리수를 가진 자연수인 특수한 경우에 사용 가능하다.** 



#### FLOW

1. 가장 낮은 자릿수만 가지고 재정렬한다.
2. 계속 자릿수를 올리면서 앞에 남은 자릿수가 없을 때 까지 정렬한다.

**안정성을 유지하며 정렬하는것이 중요하다. 비교정렬이 아니기 때문에 정수의 정렬에서 성능이 좋다.**



#### Time Complexity 

+ O(dN)  d : 가장 큰 수의 자릿수

<br/>



#### FLOW

1. 0-9까지의 값을 저장할 버킷을 준비한다.
2. 모든 숫자의 N(1,10,100 ...)의 자릿수를 해당 버킷에 분류한다.
3. 0-9까지의 버킷에 저장된 값을 순서대로 빼서 저장한다.
4. 자릿수를 늘려서 최대 자릿수까지 2,3번을 반복한다.

+ 버킷은 queue를 활용한다.

<br/>

---------------------

<br/>

``` c++

  #include <iostream>
  #include <queue>
  #include <vector>
  using namespace std;
  vector<int> v = {152, 73, 69, 41, 28, 1247, 2, 33, 674, 388};
  queue<int> q[10];

  int main() {
    int max = 1;
    for (int i = 0; i < v.size(); i++) {
      if (max < v[i]) {
        while (max < v[i]) {
          max *= 10;
        }
      }
    }

    int mod = 10;

    while (mod <= max) {
      for (int i = 0; i < v.size(); i++) {
        if (mod > v[i]) {
          q[0].push(v[i]);
        } else {
          int num = (v[i] / mod) % 10;
          q[num].push(v[i]);
        }
      }

      int idx = 0;
      for (int i = 0; i < 10; i++) {
        if (!q[i].empty()) {
          while (!q[i].empty()) {
            v[idx] = q[i].front();
            q[i].pop();
            idx++;
          }
        }
      }
      mod *= 10;
    }

    for (int i = 0; i < v.size(); i++) {
      cout << v[i] << " ";
    }
    return 0;
  }

```

<br/><br/>