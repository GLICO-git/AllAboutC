# AllAboutC
__C 언어 정리__<br>
C언어 기초는 **제외**함<br>
포인터 부분부터 정리해서 올림

## 목차
<details><summary>
Chapter1 : Markdown 사용법
</summary><div markdown="1">

- 제목
- 강조
- 리스트
- 링크
- 이미지
- 줄바꿈
- 코드 강조
- 표
- 인용문
</div></details>
<details><summary>
Chapter2 : Pointer 1차시
</summary><div markdown="1">

1. [포인터란?](#포인터란?)<br>
1. [포인터 변수](#포인터-변수)<br>
    - [주소 연산자 &](#주소-연산자-&)<br>
    - [역참조 연산자 *](#역참조-연산자-*)<br>
    - [포인터 변수의 크기](#포인터-변수의-크기)<br>
1. [void형 포인터](#void형-포인터)<br>
1. [포인터 연산](#포인터-연산)<br>
1. [포인터와 함수](#포인터와-함수)<br>
</div></details>
<details><summary>
Chapter3 : Pointer 2차시
</summary><div markdown="1">

1. [포인터와 배열](#포인터와-배열)<br>
1. [배열을 매개변수로 갖는 함수](#배열을-매개변수로-갖는-함수)<br>
1. [문자열 포인터와 문자 배열의 차이점](#문자열-포인터와-문자-배열의-차이점)<br>
1. [동적 메모리 할당](#동적-메모리-할당)<br>
</div></details>
<details><summary>
Chapter4 : Pointer 3차시
</summary><div markdown="1">

1. [포인터 배열](#포인터-배열)<br>
1. [main()함수의 인자](#main()함수의-인자)<br>
1. [형 한정자](#Chapter4/형-한정자)<br>
    - [const](#const)<br>
        - [const 포인트 유의점](#const-변수를-포인트-할-때,-유의점)<br>
        - [상수 포인터](#상수-포인터)<br>
        - [const 변수에 대한 상수 포인터 사용](#const-변수에-대한-상수-포인터-사용)<br>
    - [restrict](#restrict)<br>
1. [포인터 함수](#함수-포인터)<br>
</div></details>
<details><summary>
Chapter5 : 사용자 정의형 - 구조체
</summary><div markdown="1">

1. [구조체](#구조체)<br>
    - [구조체 태그가 없는 경우](#구조체-태그가-없는-경우)<br>
    - [typedef](#typedef)<br>
    - [구조체 초기화](#구조체-초기화)<br>
    - [복합 리터럴](#복합-리터럴)<br>
    - [구조체의 구조체](#구조체의-구조체)<br>
    - [구조체 포인터](#구조체-포인터)
    - [멤버 접근 연산자](#멤버-접근-연산자)<br>
    - [구조체와 함수](#구조체와-함수)
    </div></details>
    <details><summary>
    Chapter6 : 사용자 정의형 - 공용체, 열거형
    </summary><div markdown="1">

    1. [공용체](#공용체)
        - [공용체 선언](#공용체-선언)
        - [공용체의 크기](#공용체의-크기)
        - [공용체의 사용](#공용체의-사용)
    1. [열거형](#열거형)
        - [열거형 선언](#열거형-선언)
            - [열거형 변수 선언](#열거형-변수-선언)
        - [열거형의 사용](#열거형의-사용)
</div></details>
<details><summary>
Chapter7 : 비트 수준 접근
</summary><div markdonw="1">

- [비트 수준 접근이란?](#비트-수준-접근이란?)
  - [비트 단위 연산자](#비트-단위-연산자)
    - [논리 연산자](#논리-연산자)
      - [~ 연산자](#-연산자)
      - [&, ^, | 연산자](#---연산자)
    - [이동 연산자](#이동-연산자)
      - [왼쪽 이동 연산자 <<](#왼쪽-이동-연산자-)
      - [오른쪽 이동 연산자 >>](#오른쪽-이동-연산자-)
  - [마스킹 연산](#마스킹-연산)
  - [패킹과 언패킹](#패킹과-언패킹)
    - [패킹](#패킹)
    - [언패킹](#언패킹)

    </div></details>
<details><summary>
Chapter8 : 전처리기
</summary><div markdown="1">

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
  </div></details>

  <details><summary>
  Chapter9 : 입력과 출력
  </summary><div markdown="1">

1. [getchar()와 putchar()](#getchar()와-putchar())
    - [getchar()](#getchar())
    - [putchar()](#putchar())
2. [표준입출력 장치](#표준입출력-장치))
    - [입출력 재지정(<, >)](#입출력-재지정(<,\>))
    - [파이프(|)](#파이프(|))
    - [printf()](#printf())
      - [플래그](#플래그)
      - [폭](#폭)
      - [정밀도](#정밀도)
      - [형변환자](#형변환자)
    - [scanf()](##scanf())
      - [*](#*)
      - [폭](#폭)
      - [변환문자](#변환문자)
      - [참고](#참고)
    - [sprintf()와 sscanf()](#sprintf()와-sscanf())
      - [sprintf(),sscanf()의 특징](#sprintf(),sscanf()의-특징) 
3. [파일입출력](#파일입출력)
   - [fopen()](#fopen())
     - [모드](#모드)
   - [fclose()](#fclose())
   - [getc()와 putc()](#getc()와-putc())
   - [fprintf()와 fscanf()](#fprintf()와-fscanf())
4. [파일의 임의의 위치 접근](#파일의-임의의-위치-접근)
   - [ftell()](#ftell())
   - [fseek()](#fseek())
     - [place](#place)
   - [rewind()](#rewind())
5. [이진 파일](#이진-파일)
   - [fwrite()](#fwrite())
   - [fread()](#fread())

  </div></details>
<details><summary>
Chapter10 : 고급 프로그래밍
</summary><div markdown="1">

1. [메모리배치](#메모리배치)
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
</div></details>