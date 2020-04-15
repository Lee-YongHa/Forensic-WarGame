## FTZ 접속

<br>

#### 접속 방법

 1. Red Hat Linux 9.0 접속

    > ID : root	,	PW : hackerschool

<br>

 2. IP 주소 확인

    `ifconfig`

    ![1569215052412](./images/1569215052412.png)

<br>

3. 터미널 프로그램 (Xshell) 으로 시스템에 접속

<br>

4. 웹 서버 시작

   `/usr/local/apache/bin/apachectl start`

   ![1569215680597](./images/1569215680597.png)

   `netstat -nltp`

   ![1569215755321](./images/1569215755321.png)

 <br>  

5. level 1 사용자 문서 생성

   1. level 1 로 접속

      > ID : level1	,	PW : level1	

   2. 웹 문서 (index.html) 파일 생성

      ```
      [level1@ftz level1]$ cd public_html
      [level1@ftz public_html]$ vi index.html
      ```

      ![1569216258539](./images/1569216258539.png)

   3. 생성된 문서 확인

      1. 웹브라우저 접속

      2. http://${FTZ's IP address}/~level1/

         > http://192.168.8.130/~level1/

         ![1569217029905](./images/1569217029905.png)

