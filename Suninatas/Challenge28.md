## Challenge 28

<br>

1. 문제

   ![](./images/1587037139594.png)

   ​		→ 암호가 없는데 암호를 입력하라고 함

   ​		⇒ ZIP 포맷을 이용해 암호 메세지가 뜨도록 변형을 주었을 것

<br>

2. 파일 다운로드

   ![1587037494981](./images/1587037494981.png)

   <br>

   ![](./images/1587037681205.png)

   ​							→ 파일에 암호가 걸려 있어 압축 해제 불가능

<br>

3. ZIP 파일 분석

   - ZIP 구조

     ![](./images/1587039117690.png)

     ​						→ local file header + file data + data descriptor가 반복

     ​						→ 마지막에 Central directory 위치

     <br>

     ![1587040022058](./images/1587040022058.png)

     ​		→ Local file header의 Signature : [50 4B 03 04]

     ​		→ Flag

     ​										![](./images/1587039681366.png)

     ​											→ Bit 00 : 암호화된 파일 의미

     <br>

     ![1587039274619](./images/1587039274619.png)

     ​								→ Central directory에 ZIP 안 파일들의 암호화 정보가 들어있음

     <br>

     ![1587039350309](./images/1587039350309.png)

     ​		→ Central directory file header의 Signature : [50 4B 01 02]

     ​		→ Flag

     ​										![](./images/1587039681366.png)

     ​											→ Bit 00 : 암호화된 파일 의미

     

   <br>

4. ZIP 파일 hex 수정

   ![1587040166338](./images/1587040166338.png)

   → Local file header : 3개 존재

   <br>

   ![1587040191507](./images/1587040191507.png)

    → 현재 Flag : [09 08]

   - [09 08] = 00001001 00001000

   - Bit 00을 0으로 set (little endian)

     ⇒ 00001000 00001000 = [08 08]

   <br>

   ![1587039737111](./images/1587039737111.png)

   → Central directory file header: 3개 존재

   <br>

   ![1587039769750](./images/1587039769750.png)

   → 현재 Flag : [09 08]

   - [09 08] = 00001001 00001000

   - Bit 00을 0으로 set (little endian)

     ⇒ 00001000 00001000 = [08 08]

<br>

5. ZIP 파일 압축 해제

   ![1587040529242](./images/1587040529242.png)

   ​					→ 암호 없이 압축 해제

<br>

6. AuthKey 확인

   1) Am_I_key2.txt	![1587040587720](./images/1587040587720.png)

   <br>

   2) Am_I_key3.txt

   ![1587040614340](./images/1587040614340.png)

   <br>

   3) Am_I_key.zip - There_is_key.txt

   ![](./images/1587040675366.png)

   → Base64 복호화

   ![1587040730527](./images/1587040730527.png)

   ⇒ AuthKey : `ta5ty_H4z3lnut_coffee`

