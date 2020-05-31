---
layout:	post
title:	"Stable / Unstable Sort"
date:	2020-05-31 12:35:00
category: [computerscience]




---



## [Sort] Stable / Unstable Sort

<br/>

<br/>



#### Stable Sort

+  같은 key를 가진 record가 정렬 전,후에 순서가 뒤바뀌지 않는 경우이다.
+ bubble, insertion, merge



ex) 

**Merge sort**

​	1 2(1) | 3 2(2)

​	1 `2(1) 2(2)` 3 

​	=> 같은 값의 초기순서가 유지된다.

<br/>

--------------

<br/>

#### Unstable Sort

+ 같은 key를 가진 record가 정렬 전,후에 순서가 뒤바뀌는 경우
+ Quick, heap, selection



ex)

 **Quick sort**

4 2(1) 3 2(2)  // pivot = 4 , right = 2

pivot보다 오른쪽에 모두 작은 값이 존재하므로 right와 pivot을 swap한다. 

`2(2) 2(1)` 3 4 

=> 정렬이 끝났으나 순서가 stable하지 못하다.



**Heap Sort**

min heap을 기준으로, data을 삽입할 때에 1 2 3 2 순서로 진행하면, 1 2(1) 3 2(2) 가 된다.

최소값을 pop 할 경우, 맨 뒤의 원소가 root로 올라가고 재정렬을 진행한다.

`2(2) 2(1)` 3

크기를 만족하여 정렬이 끝났으나 unstable 상태가 된다.



**Selection Sort**

5(1) 4 5(2) 2 3

2 4 `5(2) 5(1)` 3  => unstable

<br/><br/>