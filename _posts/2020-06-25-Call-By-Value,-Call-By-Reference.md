---
layout:	post
title:	"Call By Value / Call By Reference"
date:	2020-06-25 11:50:00
category: [computerscience]


---



## [Programming] Call By Value / Call By Reference

<br/>

<br/>

면접에서 단골 질문으로 등장하는 문항이었다. 대충 알고 있다고 생각 했지만, 정확히 코드를 작성하고 설명하는데에 어려움이 있음을 느껴 업데이트 한다. 타인에게 설명하고자 할 때에 대충은 없다는 것을 다시 한번 느꼈다!

<br/>

### Call by value

<br/>

: 값에 의한 호출.

함수가 호출될 때, 메모리 공간 간에서는 함수를 위한 별도의 임시 공간이 생성된다. (종료 시 사라짐)

함수 호출 시 → 전달 되는 변수 값을 복사해서 → 함수 인자로 전달한다.

복사된 인자는 함수 안에서 지역적으로 사용되기 때문에, **local value** 속성을 가진다.  **따라서 함수 안에서 인자 값의 변경이 일어나도, 외부 변수 값은 변경되지 않는다.**

<br/>

```c++
void func(int n){
	n = 20;
}

void main(){
	int n = 10;
	func(n);
	printf("%d",n); // 10
}
```

<br/>

<br/>

### Call by reference

<br/>

: 참조에 의한 호출.

함수 호출 시, 인자로 전달되는 변수의 **레퍼런스를** 전달한다. 함수 안에서 인자의 변경이 일어나면, 전달된 객체의 값도 변경된다. 포인터(주소가) 넘어가서, 같은 메모리를 쓰고 있음을 알 수 있다.

<br/>

```c++
void func(int *n){
	*n = 20;
}

void main(){
	int n = 10;
	func(&n);
	printf("%d",n); // 20
}
```

<br/>

<br/>

### Java의 함수 호출 방식

함수에 전달되는 인자의 data type에 따라 함수 호출 방식이 달라진다.

- Primitive Type (원시 자료형) = call by value

  int, short, long, float, double, char, boolean ...

- Reference Type (참조 자료형) = call by reference

  array, class instance

String은 참조 자료형이지만, Java에서는 원시 자료형처럼 적용된다.

<br/>

### 정리

call by value의 경우, data의 값을 복사해서 함수로 전달하기 때문에 원본의 데이터가 변경될 가능성이 없다. 하지만 `인자를 넘겨줄 때 마다 메모리 공간을 할당`해야 해서 공간 낭비가 더 크다.

<br/><br/>