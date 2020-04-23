## PROB22 : Who's Notebook?

<br>

1. 문제

   ![1587557591757](./images/1587557591757.png)

<br>

2. 파일 다운로드

   ![1587557641380](./images/1587557641380.png)

<br>

3. 파일 분석

   1) 확장자 찾기

   ![](./images/1587558192655.png)	→ [41 44 53 45 47 4D 45 4E 54 45 44 46 49 4C 45] : AD1 확장자의 시그니처

   ​	<br>

   - AD1

     ![1587558278480](./images/1587558278480.png)

     ​	→ FTK Imager로 디스크 덤프 작업을 할 때 생성되는 파일의 확장자

   <br>

   ![1587558501326](./images/1587558501326.png)

   ​	⇒  확장자 수정

   <br>

   2) notebook.ad1 파일 분석

   ![](./images/1587559634339.png)

   ​	→ GPS 관련 파일 발견

   <br>

   ![1587559381826](./images/1587559381826.png)

   ​	→ www.gpsnote.net 접속

   ​	⇒ GPS ROUTE EDITOR 다운로드

   <br>

   3) 파일 추출

   - FTK Imager의 Export Files 기능을 이용해 GPS 관련 파일 추출

     ![](./images/1587559688780.png)

     ​	→ GPS ROUTE EDITOR가 GPX 확장자 파일을 지원

   <br>

   4) 추출한 파일 분석

   ​	![1587559928052](./images/1587559928052.png)

   ​	→ 빨간 선이 이동한 경로를 나타냄

   ​	⇒ 공덕역 → 김포국제공항 → 동부렌트카

   ​		(지도가 바뀐듯. 과거엔 PLACE3, 즉 도착지가 7-ELEVEN)

   ​		⇒ 공덕역 → 김포국제공항 → 7-ELEVEN

<br>

-------------------

<br>

#### 인증키 구하기

<br>

PLACE1_PLACE2_PLACE3

⇒ AuthKey : `GONGDEOK_GIMPOINTERNATIONALAIRPORT_7-ELEVEN`

​	
