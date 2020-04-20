## Game 30

<br>

1. 문제

   ![1587137253428](C:\Users\YONGHA.LEE\AppData\Roaming\Typora\typora-user-images\1587137253428.png)

<br>

2. 파일 다운로드

   ![1587139344447](C:\Users\YONGHA.LEE\AppData\Roaming\Typora\typora-user-images\1587139344447.png)

   ​	→ 메모리 덤프 파일

<br>

3. 파일 분석

   - Volatility 이용

     > Open source 기반으로 CLI 인터페이스를 제공하는 python 기반의 메모리 분석 도구

     - Windows에 Volatility 설치

       ```
       git clone https://github.com/volatilityfoundation/volatility3.git
       cd volatility3
       python setup.py build
       ```
     
     - 이미지 시스템 분석
     
       ![	](C:\Users\YONGHA.LEE\AppData\Roaming\Typora\typora-user-images\1587307631963.png) 
     
       → `vol.py -f "MemoryDump(SuNiNaTaS)" imageinfo`
     
       - imageinfo
         - 이 정보를 통해 플러그인 사용 가능
     
       ⇒ Win7SP1x86 플러그인 사용

<br>

-----------------------

<br>

#### 1번. 김장군 PC의 IP 주소는?

<br>

1. IP 주소 확인

   ![1587308383704](C:\Users\YONGHA.LEE\AppData\Roaming\Typora\typora-user-images\1587308383704.png)

   → `vol.py -f "MemoryDump(SuNiNaTaS)" --profile=Win7SP1x86 netscan`

   - netscan
     - Windows 7 이후, Windows Server 2008에서 사용되는 Plugin
     - 활성화된 네트워크 연결 정보 알 수 있음 (사용중인 IP, PORT 등)

   ⇒ Local Address : 192.168.197.138

<br>

--------------------------------------------

<br>

#### 2번. 해커가 열람한 기밀문서의 파일명은?

<br>

1. 프로세스 확인

   - 문서를 읽기 위한 프로그램, 즉 문서를 읽는 프로세스 실행

   ![1587309043081](C:\Users\YONGHA.LEE\AppData\Roaming\Typora\typora-user-images\1587309043081.png)

   → `vol.py -f "MemoryDump(SuNiNaTaS)" --profile=Win7SP1x86 pstree`

   - pstree
     - 프로세스의 상관 관계 정보
     - "." 기호를 통해 부모 / 자식 프로세스를 tree 형태로 나열하여 출력

   ⇒ notepad.exe로 문서를 읽은 것으로 추정

   ​	부모 프로세스 cmd.exe.가 존재하는 것으로 보아, cmd 창을 통해 notepad를 실행하였을 것

<br>

2. cmd 실행 기록 확인

   ![1587309396141](C:\Users\YONGHA.LEE\AppData\Roaming\Typora\typora-user-images\1587309396141.png)

   → `vol.py -f "MemoryDump(SuNiNaTaS)" --profile=Win7SP1x86 cmdscan`

   - cmdscan
     - 사용자가 cmd.exe를 통해 입력한 명령어 출력

   ⇒ 열람한 파일 : C:\Users\training\Desktop\SecreetDocumen7.txt

<br>

----------------------------

<br>

#### 3번. 기밀문서의 주요 내용은? 내용속에 "Key"가 있다

<br>

1. 메모리 덤프에서 데이터 복구

   - R-Studio 이용

     > 데이터 복구 유틸리티 세트

     ![1587311731595](C:\Users\YONGHA.LEE\AppData\Roaming\Typora\typora-user-images\1587311731595.png)

     → 메모리 덤프 파일 scan 

     → 파일 경로 따라 기밀문서 찾아 recover

     ![1587311809820](C:\Users\YONGHA.LEE\AppData\Roaming\Typora\typora-user-images\1587311809820.png)

<br>

2. 기밀문서 내용 확인

   ![1587311870813](C:\Users\YONGHA.LEE\AppData\Roaming\Typora\typora-user-images\1587311870813.png)

   ⇒ Key : 4rmy_4irforce_N4vy

<br>

------------------

<br>

#### 인증키 구하기

<br>

lowercase(MD5(1번답 + 2번답 + 3번키))

→ 192.168.197.138 + SecreetDocumen7.txt + 4rmy_4irforce_N4vy

→ MD5(192.168.197.138SecreetDocumen7.txt4rmy_4irforce_N4vy)

![1587310162628](C:\Users\YONGHA.LEE\AppData\Roaming\Typora\typora-user-images\1587310162628.png)

→ lowercase(c152e3fb5a6882563231b00f21a8ed5f)

⇒ AuthKey : `c152e3fb5a6882563231b00f21a8ed5f`