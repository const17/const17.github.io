---
layout : post
title : 포인터와 함수를 이용해 두 수 바꾸기
comment : true
---

이번 글에서는 강의 시간에 배운 `swap` 함수를 다루고자 합니다.

포인터를 배우기 전에 우리가 생각할 수 있는 소스 코드는 다음과 같았습니다.

```c
#include <stdio.h>

void swap(int x, int y){
  int temp=0;
  
  temp=x;
  x=y;
  y=temp;
}

int main(){
  int x=10, y=20;
  
  printf("Original x:%d, y:%d\n",x,y);
  
  swap(x,y);
  
  printf("Changed x:%d, y:%d\n",x,y);
  
  return 0;
}
```

```c
출력 결과
Original x:10, y:20
Changed x:10, y:20
```



```c
#include <stdio.h>

void swap(int *px, int*py){
  int temp=0;
  
  temp=*px;
  *px=*py;
  *py=temp;
}

int main(){
  int x=10, y=20;
  
  printf("Original x:%d, y:%d\n",x,y);
  
  swap(&x,&y);
  
  printf("Changed x:%d, y:%d\n",x,y);
  
  return 0;
}

```

```c
출력 결과
Original x:10, y:20
Changed x:20, y:10
```

우선 `swap` 함수에서 사용한 알고리즘이 이해가 되지 않으시는 분은 [이전 글](https://const17.github.io/5-swap/)을 참고하시면 될 것 같습니다.

