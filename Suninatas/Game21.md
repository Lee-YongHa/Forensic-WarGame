## Game 14

<br>

1. 문제

   ![1586953909605](./images/1586953909605.png)

<br>


2. 파일 다운로드

   ![1586953983416](./images/1586953983416.png)

<br>

3. 파일 분석

   - Notepad++ editor 이용

     1) passwd

     ![](./images/1587014656788.png)

     <br>

     2) shadow

     ![](./images/1587014624951.png)## Game 21

<br>

1. 문제

   ![](./images/1587033151321.png)

<br>

2. 이미지 파일 다운로드

   ![](./images/1587033205901.png)

<br>

3. 이미지 파일 분석

   ![1587033330147](./images/1587033330147.png)
   
​				→ JPG 파일임에도 파일의 크기가 비정상적으로 큼
   
<br>
   
- JPEG(Joint Photographic Experts Group) : 정지 화상(사진)을 위해서 만들어진 손실 압축 방법 표준
   
     - .jpg, .jpeg 등의 확장자 사용
     - 높은 압축률로 인해 웹 상에서 사진 등의 화상을 보관하고 전송하는 데 가장 널리 사용되는 파일 형식
   
     | File Type | Header Signature (hex) | Footer Signature (hex) |
     | :-------: | :--------------------: | :--------------------: |
     | JPEG/JFIF |      FF D8 FF E0       |         FF D9          |
     | JPEG/EXIF |      FF D8 FF E1       |         FF D9          |
   
   <br>

4. HEX 분석

   - JPEG/EXIF 형식의 파일이므로, 헤더 시그니처인 [FF D8 FF E1] 검색

   ![](./images/1587034993485.png)

   ![](./images/1587035031501.png)

   → 이외에도 여러 곳에서 헤더 시그니처 발견

   ⇒ 여러 장의 JPEG 파일이 한 장의 JPEG 파일로 겹쳐져 있음

<br>

5. File Carving (파일 카빙)

   - 헤더 시그니처를 기준으로 끊어 각각 JPEG 파일로 저장

     1) 1.jpg

     ![1587035185213](./images/1587035185213.png)

     <br>

     2) 2.jpg

     ![1587035222314](./images/1587035222314.png)

     <br>

     3) 3.jpg

     ![1587035232552](./images/1587035232552.png)

     ⇒ 이 3장의 JPEG 파일이 반복해서 생성됨

<br>

6. AuthKey 확인

   1) 1.jpg

   ![1](C:\Users\YONGHA.LEE\Security-Study\Suninatas\images\1.jpg)

   <br>

   2) 2.jpg

   ​	![	](C:\Users\YONGHA.LEE\Security-Study\Suninatas\images\2.jpg)

   <br>

   3) 3.jpg

   ​	![3](C:\Users\YONGHA.LEE\Security-Study\Suninatas\images\3.jpg)

   ​	⇒ AuthKey : `H4CC3R_IN_TH3_MIDD33_4TT4CK`

<br>

4. Password Cracking (패스워크 크래킹)

   - John the Ripper 이용

     > Unix 계열 password crack tool

<br>

         1) 크래킹할 파일(shadow)을 txt 파일로 만들기

![	](./images/1587014951102.png)	

<br>

         2) john.exe 이용해 패스워크 크래킹

![	](./images/1587015040566.png)<br>

⇒ AuthKey : `iloveu1`	



