# 전처리기
## 목차
  - [전처리기](#전처리기-1)
  - [매크로](#매크로)
    - [기호 상수 매크로](#기호-상수-매크로)
    - [문자열 대치 매크로](#문자열-대치-매크로)
    - [매개변수를 갖는 매크로](#매개변수를-갖는-매크로)
    - [유의사항](#유의사항)
  - [#연산자](#연산자)
  - [헤더파일](#헤더파일)
    - [#include](#include)
  - [조건부 컴파일](#조건부-컴파일)
    - [#undef](#undef)
    - [#ifdef, #ifndef](#ifdef-ifndef)
    - [#else](#else)
    - [#if, #elif, #else, #endif](#if-elif-else-endif)
  - [defined](#defined)
***
## 전처리기
- #으로 시작하는 행을 전처리 지시자라고 함
- 전처리 구문은 C언어의 나머지 부분과 **독립적임**
- 전처리기는 C를 알지 못 함
***
## 매크로
- 종류 :
    - 기호 상수 매크로
    - 문자열 대치 매크로
    - 인자가 있는 매크로
- cf) 매크로 선언은 무조건 한 줄로 작성해야 함<br>
  정의가 길어질 경우, `\`를 삽입하면 연결이 가능
***
### 기호 상수 매크로
- 형태 : <br>#define 식별자 상수
- 프로그램의 모든 식별자는 상수로 대치 됨

---
- ex)
```C
#define PI 3.14
```
---
### 문자열 대치 매크로
- 형태 : <br>#define 식별자 문자열
- 프로그램의 모든 식별자는 문자열로 대치 됨
  
---
- ex1)
  ```C
  #define EQ ==

  int main(){
      ...
      if(sum EQ 100)        // if(sum == 100)
      ...
  }
  ```

- ex2)
  ```C
  #define AND &&
  #define OR ||
  ...
  ```

### 매개변수를 갖는 매크로
- 형태 : <br>#define 식별자(매개변수) (수식 등)
- 전처리기는 매개변수를 실인자로 대치함
---
- ex)
```c
#define  CIRCUMFERENCE(x) (2.0*(x)*PI)
...
int main(){
    ...
    printf("원의 둘레 : %.3f\n", CIRCUMFERENCE(r));
    // printf(" ", (2.0*(r)*PI));
}
```
---
- inline 함수와 비슷하지만 차이가 있음
- 매크로는 인자의 형을 검사하지 않음

- ex)
```c
#define AREA(x) ((x)*(x)*PI)
// x에 대응되는 인자형 고려 안함
// int든 float이든 상관없음
// but, inline 함수를 사용하면 적절히 형변환됨
```
---
- 매크로는 인자들을 여러번 평가함
- ex)
```c
#define PI 3
#define AREA(x) ((x)*(x)*PI)

...생략
int r = 2;
AREA(r++);      // ((r++)*(r++)*3) -> 2 * 3 * 3
AREA(r++);      // ((r++)*(r++)*3) -> 4 * 5 * 3

r = 2;
AREA(++r);      // ((++r)*(++r)*3) -> 4 * 4 * 3
AREA(++r);      // ((++r)*(++r)*3) -> 6 * 6 * 3
...생략
```

- cf) 전위 연산자(++r)하면 r값 모두 계산 후, 대입 됨
<br>인자(++r)가 2번 사용되므로 ++r도 2번 계산하여 4가 대입 됨

---

### 유의사항
1. 매크로는 괄호를 충분히 써서 올바른 평가순서를 유지해야 함
***
- case 1)
```c
#define AREA(x) ((x)*(x)*PI)
: AREA(a+b)      // ((a+b)*(a+b)*PI)
```
- case 2)

```c
#define AREA(x) x*x*PI
: AREA(a+b)      // a+b*a+b*PI
```
- case 3)
```c
#define AREA(x) (x)*(x)*PI
: 4/AREA(2)      // 4/(2)*(2)*PI    !=     4/((2)*(2)*PI)
```
***
2. 매크로 이름과 매개변수 사이에 공백 X
***
- ex)
```c
#define AREA (x) ((x)*(x)*PI)
: AREA(5.0)      // (x) ((x)*(x)*PI)(5.0)
```
-> 문자열 매크로처럼 인식!
***
3. 세미콜론 사용에 유의
***
- ex)
```c
#define AREA(x) ((x)*(x)*PI);

: if(r>0)
    x = AREA(r);        // x = ((r)*(r)*PI);;
  else
    x = -1;
```
***
## #연산자
- "문자열 화" 연산자
- 형태 : <br>
  #define 식별자 #문자열
- ex)
```c
#define STRING(a) #a

: STRING(쥬라기공원1)       // "쥬라기공원1"
```
- 디버깅을 위해 #연산자를 이용함
- ex)
```c
#define PRINT_VAR(x) printf(#x " = %d\n", x)
...
int i = 70;

PRINT_VAR(i);       // 출력결과 : i = 70
```
## 헤더파일
1. *.h 파일
   - #include, 매크로 정의, 함수 원형, 기호 상수 등 정의
2. 시스템이 제공하는 헤더 파일(표준 헤더 파일)
    - stdio.h, stdlib.h, string.h 등
3. 사용자도 자신의 헤더 파일을 만들 수 있음
    - 소스파일과 같은 디렉터리에 생성함
    - #include로 프로그램에 삽입함
___
### #include
- 명시 방법 : <br>#include <stdio.h> 또는 #include "stdio.h"

- **#include <stdio.h>**
  - 표준헤더파일 삽입 시 사용
  - 시스템이 정의한 디렉터리에서 파일을 찾아 삽입
  - 일반적으로, 표준헤더파일이 저장된 장소는 시스템에 따라 다름

- **#include "filename.h"**
  - 사용자헤더 파일 삽입시 사용
  - 먼저, 현재 디렉터리에서 검색하고, 없다면 시스템이 정의한 디렉터리에서 검색하여 삽입

## 조건부 컴파일
- 관련 전처리 지시자 : <br> #if, #ifdef, #else, #elif, #endif, #undef
### #undef
- 앞에서 정의한 매크로를 무효화 함
- 매크로 재정의시 사용
***
- ex)

```c
#undef PI       // 이 문장 이후로는 PI 매크로 사용 불가
```
***
### #ifdef, #ifndef
- 뒤에 식별자(매크로 이름) 옴
- 뒤에 오는 식별자가 #define에 의해 정의되어 있는지 겁사
- 조건이 참이면 #endif 사이의 문장이 적용, 거짓이면 무시
***
- ex1)
```c
#ifdef A        // A가 정의되어 있다면 사이의 문장이 수행됨
    corona is fuck
#endif
```

- ex2)
```c
#ifdef PI
    #undef PI
#endif PI
#define Pi 3.141592     // PI가 정의되어 있던 없던 간에 PI를 3.141592로 정의함
```
- 그냥 #define을 2번하면 전처리기에 의해 오류가 발생함
- cf) <br>#ifdef, #ifndef는 #endif로 끝나므로 들여쓰기 하여 가독성을 높인다
- ***
### #else
- #ifdef, #ifndef가 거짓일 때 선택 됨
***
- ex)
```c
#ifdef PI
        area = r * r * PI;
    #else
        area = r * r * 3.14;
#endif

//또는

#ifndef PI
        area = r * r * 3.14;
    #else
        area = r * r * PI;
#endif
```
- PI가 선언되어 있지 않으면 3.14를 곱함
***
### #if, #elif, #else, #endif
- ex)
```c
#if N < 10
        int num[100];
    #elif N > 2000;
        int num[2000];
    #else
        int num[N];
#endif
```
- N값에 따라 num  배열의 크기 조정
## defined
- defined 뒤에 명시된 식별자가 정의되어 있는지 확인
- 정의되어 있으면 1, 아니면 0의 값을 가짐
***
- +) #if와 같이 사용하면 #ifdef와 같은 결과를 얻음
  <br> WHY -> #ifdef를 사용하면 되지 왜 #if defined를 사용할까?<br>
<br> #ifdef 뒤에는 수식이 올 수 없으므로
`#if defined(PI) && defined(PI2)`와 같이
`&&`이라는 수식을 위해 사용된다

***
- ex)
```c
#if defined(PI)
    #undef PI
#endif
```
***
- +) gcc 인 경우 명령어 라인에서 -D 옵션을 주어 사용가능함.
- ex)
``` shell
$ gcc -D DEBUG test.c
$ gcc -D DEBUG=1 test.c
```
- 이 명령어는 test.c파일 첫 행에
```c
#define DEBUG
#define DEBUG 1
```
두 문장이 있는 것과 같음
