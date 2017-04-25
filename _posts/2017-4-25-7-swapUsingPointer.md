---
layout : post
title : 포인터와 함수를 이용해 두 수 바꾸기
comment : true
---

이번 글에서는 강의 시간에 배운 `swap` 함수를 다루고자 합니다.

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

하지만 출력 결과에서 볼 수 있듯이 두 변수의 값은 변하지 않습니다.

이유는 강의 시간에 배운 **매개변수의 전달과 존재기간**에서 찾을 수 있는데요, 이는 다음과 같았습니다.

![매개변수의 전달과 존재기간](./images/swapUsingPointer.png)







```c
#include <stdio.h>

void swap(int *ptr1, int*ptr2){
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



