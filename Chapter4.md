# Pointer 
## 목차
1. [포인터 배열](#포인터-배열)<br>
1. [main()함수의 인자](#main()함수의-인자)<br>
1. [형 한정자](#형-한정자)<br>
    - [const](#const)<br>
        - [const 포인트 유의점](#const-변수를-포인트-할-때,-유의점)<br>
        - [상수 포인터](#상수-포인터)<br>
        - [const 변수에 대한 상수 포인터 사용](#const-변수에-대한-상수-포인터-사용)<br>
    - [restrict](#restrict)<br>
1. [포인터 함수](#함수-포인터)<br>

***
## 포인터 배열
- 포인터를 원소로 갖는 배열

cf) 문자형 배열을 사용하면

```C
char words[3][6] = {"cat", "dog","mouse"};
```
|메모리||||||
|:---:|---|---|---|---|---|
|c|a|t|\0|<span style="background-color:red">낭비|<span style="background-color:red">낭비
|d|o|g|\0|<span style="background-color:red">낭비|<span style="background-color:red">낭비
|m|o|u|s|e|\0|

제일 긴 문자에 따라 '열(column)'이 할당 되므로<br>
words[0][4], [0][5], [1][4], [1][5] 부분의 메모리가 낭비되고 있다.
***
Sol> *<u>포인터 배열*</u>을 통해 메모리 낭비를 최소화 한다.

- ex1)
```c
char *words[3];     // 포인터 배열 선언
```
||||||
|:---:|---|---|---|---|
words[0] -----> |c|a|t|\0|

||||||
|:---:|---|---|---|---|
words[1] -----> |d|o|g|\0|

||||||||
|:---:|---|---|---|---|---|---|
words[2] -----> |m|o|u|s|e|\0|

- ex2)
```C
...
int main(){
    char *words_p[N];        // char형 포인터 배열
    input_words(words_p);
    for(int i = 0; i < N; i++)
        free(words_[i]);
}
void input_words(char *words[]){
    char word[11];          // 단어 최대 길이 10 + NULL문자
    input_a_word(word);     // 단어 입력 함수
    words[num] = (char*)calloc(strlen(word)+ 1, sizeof(char));     // 메모리 할당
    strcpy(words[num], word);
}
```
참고
![포인터배열 참고](/img/Chapter4/포인터배열참고.png)
***

## main()함수의 인자
- main() 함수는 프로그램 실행 시 <u>**명령어 라인**</u>으로부터 인자를 전달 받을 수 있음
```C
int main(int argc, char *argv[])
```
- argc : 명령어 라인에서 전달된 인자 개수 (argument Count)
- argv : 명령어 라인에서 입력된 문자열들에 대한 포인터 (argument Value)

- ex)
```c
#include <stdio.h>
int main(int argc, char *argv[]){
    printf("총 인자 개수 : %d\n", argc);
    
    for(int i = 0; i < argc; i++)
        printf("%d번째 인자 : %s\n", i, argv[i]);
}
```

``` shell
$ prog hello main       // 명령어 라인에서 실행
```
실행결과:
```
총 인자 개수 : 3
0번째 인자 : prog
1번째 인자 : hello
2번째 인자 : main
```
***
## 형 한정자
- 변수의 사용 제한 설정
    - const
    - restrict : C99에서 추가됨

### const
- const 변수는 초기화 될 수는 있지만, 그 후에 배정되거나 증가, 감소, 수정 될 수 없음

- ex)
```c
const float pi = 3.14;      // pi에는 다른 값을 배정할 수 없음
pi = 3.141592;              // 에러
```
***
### const 변수를 포인트 할 때, 유의점
```C
const int a = 7;
int *p = &a;    // 경고
```
- p는 int형의 보통의 포인트이기 때문에, ++*p와 같은 수식을 사용하여 a의 값을 변경시킬 수 있기 때문이다.
***
- sol>
```c
const int a = 7;
const int *p = &a;      // p가 가르키는 정수가 const다
```
- p 자체는 상수가 아님
- p에 다른 주소를 배정할 수 있지만,
*p에 값을 배정할 수는 없음.
***
### 상수 포인터
```c
int a;
int *const p = &a      // p가 const, p의 주소값이 변하지 않음
```
- p는 int에 대한 상수 포인터임
- p에 값을 배정할 수는 없지만, *p는 가능함
- 즉, ++*p, *p = 10 등과 같은 수식은 가능함

### const 변수에 대한 상수포인터 사용
```C
const int a = 7;
const int *const p = &a;
```
- p는 const int를 포인트하는 상수 포인터임
- p 와 *p 모두 변경 불가<br>
// p의 주소값과 *p 값 변경 불가
***
### restrict
- 컴파일러가 코드최적화를 진행할 때 사용, 포인터 변수에 적용

- case1)
```
a = b + c;
i = j - a;
k = l / m;
```
- 컴파일 시 세번째 문장이 처음 두 문장보다
먼저/동시 실행되도록 실행코드를 생성할 수 있음

- case2)
```
*a = *b + *c;
*i = *j - *a;
*k = *l / *m;   // a와 k가 가르키는 곳이 같다면?
```
-> 포인터들이 어떤 메모리 공간을 가르키는지 알 수 없으므로 실행코드 최적화 불가

- sol>
```c
restrict int *p, *q; 
```
-> p와q는 같은 곳을 가르키고 있지 않다는 것을 컴파일러에게 알려줌으로써 해결
***
## 함수 포인터
- 하나의 함수를 여러 목적으로 유연하게 사용하고자 할 때 유용함
- 함수명 자체가 함수 포인터
    - 선언 방법
        - 형(*변수명)(매개변수_목록)
         - 형 : 함수 포인터 변수가 가르키는 함수의 리턴형
        - 변수명 : 함수 포인터 명
        - 매개변수_목록 : 함수 포인터 변수가 가르키는 함수의 매개변수 목록
***
- ex 선언 방법)
```c
int (*fp)(int, int);        // 올바른 선언
int *fp (int, int);         // 틀린 선언(함수 원형)
```

- ex1 사용 예시)
```c
#include <stdio.h>

int sum(int, int);

int main(){
    int(*fp)(int, int);
    
    fp = sum;
    int res = fp(10, 20);    // sum(10, 20)
    printf("%d\n", res);
}

int sum(int a, int b){
    return a + b;
}
```

- ex2 사용 예시)
```c
#include <stdio.h>

void func(int(*)(int, int));
int sum(int, int);
int mul(int, int);

int main(){
    func(sum);
    func(mul);
}

void func(int(*fp)(int, int)){
    int a, b, res;
    printf("두 정수 입력 : ");
    scanf("%d %d", &a, &b);
    res = fp(a,b);
    printf("결과 : %d\n", res);
}

int sum (int a, int b){
    return a + b;
}

int mul(int a, int b){
    return a*b;
}
```


