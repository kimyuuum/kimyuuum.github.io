---
layout:	post
title:	"c++ STL - Deque"
date:	2020-05-04 22:25:00
category: [ computer science ]
---





## C++ STL - Deque

<br/>

vector의 단점을 보완하기 위해 만들어진 컨테이너. deque도 vector와 마찬가지로, 배열 기반의 자료구조이다.

<br/>

vector는 새로운 원소가 추가될 경우

<br/>

1. 메모리 재할당
2. 이전 원소 복사

를 진행하므로 삽입시에 성능이 저하한다.

<br/>

<br/>

Deque는 메모리가 부족할때마다 일정 크기의 새 메모리 블록을 할당한다. (이전원소를 복사하는 방식이 아님)

⇒ 여러개의 일정 크기 메모리블록을 할당하고, 하나의 블록처럼 여기는 것이다.

```cpp
d.at(idx); // idx번째 원소를 참조한다. == d[idx]
d.front();
d.push_front(idx);
d.pop_front();
d.push_back(idx);
d.pop_back();
d.clear();
```

deque는 중간 삽입도 가능하다.

`d.insert(1,2,3)` → 1번째 idx에, 2개의 '3'을 insert.

`d.insert(1,2)` → 1번째 idx에 2를 삽입한다.

`d.erase(iter)` → iter가 가리키는 원소를 제거한다.

<br/>

<br/>