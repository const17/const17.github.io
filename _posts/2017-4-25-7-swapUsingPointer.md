---
layout : post
title : 포인터와 함수를 이용해 두 수의 값 바꾸기
comment : true
---

이번 글에서는 강의 시간에 배운 `swap` 함수(두 수의 값을 바꾸는 함수)를 다루고자 합니다.

포인터를 배우기 전에 우리가 생각할 수 있는 소스 코드는 다음과 같았습니다.

```c
#include <stdio.h>

void swap(int n1, int n2){
  int temp=0;
  
  temp=n1;
  n1=n2;
  n2=temp;
}

int main(){
  int num1=10, num2=20;
  
  printf("Original num1:%d, num2:%d\n",num1,num2);
  
  swap(num1,num2);
  
  printf("Changed num1:%d, num2:%d\n",num1,num2);
  
  return 0;
}
```

```c
출력 결과
Original num1:10, num2:20
Changed num1:10, num2:20
```
우선 `swap` 함수에서 사용한 알고리즘이 이해가 되지 않으시는 분은 [이전 글](https://const17.github.io/5-swap/)을 참고하시면 될 것 같습니다.

출력 결과에서 볼 수 있듯이 두 변수의 값은 변하지 않습니다.

이유는 강의 시간에 배운 **매개변수의 전달과 존재기간**에서 찾을 수 있는데요, 이는 다음과 같았습니다.

![매개변수의 전달과 존재기간](/./images/swapUsingPointer.png)

함수 내에서의 흐름은 다음과 같은데요,

![잘못된 swap](/./images/swapUsingPointer2.png)

*이미지 출처 : 열혈 C 프로그래밍, 윤성우 저*

`main` 함수에서 `num1`과 `num2`의 **값**을 `swap` 함수의 매개변수로 넘겨줍니다.

이 때 **매개변수를 위해 새로운 메모리 영역이 생성**되고 **이 메모리 영역 내에서의 값(`n1`과 `n2`)이 변하**기 때문에 `main`함수 내의 `num1`과 `num2`에는 **아무런 영향을 미치지 못하는 것**입니다.

이렇게 함수를 호출할 때 단순히 **값을 전달**하는 함수호출을 가리켜 **Call-by-value**라고 합니다.

Call-by-value 방식으로는 **함수**(여기선 `swap`) **외부에서 선언된 변수**(여기선 `main`함수의 `num1`과 `num2`)에 **접근이 불가**합니다.

`swap` 함수를 포인터를 이용하여 수정한다면 소스 코드는 다음과 같습니다.

```c
#include <stdio.h>

void swap(int* ptr1, int* ptr2){
  int temp=0;
  
  temp=*ptr1;
  *ptr1=*ptr2;
  *ptr2=temp;
}

int main(){
  int num1=10, num2=20;
  
  printf("Original num1:%d, num2:%d\n",num1,num2);
  
  swap(&num1,&num2);
  
  printf("Changed num1:%d, num2:%d\n",num1,num2);
  
  return 0;
}

```

```c
출력 결과
Original num1:10, num2:20
Changed num1:20, num2:10
```

출력 결과에서 볼 수 있듯이 이번엔 두 정수의 값이 바뀐 것을 알 수 있습니다.

`main` 함수에서 `num1`과 `num2`의 **값**이 아닌 `num1`과 `num2`의 **주소**를 매개변수로 넘겨주고 있으므로 `swap` 함수에서는 `main`함수의 `num1`과 `num2`에 접근이 가능합니다.

풀어서 말하면 `swap`함수 내의 `*ptr1`은 **포인터 변수 ptr1이 가리키는 메모리 공간인 변수 num1에 저장된 값**, 즉 10을 의미하고 같은 원리로 `*ptr2`는 `num2`의 값인 20을 의미합니다.

함수 내에서의 흐름은 다음과 같습니다.

![CallByReference](/./images/swapUsingPointer3.png)

*이미지 출처 : 열혈 C 프로그래밍, 윤성우 저*

결과적으로 `main` 함수의 `num1`과 `num2`의 값이 서로 바뀌게 됩니다.

이와 같이 **메모리의 접근에 사용되는 주소 값을 전달**하여 **외부에서 선언된 변수에 접근이 가능**한 형태의 함수호출을 가리켜 **Call-by-reference**라고 합니다.
