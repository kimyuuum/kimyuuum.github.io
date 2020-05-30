---
layout:	post
title:	"Sort - Insertion Sort"
date:	2020-05-30 23:34:00
category: [computerscience]
---



## [Sort] Insertion Sort

<br/>

<br/>

**이미 정렬되어있는 배열에 원소를 추가할 경우, 제 자리를 탐색하여 해당 자리에 삽입하여 정렬된 상태를 유지시키며 크기를 늘리는 정렬**



Selection/Bubble Sort가 N개부터 크기를 줄여나가며 정렬을 하는것과는 반대로 Insertion Sort는 1부터 크기를 하나씩 늘린다.



+ 배열이 정렬되어있는 상태라면, while이 한번도 수행되지 않아서 for문은 상수시간이 소요된다. 

+ for문은 n-1번 순환하므로 O(n)

  

### Time Complexity 

+ O(N^2) / 최선의 경우 O(N)

### Space Complexity

+ O(N)

`stable sort`이다.



### FLOW

1. 2번째 idx부터 시작한다. 
2. 그 앞의 원소들과 비교해서, 삽입 위치를 지정하고 자료를 뒤로 밀어낸 뒤에 삽입한다.

<br/>

---------------------

<br/>

<br/>

``` c++

  for(int i=1; i<n; i++){
    int j = i-1;
    while(j >= 0 && arr[j] > arr[j+1]){
      swap(arr[j],arr[j+1]);
      j--;
    }
  }

```



<br/>

<br/>



