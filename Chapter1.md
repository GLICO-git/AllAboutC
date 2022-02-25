#[`마크다운` 사용법]

#

###<제목>

```
#제목
##제목
###제목
####제목
#####제목
######제목
```
#제목
##제목
###제목
####제목
#####제목
######제목
6가지의 헤더 사용 가능
***
###<강조>

```
이텔릭체 *문장* 혹은 _문장_
볼드체 **문장** 혹은 __문장__
밑줄 <u>문장</u>
```
이텔릭체 *문장* 혹은 _문장_
볼드체 **문장** 혹은 __문장__
밑줄 <u>문장</u>
***
###<리스트>
```
1. 순서가 필요한 목록
    - 순서가 필요하지 않은 목록
1. 순서가 필요한 목록
1. 순서가 필요한 목록
- 순서가 필요하지 않은 목록
    - 순서가 필요하지 않은 목록
```

1. 순서가 필요한 목록
    - 순서가 필요하지 않은 목록
1. 순서가 필요한 목록
1. 순서가 필요한 목록
- 순서가 필요하지 않은 목록
    - 순서가 필요하지 않은 목록
***
###<링크>
```
[Google](https://www.google.com).   
Google : https://www.google.com.   
Naver : <https://www.naver.com>.  
[Github][git]

[git] : https://www.github.com
```
[Google](https://www.google.com)
Google : https://www.google.com
Naver : <https://www.naver.com>
[Github][git]

[git]:https://www.github.com
***
###<줄바꿈>
```
안녕하세요<br>감사해요<br>잘있어요 다시만나요
```
안녕하세요<br>감사해요<br>잘있어요  다시만나요
(띄어쓰기 2번이나 `<br>` 적용)
***
###<이미지>
```
![git logo](https://mblogthumb-phinf.pstatic.net/MjAxOTEyMTVfMjc4/MDAxNTc2NDE0MTAwNjg1.cp_9N4gi8GOe7idQjx6pC1LUhK9EqpIs9uArKqZq6iUg.1vF6bTjG3vJW4mb_WagZ5gh0gfwjoo2bznBTEs-tyXkg.JPEG.nilsine11202/github.jpg?type=w800)
```
`![설명](이미지 링크)`
![git logo](https://mblogthumb-phinf.pstatic.net/MjAxOTEyMTVfMjc4/MDAxNTc2NDE0MTAwNjg1.cp_9N4gi8GOe7idQjx6pC1LUhK9EqpIs9uArKqZq6iUg.1vF6bTjG3vJW4mb_WagZ5gh0gfwjoo2bznBTEs-tyXkg.JPEG.nilsine11202/github.jpg?type=w800)
***
###<이미지 링크>
```
[![git logo](https://mblogthumb-phinf.pstatic.net/MjAxOTEyMTVfMjc4/MDAxNTc2NDE0MTAwNjg1.cp_9N4gi8GOe7idQjx6pC1LUhK9EqpIs9uArKqZq6iUg.1vF6bTjG3vJW4mb_WagZ5gh0gfwjoo2bznBTEs-tyXkg.JPEG.nilsine11202/github.jpg?type=w800)](https://www.github.com)
```
이미지 마크다운`![설명](이미지 링크)`을 `[이미지 마크다운](링크)`으로 묶어줍니다.
[![git logo](https://mblogthumb-phinf.pstatic.net/MjAxOTEyMTVfMjc4/MDAxNTc2NDE0MTAwNjg1.cp_9N4gi8GOe7idQjx6pC1LUhK9EqpIs9uArKqZq6iUg.1vF6bTjG3vJW4mb_WagZ5gh0gfwjoo2bznBTEs-tyXkg.JPEG.nilsine11202/github.jpg?type=w800)](https://www.github.com)
사진을 누르면 github로 이동합니다.
***
###<코드강조>
```
`(grave)사용
`코드` 

```
***
###<표>

```
|제목 | 열1 | 열2|
|:---|:---:|:---|
|왼쪽 정렬|가운데 정렬|오른쪽 정렬|
|가나다|10|20|
|라마바|5||

제목 | 열1 | 열2
:---|:---:|:---
왼쪽 정렬|가운데 정렬|오른쪽 정렬
가나다|10|20
라마바|5|
```
헤더의 :을 통해 정렬 위치를 정합니다.
제일 좌,우측의 `|`는 생략이 가능합니다.
|제목 | 열1 | 열2|
|:---|:---:|:---|
|왼쪽 정렬|가운데 정렬|오른쪽 정렬|
|가나다|10|20|
|라마바|5||
***
###<인용문>
```
> 인용문
> 인용문
```

> 퇴근하고 싶다.
> (출처: 글리코)
***
###<수평선>
```
--- (hyphens)
*** (Asterisks)
___ (UnderScores)
```

---
***
___
