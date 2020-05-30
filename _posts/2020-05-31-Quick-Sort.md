---
layout:	post
title:	"Sort - Quick Sort"
date:	2020-05-31 00:15:00
category: [computerscience]


---



## [Sort] Quick Sort

<br/>

<br/>

**평균 성능이 좋아 가장 빈번하게 쓰이는 정렬이다.**



#### Time Complexity 

+ 평균 O(nlogn) | 최악 O(N^2) ( 이미 정렬되어있거나, 역순인 경우)

#### Space Complexity

+ O(logn)

`unstable sort`이다.

<br/>

#### FLOW

1. 배열의 가장 왼쪽 또는 오른쪽을 pivot값으로 설정한다.

2. pivot보다 작은 원소는 왼쪽, 큰 원소는 오른쪽에 배치한다.

3. pivot을 제외하고 나눠진 값에 대하여 다시 재귀적으로 pivot을 설정하여 반복한다.

   => 부분 list들이 더이상 분할 불가할때까지 반복한다. (size == 0 or 1)

<br/>

+ 전체 list를 2개로 분할한다 => 각각의 부분 list에 대하여 다시 quick sort를 진행한다.
+ quick sort는 merge sort와는 다르게 리스트를 비균등하게 분할한다.

<br/>

---------------------

<br/>



#### 분할정복

: 문제를 작은 2개의 문제로 분리하고, 각각을 해결한 다음 결과를 모아서 원래의 문제를 해결한다. 



``` c++

  int partition(int left,int right){

    int pivot = arr[left];
    int low = left+1;
    int high = right;

    while(low < high){
      while(low <= right && arr[low] <= pivot){
        low++;
      }
      while(high > left && arr[high] > pivot){
        high--;
      }

      if(low > high){
        swap(arr[high],arr[left]);
      }else{
        swap(arr[low],arr[high]);
      }
    }

    return high;
  }

  int quicksort(int left,int right){
    if(left < right){
      int q = partition(left,right);
      quicksort(left,q-1);
      quicksort(q+1,right);
    }
  }

```



<br/>

#### Quick Sort 개선

1. Random 분할

   > pivot을 0~n-1범위의 난수로 선택한다. 난수의 위치가 배열 제일 오른쪽 원소와 위치를 바꾸고, quick sort를 실행한다.

   

2. 삽입 정렬 활용하기

   > 삽입 정렬은 크기가 작은 배열에서 효율이 매우 좋다. 
   >
   > 추가적인 메모리를 필요로 하지도 않는다.
   >
   > 작은 구간에서 활용하고, 재귀의 깊이를 줄인다.

   

3. 세 값의 중위

   > 1. 가장 왼쪽
   > 2. 가장 오른쪽
   > 3. 중간값
   >
   > => 세 값을 정렬하고, 가장 작은 값을 왼쪽에, 큰 값을 맨 오른쪽에 배치한다. 그리고 arr[right-1]에 중간값을 배치한다.
   >
   > 정렬 구간을 arr[left + 1] ~ arr[right-2] 로 줄일 수 있다.

   `재귀의 깊이도 줄일 수 있고, 분할도 대부분 중앙에서 이뤄진다.`

<br/><br/>