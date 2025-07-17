GIT & GITHUB에 관하여
======================

> 이게머지   

# 1. GIT & GITHUB를 왜 쓰는걸까?
## 1.1. GIT이란?
코드 변경점 기록(버전 관리 도구). 
오류가 나기 전의 코드로 돌아가서 고쳐야할 때

## 1.2. GITHUB란?
온라인 백업, 공유, 협업(온라인 코드 저장소)
# 2. linux 기본 명령어
1. pwd: print working directory. 현재 내가 작업하는 폴더를 보여달라는 뜻
2. ls: list. 현재 경로 내의 폴더와 파일 내역을 보여달라는 뜻
3. ls -a: list all. 숨겨진 파일도 모두 보여달라는 뜻
4. cd 폴더명: change directory. 해당 디렉토리로 이동하라는 뜻
5. ..: 한 단계 위의 폴더라는 뜻
 
# 3. GIT 필수 명렁어 list
1. git init
2. git add
3. git commit
4. git status
5. git log
6. git push
7. git clone
8. git pull
9. git branch
10. git checkout
11. git merge

### 1.2.2. 단점
	1. 표준이 없다.
	2. 표준이 없기 때문에 도구에 따라서 변환방식이나 생성물이 다르다.
	3. 모든 HTML 마크업을 대신하지 못한다.

****
# 2. 마크다운 사용법(문법)
## 2.1. 헤더Headers
* 큰제목: 문서 제목
    ```
    This is an H1
    =============
    ```
    This is an H1
    =============

* 작은제목: 문서 부제목
    ```
    This is an H2
    -------------
    ```
    This is an H2
    -------------

* 글머리: 1~6까지만 지원
```
# This is a H1
## This is a H2
### This is a H3
#### This is a H4
##### This is a H5
###### This is a H6
```
# This is a H1
## This is a H2
### This is a H3
#### This is a H4
##### This is a H5
###### This is a H6
####### This is a H7(지원하지 않음)

## 2.2. BlockQuote
이메일에서 사용하는 ```>``` 블럭인용문자를 이용한다.
