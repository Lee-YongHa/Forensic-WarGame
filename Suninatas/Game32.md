## Game 32

<br>

1. 문제

   ![](C:\Users\YONGHA.LEE\AppData\Roaming\Typora\typora-user-images\1587310718995.png)

<br>

2. 파일 다운로드

   ![](C:\Users\YONGHA.LEE\AppData\Roaming\Typora\typora-user-images\1587387302362.png)

   ​	→ USB 이미지 파일

<br>

3. 파일 분석

   - FAT32 파일 시스템의 Boot Sector(부트 섹터) - 첫 번째 섹터

   ![1587388139014](C:\Users\YONGHA.LEE\AppData\Roaming\Typora\typora-user-images\1587388139014.png)

   ​	→ Boot Record의 시그니처 [55 AA]의 위치가 맨 끝이 아니라 앞으로 당겨져 있음

   <br>
   
   - Backup Sector(백업 섹터) - 여섯 번째 섹터
   
   ![1587389232215](C:\Users\YONGHA.LEE\AppData\Roaming\Typora\typora-user-images\1587389232215.png)
   
   ​	→ 마찬가지로 시그니처 [55 AA]가 앞으로 당겨져 있음

<br>

3. 파일 복구

   ![](C:\Users\YONGHA.LEE\AppData\Roaming\Typora\typora-user-images\1587389619234.png)

   ​	→ 시그니처 [55 AA]가 섹터의 맨 끝에 위치하도록 216 byte의 Null byte 삽입

   ​	⇒ 다른 섹터도 시그니처 [55 AA]가 맨 끝에 위치하는 것 확인

<br>

4. 복구된 파일 분석

   ![1587389785452](C:\Users\YONGHA.LEE\AppData\Roaming\Typora\typora-user-images\1587389785452.png)

   ​	→ 다음 테러 계획이 들어있는 문서 확인

   <br>

   ![1587389891677](C:\Users\YONGHA.LEE\AppData\Roaming\Typora\typora-user-images\1587389891677.png)

   ​	→ FTK Imager의 Export Files 기능 이용해 문서 파일 복구

<br>

------------

<br>

#### 1번. 다음 테러 계획이 들어있는 문서의 수정 일시는? (UTC+9)

<br>

1. 문서 파일의 속성 확인

   ![1587390022099](C:\Users\YONGHA.LEE\AppData\Roaming\Typora\typora-user-images\1587390022099.png)

   ​				⇒ 수정 일시 : 2016-05-30_11:44:02

<br>

-------------------------

<br>

#### 2번. 다음 테러 장소는?

<br>

1. 문서 파일 확인

   ![](C:\Users\YONGHA.LEE\AppData\Roaming\Typora\typora-user-images\1587390144376.png)

   ​	⇒ 다음 테러 장소 : Rose Park

<br>

------------------

<br>

#### 인증키 구하기

<br>

lowercase(MD5(YYYY-MM-DD_HH:MM:SS_장소))

→ 2016-05-30_11:44:02_Rose Park

→ MD5(2016-05-30_11:44:02_Rose Park)

![](C:\Users\YONGHA.LEE\AppData\Roaming\Typora\typora-user-images\1587390218606.png)

→ lowercase(8ce84f2f0568e3c70665167d44e53c2a)

⇒ AuthKey : `8ce84f2f0568e3c70665167d44e53c2a`
