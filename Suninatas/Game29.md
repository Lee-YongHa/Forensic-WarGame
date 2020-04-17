

## Game 29

<br>

1. 문제

   ![](C:\Users\YONGHA.LEE\AppData\Roaming\Typora\typora-user-images\1587127086195.png)


<br>

2. 파일 다운로드

   ![1587127911720](C:\Users\YONGHA.LEE\AppData\Roaming\Typora\typora-user-images\1587127911720.png)

   ​	→ 파일의 확장자를 몰라 열 수 없음


<br>

3. 파일 분석

   ![](C:\Users\YONGHA.LEE\AppData\Roaming\Typora\typora-user-images\1587128465491.png)

   <br>

   - 압축 파일의 시그니처 목록

     | File Type | Header Signature (hex) | ASCII code |
     | --------- | ---------------------- | ---------- |
     | ALZ       | 41 4C 5A 01            | ALZ        |
     | EGG       | 45 47 47 41            | EGGA       |
     | ZIP       | 50 4B 03 04            | PK         |
     | RAR       | 52 61 72 21            | Rar!       |

   <br>

   → EGG 파일로 확장자 수정 후 압축 해제

   ![1587129009527](C:\Users\YONGHA.LEE\AppData\Roaming\Typora\typora-user-images\1587129009527.png)

<br>

-----------------------

<br>

#### 1번. 웹 서핑은 잘 되는데, 네이버에만 들어가면 경찰청 차단 화면으로 넘어간다. 

#### 	  원인을 찾으면 Key가 보인다

<br>

1. www.naver.com 접속 확인

   ![](C:\Users\YONGHA.LEE\AppData\Roaming\Typora\typora-user-images\1587131982092.png)

   → 사이트 차단

   ⇒ DNS 혹은 hosts 조작

<br>

2. hosts 파일 확인

   - hosts 파일 위치 : C:\Windows\System32\drives\etc

   ![1587132249678](C:\Users\YONGHA.LEE\AppData\Roaming\Typora\typora-user-images\1587132249678.png)

   ![](C:\Users\YONGHA.LEE\AppData\Roaming\Typora\typora-user-images\1587132621961.png)	→ 이상 없음

   <br>

   - 숨김 파일, 폴더 및 드라이브 표시 설정

   ![1587132827744](C:\Users\YONGHA.LEE\AppData\Roaming\Typora\typora-user-images\1587132827744.png)

   ![1587132868518](C:\Users\YONGHA.LEE\AppData\Roaming\Typora\typora-user-images\1587132868518.png)

   | naver.com의 올바른 도메인 |
   | :-----------------------: |
   |       210.89.160.88       |
   |      125.209.222.141      |
   |      125.209.222.142      |
   |       210.89.164.90       |

   ​	→ hosts 파일에 naver.com의 도메인이 잘못 설정되어 있음

   ​	⇒ Key : `what_the_he11_1s_keey`

<br>

--------------------

<br>

#### 2번. 유성준이 설치해 놓은 키로거의 절대경로 및 파일명은? (모두 소문자)

<br>

1. 최근 위치 확인

   ![](C:\Users\YONGHA.LEE\AppData\Roaming\Typora\typora-user-images\1587133359937.png)

   ​	→ 수상한 폴더 발견

<br>

2. v196vv8 폴더 분석

   - C:\v196vv8\v1valv\Computer1\17042020 #training\ss 경로 접속

     ![1587134779343](C:\Users\YONGHA.LEE\AppData\Roaming\Typora\typora-user-images\1587134779343.png)

     → 59.jpg : 키로깅되고 있다는 증거

     <br>

     ![1587135502551](C:\Users\YONGHA.LEE\AppData\Roaming\Typora\typora-user-images\1587135502551.png)

     → 9.jpg : 키로거 위치 확인

     ⇒ c:\v196vv8\v1tvr0.exe

<br>

-------------------------------

<br>

#### 3번. 키로거가 다운로드 된 시간은?

<br>

1. BrowsingHistoryView 프로그램 실행

   ![](C:\Users\YONGHA.LEE\AppData\Roaming\Typora\typora-user-images\1587136370261.png)

   → 키로거 다운로드 시간 확인

   ⇒ 2016-05-24_04:25:06

<br>

-----------------------------------------------------

<br>

#### 4번. 키로거를 통해서 알아내고자 했던 내용은 무엇인가? 내용을 찾으면 Key가 보인다

<br>

2. v196vv8 폴더 분석

   - c:\v196vv8\v1valv\Computer1\17042020 #training 경로 접속

     ![1587134075137](C:\Users\YONGHA.LEE\AppData\Roaming\Typora\typora-user-images\1587134075137.png)

     ​	→ 2개의 dat 파일 발견

     <br>

     - w1.dat

       ![1587134149003](C:\Users\YONGHA.LEE\AppData\Roaming\Typora\typora-user-images\1587134149003.png)

     <br>

     - z1.dat

       ![1587134208529](C:\Users\YONGHA.LEE\AppData\Roaming\Typora\typora-user-images\1587134208529.png)

       ​	⇒ Key : `blackkey is a Good man`

<br>

-------------------------

<br>

#### 인증키 구하기

<br>

lowercase(MD5(1번키 + 2번답 + 3번답 + 4번키))

→ what_the_he11_1s_keey + c:\v196vv8\v1tvr0.exe + 2016-05-24_04:25:06 + blackkey is a Good man

→ MD5(what_the_he11_1s_keeyc:\v196vv8\v1tvr0.exe2016-05-24_04:25:06blackkey is a Good man)

​	![](C:\Users\YONGHA.LEE\AppData\Roaming\Typora\typora-user-images\1587136959147.png)

→ lowercase(970f891e3667fce147b222cc9a8699d4)

⇒ AuthKey : `970f891e3667fce147b222cc9a8699d4`