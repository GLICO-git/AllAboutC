# 고급 프로그래밍
## 목차
1. [메모리배치](#메모리-배치)
1. [대형 프로그램 구성](#대형-프로그램-구성)
    - [컴파일](#컴파일)
1. [사용자 헤더파일](#사용자-헤더파일)
1. [외부 변수](#외부-변수)
    - [정적 외부 변수](#정적-외부-변수)
1. [추상 자료형](#추상-자료형)
    - [스택](#스택)
        - [연산자](#연산자)
1. [가변 인자 함수](#가변-인자-함수)
1. [자기 참조 구조체](#자기-참조-구조체)
1. [동적 메모리 할당과 자기참조 구조체](#동적-메모리-할당과-자기참조-구조체)
    - [가비지](#가비지)
    - [주의사항](#주의사항)
1. [플렉시블 배열 멤버](#플렉시블-배열-멤버)

***
## 메모리 배치
![메모리배치](/img/Chapter10/Chapter10_%EB%A9%94%EB%AA%A8%EB%A6%AC%EB%B0%B0%EC%B9%98.png)

- 스택 : 함수의 지역변수, 매개변수, 리턴 주소 저장 <br>
- 힙 : malloc(), calloc()에 의해 할당되는 공간 <br>
- BSS : 초기화 되지 않은 전역변수, 정적변수 저장, 0으로 초기화 된 변수<br>
- 데이터 : 초기화 된 전역변수, 정적변수 저장<br>
- 텍스트 : 실행 코드(문장) 저장
***
## 대형 프로그램 구성
- 프로그램은 여러 파일로 작성될 수 있음
- 관련 함수들은 하나의 파일에 저장
- 한 프로그램을 이루는 파일들은 보통 같은 디렉터리에 저장됨
***
### 컴파일
- 프로그램을 이루는 모든 파일 명시<br>
`$gcc -o grade main.c grade.c`<br>
// main.c와 grade.c를 grade라는 이름의 실행파일로 컴파일 함

- 파일 별 컴파일<br>
```bash
$gcc -c main.c      // -c 옵션을 통해 main.o 파일 생성
$gcc -c grade.c
$gcc -o grade main.o grade.o

// 프로그램 수정 시 수정 된 파일만 재컴파일 후 합친다
$vi main.c      // 파일 수정
$gcc -c main.c
$gcc -o grade main.o grade.o        // 재컴파일
```
***
## 사용자 헤더파일
- 다른 소스파일과 같은 디렉터리에 둠
- 헤더 파일을 여러번 포함해도 되게끔 작성하는 것이 좋음
***
- ex 1)
``` c
#ifndef Header
    #define Header
    ... 
#endif
```
- 전처리기를 사용하여 헤더 파일을 여러번 포함해도 되게끔 작성함

- ex 2)
```c
// grade.h 파일
#ifndef GRADE
    #define GRADE
    #include <stdio.h>
    typedef struct grade{
        int grade[3];
        int sum;
    }grade;

    int grade_proc3(grade *);
#endif
```
- 사용자 헤더 파일(grade.h)을 만들어 main.c 파일과 grade.c 파일에서 중복된 코드를 삭제 할 수 있음
***
## 외부 변수
- 함수 밖에 선언 된 변수
- 모든 함수에서 참조 가능
- 함수 간 정보 전달 유용함
- 다른 파일에 정의 된 외부 변수는 `extern`을 사용하여 참조

\+) 참고 : <br>
```c
int a;          // 변수 선언 : 초기화 X
int b = 7;      // 변수 정의 : 초기화 O
```

- ex)
```c
// 1.c 파일
int a;      // 선언
int main(){
    ...
}

// 2.c 파일
extern int a;
int main(){
    ...
}
```
- `extern`을 활용하여 1.c파일의 a변수를 2.c파일에서도 사용 가능함<br>
- 하지만, 1.c 파일에서 `static int a;`로 선언 시 2.c 파일에서 사용 불가함
***
### 정적 외부 변수
- 외부 변수에 `static`이 적용된 변수
- 정적 외부 변수는 그 변수가 선언된 파일 내에 있는 함수에서만 사용가능 <br>
-> 데이터 접근을 제한하여 안전한 프로그램 만들 수 있음
***
## 추상 자료형
- 처리해야 할 데이터 집합과 그 연산을 정의한 명세
***
### 스택
- 데이터를 선형으로 저장하는 자료구조로써, 후입선출의 구조를 가짐
- a, b, c 순으로 들어와서 c, b, a 순으로 나간다
- 함수 호출에 의해 생성되는 함수 프레임은 메모리의 스택 부분에 저장됨
***
#### 연산자
- push : 스택에 데이터 삽입<br>
- pop : 스택으로부터 데이터 삭제 <br>
- top : 스택 제일 위의 데이터 확인<br>
- empty : 스택이 비었는지 검사 <br>
- full : 스택이 가득 차있는지 검사 <br>
- reset : 스택 초기화 <br>
***
- ex)
```c
#include <stdio.h>

#define MAX_LEN 100
#define FULL (MAX_LEN -1)


typedef struct stack{
    char s[MAX_LEN];
    int top;
}stack;

void push(char c, stack *stk){
    skt -> top++;
    stk -> s[stk -> top] = c;
}

void reset(stack *stk){
    stk -> top = -1;
}

char pop(stack *skt){
    return stk -> s[top--];
}

char top(const stack *stk){
    return (stk -> s[stk -> pop]);
}

bool full (const stack* skt){
    return (stk -> top == FULL);
}

int main(){
    ...
}
```
***
## 가변 인자 함수
- 함수의 매개변수의 개수가 정해져 있지 않은 함수
- 매개변수에서 `...`(점 3개)로 표시
- `<stdarg.h>`에 정의된 매크로 사용
- 종류 : <br>
`va_start(ap, v)`   : ap가 가변인자의 첫 인자 포인트, v가 가변인자 바로 직전의 인자<br>
`va_arg(ap, type)`  : ap가 포인트하는 곳의 값을 type형으로 읽고, ap는 다음 인자를 포인트<br>
`va_copy(dest, src)`    : src 포인터를 dest로 복사<br>
`va_end(ap)`    : va_start()로 초기화 된 ap 포인터 제거
***
- ex)
```c
#include <stdio.h>

#define END 0
#define INT 1
#define DOUBLE 2

double va_sum(int, ...);

int main(){
    sum = va_sum(INT, 3, DOUBLE, 3.0, END);
}

double va_sum(int type, ...){
    double sum = 0.0;
    va_list ap;     // 가변 인자 선언
    va_start(ap, type);

    while(type != 0){
        if(type == INT)
            sum += va_arg(ap, int);
        else
            sum += va_arg(ap, double);
        type = va_arg(ap, int);
    }

    va_end(ap);
    return sum;
}
```
***
## 자기 참조 구조체
- 자신과 같은 구조체 형을 포인트하는 멤버를 갖는 구조체
***
- ex)
```c
struct list{
    int data;
    struct list * next;
}

int main(){
    struct list a = {1, NULL}, b = {2, NULL}, c = {3, NULL};    // 그림 1 참조

    a.next = &b;
    b.next = &c;
    c.next = &a;            // 그림 2 참조
     printf("a: %d, b: %d, c: %d\n", a.data, b.data, c.data);
     printf("a: %d, b(a.next -> data): %d, c(b.next -> data): %d\n", a.data, a.next->data, b.next->data);
}
```
- 실행 결과 : <br>
``` bash
a: 1, b: 2, c: 3
a: 1, b(a.next -> data): 2, c(b.next -> data): 3
```

- 그림 1
![그림1](/img/Chapter10/Chapter10_%EA%B7%B8%EB%A6%BC1.png)

- 그림 2
![그림2](/img/Chapter10/Chapter10_%EA%B7%B8%EB%A6%BC2.png)
***

## 동적 메모리 할당과 자기참조 구조체
- 자기 참조 구조체는 동적 메모리 할당 기법과 함께 사용 됨
- 동적으로 할당받은 구조체는 기족 구조체가 포인트하여 유지함
***
- ex)
```c
tmp = (struct *list)malloc(sizeof(struct list));
tmp -> data = 4;
tmp -> next = NULL;
```
***
### 가비지
- 동적으로 할당 받은 메모리 공간은 어느 방법으로든 접근 할 수 있게 만들어야 함
- 가비지 : 접근할 수 없는 동적으로 할당 받은 메모리 공간
- 가비지가 발생하지 않게 하기 위해서는 이전 포인터를 잘 관리해야 함
***
- ex)
``` c
struct* list tmp;
tmp = (strcut* list)malloc(sizeof(struct list));
tmp -> data = 10;
tmp -> next = NULL;         // 가비지 발생 (data가 4인 구조체로 접근 불가, 그림 1 참조)

// sol, 그림 2 참조
tmp -> next = (struct* list)malloc(sizeof(struct list));
tmp -> next -> data = 10;
tmp -> next -> next = NULL;
```
- 그림 1)
![가비지1](/img/Chapter10/Chapter10_%EA%B0%80%EB%B9%84%EC%A7%801.png)
- 그림 2)
![가비지2](/img/Chapter10/Chapter10_%EA%B0%80%EB%B9%84%EC%A7%802.png)
***
### 주의사항
- 포인터를 다룰 시에는 함수를 만들어서 할 것
- `InitNode()`, `InsertNode()`, `DeleteNode()`
- 포인터 선언 시 초기화<br>
`int *p = NULL;`
- `malloc()`, `calloc()`사용 시 `free()`함수 사용
- `free()` 사용 후 `NULL`로 초기화
```c
free(p);
p = NULL;
```
***
## 플렉시블 배열 멤버
- 동적 할당 자기참조 구조체의 대안으로 사용할 만 함
- 두 개 이상의 멤버를 갖는 구조체형 정의에서 크기가 명시되어 있지 않은 마지막 배열 멤버를 뜻 함
 ***
 - ex)
 ```c
 srtuct subject{
     int num;
     int grade[];       // 플렉시블 배열 멤버
 };
```
- 이 구조체의 크기는 플렉시블 배열 멤버를 제외한 크기임

- 사용 전에 메모리 할당을 받아야 함
```c
struct subject science;
science.num = 10;           // OK
science.garde[0] = 95;      // 오류!!

// sol
struct subject *science_p;
science_p = (struct subject *)malloc(sizeof(struct subject) + sizeof(int)* 10);
// grade[]를 위해 40bytes할당 -> int형(4bytes) 원소 10개

science -> num = 20;        // OK
science -> grade[4] = 85;   // OK