## Steganography3 : Another picture!



1. 문제

   ![1588519611845](../images/1588519611845.png)

<br>

2. 파일 다운로드

   ![1588519786471](../images/1588519786471.png)

<br>

3. 파일 분석

   ![](../images/1588520584029.png)

   → 수상한 16진수 숫자열 발견

   → 16진수 숫자열이 아스키 코드로 변환되어 있음 (0x30 : 0, 0x31 : 1)

   ⇒ 2진수 숫자열

   <br>

4. 2진수 숫자열 해석

   1) 8bit씩 나누기

   ​	![1588520834165](../images/1588520834165.png)

   <br>

   2) 아스키 코드로 변환

   ​	![1588520930091](../images/1588520930091.png)

   ​	⇒ Password : `koekj3s`





