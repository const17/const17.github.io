---
layout : post
title : 함수 - int와 void의 차이
---

지난 글에서 **정수 2개 중 작은 정수를 출력**할 때, `void`형 함수 `printSmaller`를 사용하였는데요,

사실 `void`형이 아닌 `int`형 함수를 사용해도 동일한 기능을 하는 소스 코드를 작성할 수 있습니다.

```c
#include <stdio.h>

int printSmaller(int a, int b){
  if(a<b)
    return a;
  else
    return b;
}

int main(){  
  printf("%d\n",printSmaller(2,3));

  return 0;
}
```
```c
출력 결과
2
```

함수의 조건문에서 `printf`대신 `return`을 사용하는 것과,

`main` 함수에서 `printSmaller()`를 직접 호출하는 대신 `printf`를 사용하여 함수의 값을 출력한다는 것에서 차이를 보이는데요,

이는 `int`와 `void`의 **반환형의 차이** 때문입니다.

이름에서도 알 수 있듯이 `int`는 **int(Integer, 정수)형의 값을 반환(`return`)**해주는 반면, `void`는 **어떠한 값도 반환하지 않습니다**(void의 사전적 의미는 '빈, 공허한').

그렇기 때문에 `void`형 함수에서는 **값을 비교해 둘 중 작은 값을 바로 출력**해주고,

`int`형 함수에서는 **값을 비교해 둘 중 작은 값을 반환하여 main함수에서 출력** 해주는 것입니다.

물론 다음과 같이 `int`형 함수에서도 값을 직접 출력하는 것이 가능합니다.

```c
int printSmaller(int a, int b){
  if(a<b)
   printf("%d\n",a);
  else
   printf("%d\n",b);
  
  return 0;
}

int main(){
  printSmaller(2,3);
  
  return 0;
}
```
```c
출력 결과
2
```
하지만 이런 방식은 **함수의 반환형(`int`)의 특징을 살리지 못하기에 지양**되고 있습니다.
