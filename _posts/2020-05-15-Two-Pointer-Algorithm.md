---
layout:	post
title:	"Two Pointer Algorithm"
date:	2020-05-15 15:25:00
category: [ computer science ]
---



## [Two Pointer Algorithm]

<br/>

직관적으로 보았을 때, O(N^2) 이상으로 해결해야 하는 문제를, O(N)에 해결 가능하다.

<br/>



### 조건

연속되는 value들을 이용하여 특정 목표에 맞는 값을 찾아주는 알고리즘.

연속성을 활용하는 것이 특징이다.

주어진 값들을 그대로 활용하거나, 정렬을 통해서 연속성을 추가해줄 수 있는 경우에 사용 가능하다.

### <br/><br/>

### Example - 배열의 구간합이 특정 값을 만족해야하는 경우

- 배열의 원소가 모두 양수라면, 구간을 증가시킬 경우 구간합도 증가한다.

**만약 계속 커지다가 특정 수를 초과하면?**

⇒ left pointer를 증가시킨다.

<br/>

### FLOW

1. left = 0,  right = 0, sum = 0, num = 달성해야 하는 구간 합으로 설정한다.

2. while(1) 내에서

   1. `if(sum ≥ num)`

      ⇒ sum에서 arr[left]를 감소시키고, left idx를 증가시킨다

   2. 만약 right가 배열 마지막 idx까지 도달했을 경우 (arr의 size가 n일 경우 n)

      ⇒ 무한루프를 탈출한다.

   3. `if(sum < m)`

      ⇒ right idx를 증가시키고, sum += arr[right]을 실행한다.

**left idx를 먼저 체크해주어야 하는 이유**

:  2-1과 2-2의 FLOW가 변경될 경우, 그 전 상황에서 right를 증가시켰는데, right가 배열의 끝에 도달했다는 이유만으로 종료시킬 경우, left를 증가시키며 값을 계산할 수 없다.



<br/>



``` c++

while(1){
    if(sum >= num){
      left++;
      sum -= arr[left];
    }else if(right == n){
      break;
    }else{
      right++;
      sum += arr[right];
    }

    if(sum == num){
      //특정 조건 만족
    }
  }

```



<br/>

<br/>