# Pointer
## 목차
1. [포인터란?](#포인터란?)<br>
1. [포인터 변수](#포인터-변수)<br>
    - [주소 연산자 &](#주소-연산자)<br>
    - [역참조 연산자 *](#역참조-연산자)<br>
    - [포인터 변수의 크기](#포인터-변수의-크기)<br>
1. [void형 포인터](#void형-포인터)<br>
1. [포인터 연산](#포인터-연산)<br>
1. [포인터와 함수](#포인터와-함수)<br>
***

## 포인터란? 
- 주소를 다루기 위한 자료형<br>
-> 데이터를 가진 <u>__메모리__</u> 공간을 주소로 접근하기 위해 사용<br>

cf) 메모리는 각 bytes별로 주소가 붙여진 1차원 배열.
- 할당받은 메모리 공간은 변수 이름으로 접근한다.
    - ex) 
    ```C
    int a; // 메모리 할당
    a = 4; // 변수 이름으로 접근
    ```

***
## 포인터 변수
- 값으로 메모리 주소를 갖는 변수
    - ex) 
    ``` C
    int *p; // int형 포인터 변수 p 선언
    int *p, *q; // int형 포인터 변수 p와  int형 포인터 변수 q 선언
    int *p, q; // int형 포인터 변수 p와 int형 변수 q 선언
#### 주소 연산자 &
- 메모리에 할당된 변수의 주소값을 알려주는 연산자.
    - cf) 상수나 수식 앞에서는 & 사용 불가

    ```C
    int i ;
    printf("%u", &i); // i의 주소값 출력
    printf("%u", &3); // 상수 앞에 & 사용 (Warning)
    printf("%u", &(i+3)); // 수식 앞에서 사용 (오류)
    ```
    - 포인터 변수 사용법
    ```C
    int i, *p;  // int i와 포인터 변수 p 선언
    i = 100;
    p = &i;     // 변수 i의 메모리 주소를 p에 할당
    ```

#### 역참조 연산자 *
- 포인터가 가르키는 메모리 공간에 접근하기 위한 연산자
- cf) 단항 연산자, 우에서 좌로의 결합 순위 
    <br>-> 차후 실습문제에서 설명
- ex)
```C
int i = 100, *p;
p = &i;

printf("%d", i);    // 100
printf("%d", *p);   // 100
*p = 200;

printf("%d", i);    // 200
```
#### 포인터 변수의 크기
- System에 따라 상이함
- `Sizeof` 연산자로 계산
- 포인터 변수가 가르키는 형과 관계없이 크기가 동일
    - ex)
    ```C
    int i, *ip;     // Sizeof(i) = 4
    double d, *dp;  // Sizeof(d) = 8
    ip = &i;        // Sizeof(ip) = 8
    dp = &d;        // Sizeof(dp) = 8
    ```

***
## void형 포인터
```C
int *p;
float x;
void *v;
p = &x;     // 오류, 두 형이 다름(int vs float), 포인터는 자동 형 변환 X
v = &x;
p = v;
```
- 사용시 형 변환 필요

```C
int i, j = 20;
void *v;
v = &j;
i = *(int*)v) + 10; // *v를 사용하기 위해 int * 로 캐스팅

```
***
## 포인터 연산
- p, q가 포인터 변수라면...
    - p + i, p - i 는 p가 가르키는 곳에서 i번째 앞, 뒤 원소
    - p - q 는 p와 q 사이의 원소 개수
- ex)
```C
// p가 int형 포인터, 주소 1000, Sizeof(p) = 4
p - 1 = 996
p     = 1000
p + 1 = 1004
p - q = 2       // (p = 1000, q = 992) 
```
- ex2)
```C
double x[10], *p, *q;
p = &x[2];
q = p + 5;
printf("q-p = %d\n", q-p);  // 5 (p와 q사이의 원소의 개수)
printf("(int)q - (int)p = %d\n", (int)q-(int)p); 
// 40 double형 8 바이트 X 5 = 40
```
***
## 포인터와 함수
- C는 "값에 의한 호출" Call by Value 사용
    - 변수가 함수의 인자로 전달될 때, 변수의 <u>**복사본**</u>이 전달됨.
    - 호출한 환경의 변수 자체는 변경되지 않음
- "주소에 의한 호출" Call by Reference로 원본에 접근함 

#### 사용 방법
- 1. 함수 매개변수를 포인터 형으로 선언
- 2. 함수 몸체에서 **역참조 연산자(&)** 사용
- 3. 함수를 호출 할 때, <u>**주소**</u>를 인자로 전달 

- ex) Call by Value
``` C
void Swap(int num1, int num2){
    int temp = num1;
    num1 = num2;
    num2 = temp;
}

int main(void){
    int a = 4;
    int b = 6;
    
    Swap(a, b);     // a = 4, b = 6, 스왑 실행 X
}
```

- ex) Call by Reference
```C
void Swap(int *num1, int *num2){
    int temp = *num1;
    *num1 = *num2;
    *num2 = temp;
}

int main(void){
    int a = 4;
    int b = 6;

    Swap(&a, &b);     // a = 6, b = 4, 스왑 실행 O
}
```