## Forensic 3 (PapaSmurphey's Pizza)

<br>

1. 문제

   ![](C:\Users\YONGHA.LEE\AppData\Roaming\Typora\typora-user-images\1587548115409.png)

<br>

2. 파일 다운로드![1587549056750](C:\Users\YONGHA.LEE\AppData\Roaming\Typora\typora-user-images\1587549056750.png)

<br>

3. 파일 분석

   1) 압축 해제

   - forensic_3/flashdrive 폴더 생성

   ![](C:\Users\YONGHA.LEE\AppData\Roaming\Typora\typora-user-images\1587555328410.png)

   <br>

   2)  siggies.txt 파일 분석

   ![](C:\Users\YONGHA.LEE\AppData\Roaming\Typora\typora-user-images\1587555431879.png)

   ​	→ 파일 확장자에 따른 시그니처가 쓰여져 있음

   <br>

   3) shh.jpg 파일 분석![1587555508882](C:\Users\YONGHA.LEE\AppData\Roaming\Typora\typora-user-images\1587555508882.png)

   ​	→ jpg 파일임에도 용량이 너무 큼

   <br>

   ![1587555568144](C:\Users\YONGHA.LEE\AppData\Roaming\Typora\typora-user-images\1587555568144.png)

   ​	→ siggies.txt에서 JPG 확장자의 시그니처 찾음

   <br>

   ![1587555684132](C:\Users\YONGHA.LEE\AppData\Roaming\Typora\typora-user-images\1587555684132.png)

   ​	→ 첫 번째 [FF D8 FF E0] ~ [FF D9] : Header, Footer 시그니처 사이의 데이터를 분리해 1.jpg로 저장

   <br>

   ![](C:\Users\YONGHA.LEE\AppData\Roaming\Typora\typora-user-images\1587555786677.png)

   ⇒ 1.jpg

   <br>

   ![1587555886597](C:\Users\YONGHA.LEE\AppData\Roaming\Typora\typora-user-images\1587555886597.png)

   ​	→ 두 번째 [FF D8 FF E0] ~ [FF D9] : Header, Footer 시그니처 사이의 데이터를 분리해 2.jpg로 저장

   <br>

   ![1587555941178](C:\Users\YONGHA.LEE\AppData\Roaming\Typora\typora-user-images\1587555941178.png)

   ⇒ 2.jpg

   <br>

4. RAR 파일 생성

   ![1587556035284](C:\Users\YONGHA.LEE\AppData\Roaming\Typora\typora-user-images\1587556035284.png)

   → 1.jpg, 2.jpg를 분리하고 남은 데이터의 시그니처

   <br>

   ![1587556109707](C:\Users\YONGHA.LEE\AppData\Roaming\Typora\typora-user-images\1587556109707.png)

   → siggies.txt에서 찾은 RAR 확장자의 시그니처를 편집한 것으로 추측

   <br>

   ![1587556170797](C:\Users\YONGHA.LEE\AppData\Roaming\Typora\typora-user-images\1587556170797.png)

   → RAR 확장자의 시그니처로 수정한 후, after.rar 파일로 저장

<br>

5. after.rar 파일 분석

   1) 압축 해제

   ​	![](C:\Users\YONGHA.LEE\AppData\Roaming\Typora\typora-user-images\1587556265754.png)

   ​		→ 암호가 걸려 있음

   ​		⇒ 2.jpg에 써있는 암호 `GL0zMe`를 이용해 압축 해제

   ​	<br>

   ![1587556448362](C:\Users\YONGHA.LEE\AppData\Roaming\Typora\typora-user-images\1587556448362.png)

   ​	→ after.rar 안에 있던 파일

   <br>

   2) DNM Login.txt 파일 분석

   ​	![1587556520173](C:\Users\YONGHA.LEE\AppData\Roaming\Typora\typora-user-images\1587556520173.png)

   ​	⇒ Password : `HTS{You_caught_me!}`

