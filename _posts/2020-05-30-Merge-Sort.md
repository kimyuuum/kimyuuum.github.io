---
layout:	post
title:	"Sort - Merge Sort"
date:	2020-05-30 23:50:00
category: [computerscience]

---



## [Sort] Merge Sort

<br/>

<br/>

**입력을 반으로 나누고, 전/후반부를 독립적으로 정렬한다. 이 두개를 merge해서, 정렬 배열을 얻는다.**



#### Time Complexity 

+ O(nlogn)

  > 크기가 8인 배열은 최종적으로 N/8 크기가 8개 생긴다. 
  >
  > 즉, 3번만에 배열의 길이가 1인것을 만들어낸 것인데, 분할 과정은 매번 **절반씩** 감소한다. 그러므로, 밑이 2인 logN만큼 반복한다.
  > 
  >
  > 각 분할별로 merge를 진행하므로, (최대 N)  N * logN = NlogN이 된다.



#### Space Complexity

+ O(nlogn)

`stable sort`이다.

<br/>

#### FLOW

1. base condition - size가 0 또는 1이면 이미 정렬된것으로 본다.
2. 정렬되지 않은 list의 길이를 절반으로 자르고, 비슷한 크기의 두 부분 list로 나눈다.
3. 재귀적으로 merge sort를 실행한다.
4. 두 부분 list를 다시 merge한다.

<br/>

`Divide (분할) => Conquer (정복) => Combine (결합)`

<br/>

+ 추가 list가 필요하다. (임시 배열)
+ 실제로 정렬이 이루어지는 시점은, 두 개의 list가 merge될때이다.

<br/>

---------------------

<br/>

``` c++

  void merge(int left, int mid, int right){
    vector<int> temp;
    int i = left;
    int j = mid+1;
    int cnt = 0;

    while(i <= mid && j <= right){
      if(arr[i] < arr[j]){
        temp.push_back(arr[i]);
        i++;
      }else{
        temp.push_back(arr[j]);
        j++;
      }
    }

    while(i <= mid){
      temp.push_back(arr[i]);
      i++;
    }

    while(j <= right){
      temp.push_back(arr[j]);
      j++;
    }

    for(int idx=left; idx<= right; idx++){
      arr[idx] = temp[cnt++];
    }

  }

  void mergesort(int left,int right){
    if( left < right ){
      int mid = (left + right) / 2;
      mergesort(left,mid);
      mergesort(mid+1,right);
      merge(left,mid,right);
    }
  }

```



<br/>

<br/>



