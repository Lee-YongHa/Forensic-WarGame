## Puzzle #1: Ann's Bad AIM

From : http://forensicscontest.com/2009/09/25/puzzle-1-anns-bad-aim

<br>

1. 문제

   ![1588692864851](./images/1588692864851.png)
   
   ​	→ IM : Instant Message
   
   ​	⇒ TCP 분석

<br>

2. 파일 다운로드

   ![1588692904425](./images/1588692904425.png)

   ​	→ PCAP : Wireshark, TcpDump/WinDump, snort 등 많은 네트워크 툴에서 캡쳐된 네트워크 데이터 저장

<br>

--------------

<br>

#### 1. What is the name of Ann's IM buddy?

<br>

1. 파일 분석

   - Wireshark 이용

   1) TCP stream 분석

   ![1588693511572](./images/1588693511572.png)

   → Analyze - Follow - TCP stream

   <br>

   ![1588693635504](./images/1588693635504.png)

   → 숫자를 하나씩 올려가며 메시지 확인

   <br>

   ![1588693714003](./images/1588693714003.png)

   → 2번 stream에서 이름이 등장

   → `Sec558user1`이 자주 등장하고, `DEST`는 destination을 의미하는 것으로 추측

   ⇒ `Sec58user1`이 수신자일 것으로 추측

   <br>

   2) AIM 메시지 확인

   ![](./images/1588693934200.png)

   → 대화 내용 중 하나 선택

   → Decode As

   <br>

   ![](./images/1588693970870.png)

   → Tcp port 443 확인

   → AIM 메시지로 decode

   <br>

   ![1588694295423](./images/1588694295423.png)

   ⇒ Buddy : `Sec558user1`

<br>

----------

<br>

#### 2. What was the first comment in the captured IM conversation?

<br>

1. 파일 분석

   1) 첫번째 방법 : TCP stream

   ![](./images/1588694791254.png)

   ⇒ First comment : `Here's the secret recipe`

   <br>

   2) 두번째 방법 : aim.buddyname 필터링

   ![](./images/1588694636318.png)

   ⇒ First comment : `Here's the secret recipe`

<br>

----------

<br>

#### 3. What is the name of the file Ann transferred?

<br>

1. 파일 분석

   1) 첫번째 방법 : TCP stream

   ![1588694810700](./images/1588694810700.png)

   ⇒ File name : `recipe.docx`

   <br>

   2) 두번째 방법 : aim.buddyname 필터링

   ![1588695050880](./images/1588695050880.png)

   ⇒ File name : `recipe.docx`

<br>

----------

<br>

#### 4. What is the magic number of the file you want to extract (first your bytes)?

<br>

1. 파일 분석

   1) TCP stream

   ![](./images/1588696241105.png)

   → 5번 stream에 recipe.docx 등장

   <br>

   ![](./images/1588696192451.png)

   → 5번 stream의 recipe.docx 부분을 Raw로 Save as

   <br>

   2) 5번 stream 분석

   ![1588695468715](./images/1588695468715.png)

   → File Magic Number = File Signature

   → DOCX 파일의 signature : [50 4B 03 04]

   ⇒ Magic number : `50 4B 03 04`

<br>

------

<br>

#### 5. What was the MD5sum of the file?

<br>

1. recipe.docx 파일 생성

   ![1588695637907](./images/1588695637907.png)

<br>

2. MD5sum 계산

   ![1588696320805](./images/1588696320805.png)

   → Analysis - Checksums - MD-5

   ⇒ MD5sum : `8350582774E1D4DBE1D61D64C89E0EA1`

<br>

----------

<br>

#### 6. What is the secret recipe?

<br>

1. recipe.docx 파일 확인

   ![1588696401515](./images/1588696401515.png)