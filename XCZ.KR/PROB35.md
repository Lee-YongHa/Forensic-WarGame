## PROB35 : ZIP

1. 문제

   ![](./images/1587811702398.png)

<br>

2. 파일 다운로드

   ![](./images/1587812074265.png)

<br>

3. 파일 분석

   1) End of Central Directory Record

   ![1587824165157](./images/1587824165157.png)

   ​	→ 압축 파일 내 파일 개수 : 2

   <br>

   2) Local File Header

   ![1587824286994](./images/1587824286994.png)

   ​	→ [50 4B 03 04] : 시그니처 검색. Local File Header 2개 존재

   ​	⇒ 첫 번째 Local File Header 손상 : File name 없음

   <br>

   3) Central Directory

   ![1587824400893](./images/1587824400893.png)

   ​	→ [50 4B 01 02] : 시그니처 검색. Central Directory File Header 1개 존재

   ​	⇒ Central Directory File Header 손상

<br>

4. Local File Header 복구

   ![1587824872487](./images/1587824872487.png)

   ​	→ File Name Length : 9

   ​	⇒ 9만큼 File Name을 만듦

<br>

5. Central Directory File Header 복구

   ![](./images/1587825458073.png)

   ​	→ [00 00 00 00 01 00 20 00 00 00 00 00 00 00] 

   ​				: File comment length + Disk * start + Internal attr + External attr + Relative offset of local header

<br>

6. 복구한 ZIP 파일 압축 해제

   ![1587825502386](./images/1587825502386.png)

<br>

7. AAAAAAAAA 파일 분석

   1) 확장자 찾기

   ![1587825569456](./images/1587825569456.png)

   ​	→ [89 50 4E 47 0D 0A 10 0A] : PNG 파일 Header signature

   <br>

   ![1587825625819](./images/1587825625819.png)

   ​	→ [49 45 4E 44 AE 42 60 82] : PNG 파일 Footer signature

   <br>

   2) 파일 확인

   ​	![AAAAAAAAA](C:\Users\YONGHA.LEE\Desktop\Security-Study\XCZ.KR\AAAAAAAAA.png)

<br>

8. flag.rar 파일 분석

   1) 압축 해제

   ​	![1587825765597](./images/1587825765597.png)

   ​	→ AAAAAAAAA.png 에서 얻은 pw로 압축 해제

   <br>

   2) flag.png 파일 확인

   ​	![flag](C:\Users\YONGHA.LEE\Desktop\Security-Study\XCZ.KR\flag.png)

   ​	⇒ AuthKey : `z1p_1t_f0rmat_1t`

