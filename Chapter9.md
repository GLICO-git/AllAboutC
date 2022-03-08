# 입력과 출력
## 목차
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

***
## getchar()와-putchar()
- 함수 원형 :<br> int getchar(void);<br>int putchar(int c);
***
### getchar()
- 표준 입력 장치로 문자를 하나 읽는 함수
- 읽을 문자가 없으면 EOF 리턴   <br>//  End Of File(#define EOF -1)
***
- ex)<br>
`int ch = getchar();`
***
### putchar()
- 표준 출력장치로 문자를 하나 쓰는 함수
***
- ex)<br>
`putchar(ch);`
***
## 표준입출력 장치
### 입출력 재지정(<, >)
`$ io_prog < in_file > out_file`
- io_prog의 표준 입력 장치는 in_file이 되고 출력 장치는 out_file이 됨
***
### 파이프(|)
`$ io_prog | io_prog2 | io_prog3`
- io_prog2의 표준 **입력** 장치는 첫 번째 파이프<br>// io_prog의 표준 출력
- io_prog2의 표준 **출력** 장치는 두 번째 파이프<br>// io_prog3의 표준 입력
### printf()
- 첫 인자를 제어 문자열, `%`를 반환 명세라 함
- 변환 명세보다 인자가 많으면 여분의 인자는 무시 됨
- 인자가 적으면 시스템 종속적으로 처리 됨
- 변환 명세 형식 : <br>
`%[플래그][폭][.정밀도][형변환자]변환문자`
#### 플래그
- \- : 필드에서 좌측 정렬
- \+ : 숫자 앞에 +나 -를 항상 붙여 출력
- 공백 : 양수 앞에 공백을 붙여 출력
- 0 : 숫자 우측 정렬로 출력 시 빈 공간 0으로 채움
- \# : 8진수 앞에 0, 16진수 앞에 0x를 출력
***
- ex)

```c
printf("%03d", 2);      // 002
printf("% d", 2);       //   2
printf("%#x", 15);      // 0xF
printf("%-3d", 2);      // 2
printf("%+d", 2);       // +2
```
***
#### 폭
- 필드의 크기(자릿수) 지정
- 양의 정수나 * 사용 (*는 인자로 받아들임)ㅓ
***
- ex)
```c
printf("i = %8d", i);
printf("i = %*d", 8, i);
```
***
#### 정밀도
- .(점) 뒤에 명시
- 변환 문자 별로 의미가 다름.
<br>

변환 문자| 의미
:---:|:---:
a, A, e, E, f, F | 소수점 이하의 자릿수
g, G | 최대 유효 숫자
s | 문자열로부터 출력된 문자 최대 개수
***
- ex)
```c
float pi = 3.141592;
char str[10] = "abcde";

printf("%.2f", pi);       // 3.14
printf("%.6g", pi);       // 3.14159
printf("%.3s", str);      // "abc"
```
***
#### 형변환자

변환문자|뒤에 올 수 있는 변환 문자|변환 형
:---:|:---:|:---:
hh|d, i, o, u, x, X|signed/unsigned char
h|d, i, o, u, x, X| signed/unsigned short
l|d, i, o, u, x, X| signed/unsigned long
ll|d, i,  o, u, x, X| signed/unsigned long long
z| d, i, o, u, x, X| size_t
L| a, A, e, E, f, F, g, G| long double
***
- ex)
```c
printf("%u", 256);                // 256
printf("%hhu", 256);              // 0
printf("%d", 2100000000);         // 2100000000
printf("%d", 21000000001);         // -4748369475 (overflow)
printf("%d", 21000000001LL);       // -4748369475 (overflow)
printf("%lld", 2100000001LL);     // 2100000001
```
- 256은 2진수로 0001 0000 0000 이다.
- `%hhu`의 경우 char형을 반환 (1byte)하므로 하위 1byte인 0000 0000을 반환한다
***
### scanf()
- 입력 스트림에서 변환명세대로 읽어서 대응인자에 배정함
  - 대응 인자는 포인터이어야 함
- 제어문자열에서 제어문자가 아닌 일반문자는 입력스트림에서 같은 문자를 제거함
- 변환 명세의 형식 : <br>
`%[*][폭][형변환자]변환문자`
***
# *
- 입력스트림의 내용을 지움
***
- ex)
```c
scanf("%d %*d %d", &a, &b);
// 입력 스트림 : 20 50 40
// 20은 a에, 50은 무시, 40은 b에 저장됨
```
***
#### 폭
- 읽어들일 필드 크기 지정
***
- ex)
```c
int a;
char s[10];

scanf("%3d %5c", &a, s);
// 입력 스트림 : 1234567890
// 123은 a에, 45678은 s에 저장
```
***
#### 변환문자
- 원하는 문자들(스캔집합)로만 구성된 문자열을 읽어 들임
- [] 내의 첫 문자가 ^이 아니면 괄호 내의 문자가 스캔 집합이 됨
- ex)
```c
scanf("%[^  \n\t]", s);       // 공백, 개행(\n), 탭(\t) 제외하고 읽음
scanf("%[0-9a-fA-F]", s);     // 숫자와 a~f, A~F 까지만 읽음
// 입력 스트림 : 359ab78dz6b
// 359ab78d 까지만 읽고 나머지는 아직 입력 버퍼에...
```

#### 참고
- 공백 사용시 모든 공백 유지
***
- ex)

```c
scanf("%d%c%d", &a, &b, &c);    // 공백 X
// 입력 스트림 : 57   /     7
// 57은 a에, b와 c에는 공백이 저장됨
scanf("%d %c %d", &a, &b, &c);    // 공백 O
// 입력 스트림 : 57   /     7
// 57은 a에, /는 b에, c에는 7이 저장됨
```

### sprintf()와 sscanf()
- printf()와 scanf()의 문자열 버전(string)
***
- ex)
```c
sscanf(express, "%d", &opd1);
// express 배여레서 %d 형식으로 읽어와 opd1에 저장함

sprintf(result, "%d", opd1);
// opd1을 %d 형식으로, result에 저장함
```
***
#### sprintf(),sscanf()의 특징
- 두 함수는 출력 될 때 마다 문자열의 처음부터 쓰거나 읽음
***
- ex)
```c
char str[] = "1234567890"
int a, b, c, d;

sscanf(str, "%2d%2d", &a, &b);      // a = 12, b= 34
sscanf(str, "%2d%2d", &c, &d);      // c = 12, d= 34
```
- 의도와 달리, c와 d에는 56, 78이 저장되지 않음

- sol)
```c
sscanf(str, "%2d%2d%2d%2d", &a, &b, &c, &d);
// a = 12, b= 34, c = 56, d = 78

sscanf(str+4, "%2d%2d", &c, &d);
// 배열명(str)은 배열 첫 원소의 주소값
```
***

## 파일입출력
- 관련 함수 : <br>
`fopen(), fclose(), fprintf(), fscanf()`
***

### fopen()
- 파일 이름과 모드를 인자로 받음
- 지정된 모드로 파일을 열고 **FILE 포인터**를 리턴함, 실패시 NULL 리턴
***
#### 모드
모드 | 의미
:---:|:---:
r|읽기 모드
w|쓰기 모드
a|첨부 모드(이어쓰기)
b | 이진 파일
r+| 읽고 쓰기 가능
w+ | 읽고 쓰기 가능

- r+와 w+의 차이점 : <br>
r+는 file이 없으면 NULL을 리턴함<br>
w+는 file이 없으면 새로 생성한다<br>

- w 모드를 사용하면 file에 내용이 있다면 내용을 지우고 새로 씀<br>
a 모드는 이어쓰기 이므로 내용을 지우지 않는다
***
- ex)
```c
FILE *ifp, *ofp;
ifp = fopen("infile", "r");
ofp = fopen("outfile", "w");

```
- infile과 outfile의 데이터를 읽고 쓸 때, ifp와 ofp를 통해 읽고 써야 함
***
### fclose()
- fopen() 사용 후에는 fclose()를 사용하여 파일을 닫는다
- 인자로는 fopen()을 통해 리턴 된 FILE 포인터 명시
***
- ex)
```c
fclose(ifp);
fclose(ofp);
```
***
### getc()와 putc()
- 파일 포인터를 갖는다는 것만 제외하면 getchar(), putchar()와 같음
***
- ex 1)
```c
ifp = fopen("1.txt", "r");
ofp = fopen("2.txt", "2");

c = getc(ifp);    // ifp(1.txt)를 읽어와 c에 쓴다
putc(c, ofp);     // c를 ofp(2.txt)에 쓴다
```
- ex 2)
```c
while((c = getc(ifp)) != EOF)
  putc(c, ofp);

while((c = getchar()) != EOF)
  putchar(c);
```
***

### fprintf()와 fscanf()
- printf()와 scanf()의 파일 입출력 버전
- 첫 인자는 FILE 포인터임
***
- ex)
```c
fscanf(pro, "%d", &opd);
// pro 에서 %d 형식으로 읽어와 opd에 저장

fprintf(sol, "%d", opd);
// opd를 %d 형식으로 sol에 저장(쓴다)
```
***
## 파일의 임의의 위치 접근
- 입출력 함수는 이전에 마지막으로 입출력이 일어난 곳 부터 입출력을 실행함
- 파일 위치 지시자 함수들 : <br>
`ftell(), fseek(), rewind()`
***
### ftell()
- 파일 위치 지시자의 현재 값 리턴
- 형식 : <br>
`pos = ftell(FILE_ptr);`

- 리턴 값은 파일의 처음부터 몇 byte 떨어진 곳 인가를 나타냄
- 참고)<br>
영문자 1자 : 1byte<br>
숫자 1개 : 1byte<br>
한글 1자 : 2byte
***
### fseek()
- 파일 위치 지시자의 값을 직접 지정함
- 형식 : <br>
`fseek(FILE_ptr, offset, place);`
- 파일 위치 지시자를 place부터 offset 바이트 떨어진 곳을 나타내는 값으로 설정
***
#### place
값 | 문자 | 의미
:---:|:---:|:---:
0|SEEK_SET|파일의 시작
1|SEEK_CUR|현재 위치
2|SEEK_END|파일의 끝
***
- ex)
``` c
fseek(fp, 5, 0);        // == fseek(fp, 5, SEEK_SET)
// 파일의 시작부분에서 5바이트 떨어진 곳으로 지시자를 지정함

fseek(fp, -2, 2);       // == fseek(fp, -2, SEEK_END);
// 파일의 끝에서 앞으로 2바이트 떨어진 곳으로 지시자를 지정함
```
***
### rewind()
- 파일 위치 지시자를 파일의 제일 앞으로 지정함
- 형식 : <br>
`rewind(FILE_ptr);`<br>
- rewind()함수는 fseek()함수와 같은 효과를 보인다 <br>
`fseek(FILE_ptr, 0, SEEK_SET);`
<br>// 파일의 시작(SEEK_SET)에서 0바이트 떨어진 곳으로 지시자 지정)

## 이진 파일
- 메모리 내용과 같은 형식으로 작성된 파일
- 관련함수 : <br>
`fwrite(), fread()`
***
### fwrite()
- 함수 원형 : <br>
size_t fwrite(const void* buffer, size_t size, size_t count, FILE *fp);

<br>
- buffer : 파일에 쓸 데이터를 가진 포인터<br>
- size : 저장할 각 개체의 크기<br>
- count : 저장할 각 개체의 수<br>
- fp : 저장할 파일 포인터<br>

***

- ex)
```c
fwrite(&st, sizeof(student), 1, ofp);
```
***
### fread()
- 함수 원형 : <br>
size_t fread((const void* buffer, size_t size, size_t count, FILE *fp);

<br>
- buffer : 파일에 쓸 데이터를 가진 포인터<br>
- size : 저장할 각 개체의 크기<br>
- count : 저장할 각 개체의 수<br>
- fp : 저장할 파일 포인터<br>

***

- ex)
```c
fread(&st, sizeof(student), 1, ifp);
```
