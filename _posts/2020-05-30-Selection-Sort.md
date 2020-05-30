---
layout:	post
title:	"Sort - Selection Sort"
date:	2020-05-30 23:15:00
category: [computerscience]

---



## [Sort] Selection Sort

<br/>

<br/>

**해당 원소에 원소를 넣을 위치는 이미 정해져 있고, 어떤 원소를 넣을지 선택하는 정렬**

#### Time Complexity 

+ O(N^2)

#### Space Complexity

+ O(N)

<br/>

#### FLOW

1. 주어진 원소 중에서 가장 작은 원소를 찾는다.
2. 그 값을 맨 앞에 위치한 원소와 교체한다.
3. 맨 처음 위치를 제외한 나머지 리스트에 대하여 반복한다.

<br/>

---------------------

<br/>

``` c++
  
  for(int i=0; i<n-1; i++){ //한개가 남을때까지 반복한다.
      int target = i;
      for(int j=i+1; j<n; j++){
        if(arr[target] > arr[j]){
          target = j;
        }
      }
      swap(arr[target],arr[i]);
    }

```



자료 이동횟수는 미리 결정된다.

unstable한 정렬이다.

5(1) 4 5(2) 2 3

=> 2 4 5(2) 5(1) 3

첫번째 5가 정렬 후 뒤로 가기 때문에, `값이 같은 레코드가 있는 경우` 상대적 위치가 변경될 수도 있으므로 unstable한 정렬이다.

<br/>

<br/>


