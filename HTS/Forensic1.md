## Forensic 1 : First Time Go

<br>

1. 문제

   ![1587391158979](./images/1587391158979.png)

<br>

2. 파일 다운로드

   ![1587394419538](./images/1587394419538.png)

<br>

3. 파일 분석

   1) 파일 압축 해제![1587394479667](./images/1587394479667.png)

   <br>

   2) 휴지통에 있는 파일 복구![1587395116555](./images/1587395116555.png)

   <br>
   
   3) Trash-1000/expunged/2026288587/logins.txt 파일 분석
   
   ​		![1587395199181](./images/1587395199181.png)
   
   ​		⇒ Password : `LittleSister92` 
   
   ​			![1587395292103](./images/1587395292103.png)
   
   ​				⇒ 실패
   
   <br>
   
   4) Trash-1000/expunged/2026288587/Voicemail 1.wav 파일 분석
   
   ```
       ...    
       I sent you a new key over to you.    
       Use your phone number to access file.    
       ...
   ```
   
   → new key와 phone number가 들어있는 파일을 찾아야 함
   
   <br>
   
   5) Trash-1000/expunged/2026288587/Termination - Allen Smith.docx 파일 분석
   
   ​	![1587396111874](./images/1587396111874.png)
   
   ​		⇒ phone number 발견 : 519-555-4783
   
   <br>
   
   6) Trash-1000/expunged/2026288587/private/Your new password is.rar 파일 분석![1587395960030](./images/1587395960030.png)
   
   ​	→ new key, 즉 new password가 들어있을 듯한 파일 발견
   
   <br>
   
   ![1587396169760](./images/1587396169760.png)
   
   ​										→ 암호가 걸려있음
   
   <br>
   
   ![](./images/1587396282560.png)→ 발견한 phone number로 암호 해제
   
   ⇒ new key : `qPYgbs0w5&?i{8a`

