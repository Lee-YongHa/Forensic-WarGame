## Puzzle #2: Ann Skips Bail

From : http://forensicscontest.com/2009/10/10/puzzle-2-ann-skips-bail

<br>

1. 문제

   ![1588768998007](./images/1588768998007.png)
   
   ​	→ email
   
   ​	⇒ SMTP 분석

<br>

2. 파일 다운로드

   ![1588769317754](./images/1588769317754.png)

<br>

--------------

<br>

#### 1. What is Ann’s email address?

<br>

1. 파일 분석

   1) 첫번째 방법 : smtp 필터링

   ![1588769765156](./images/1588769765156.png)

   → Ann이 로그인했으므로 Ann이 발신인

   ⇒ Ann's email address : `sneakyg33@aol.com`
   
   <br>
   
   2) 두번째 방법 : 메일 복구
   
   - Windows Live Mail 이용
   
   ![1588769925758](./images/1588769925758.png)
   
   → TCP Stream : 0번 stream
   
   <br>
   
   ![1588769964335](./images/1588769964335.png)
   
   → Raw 데이터 
   
   → mail을 원본형식 그대로 저장한 확장자인 EML 파일로 저장
   
   <br>
   
   ![1588770041045](./images/1588770041045.png)
   
   <br>
   
   ![1588770155978](./images/1588770155978.png)
   
   ⇒ Ann's email address : `sneakyg33@aol.com`


<br>

----------

<br>

#### 2. What is Ann’s email password?

<br>

1. 파일 분석

   1) smtp 필터링

   ![1588770263563](./images/1588770263563.png)

   → Password : NTU4cjAwbHo=

   → Base64 Encoding 추측

   <br>

   2) Base64 Decoding

   ![1588770376524](./images/1588770376524.png)

   ⇒ Password : `558r001z`

<br>

----------

<br>

#### 3. What is Ann’s secret lover’s email address?

<br>

1. 파일 분석

   1) 메일 복구

   ![1588771080775](./images/1588771080775.png)

   → TCP Stream : 1번 stream에서 또 하나의 mail 발견

   → Raw 데이터를 EML 파일로 저장

   <br>

   ![1588771235607](./images/1588771235607.png)

   → sweetheart, love : 이전의 mail보다 친근해 보임
   
   → secret lover에게 보내는 mail로 추측
   
   ⇒ Ann’s secret lover’s email address : `mistersecretx@aol.com`

<br>

----------

<br>

#### 4. What two items did Ann tell her secret lover to bring?

<br>

1. 메일 분석

   ![1588771303225](./images/1588771303225.png)

   ⇒ Two items : `fake passport, bathing suit`

<br>

------

<br>

#### 5. What is the NAME of the attachment Ann sent to her secret lover?

<br>

1. 메일 분석

   ![1588771374710](./images/1588771374710.png)
   
   ⇒ Attachment name : `secretrendezvous.docx`

<br>

----------

<br>

#### 6. What is the MD5sum of the attachment Ann sent to her secret lover?

<br>

1. 메일 분석

   1) 첨부파일 저장
   
   ![1588771491939](./images/1588771491939.png)
   
   <br>
   
   ![1588771553216](./images/1588771553216.png)
   
   <br>
   
   2) 첨부파일 분석
   
   ![1588771619726](./images/1588771619726.png)
   
   ⇒ MD5sum : `9E423E11DB88F01BBFF81172839E1923`

<br>

--------

<br>

#### 7. In what CITY and COUNTRY is their rendez-vous point?

1. 첨부파일 분석

   ![1588771728787](./images/1588771728787.png)

   ⇒ City, Country : `Playa del Carmen, Mexico`

<br>

------

<br>

#### 8. What is the MD5sum of the image embedded in the document?

<br>

1. 첨부파일 분석

   ![1588772003033](./images/1588772003033.png)

   → PNG의 Header, Footer signature 발견

   	- [89 50 4E 47 0D 0A 1A 0A] ~ [49 45 4E 44 AE 42 60 82]
   
   → PNG 영역을 분리해 PNG 파일로 저장
   
   <br>
   
   ![1588772217647](./images/1588772217647.png)

<br>

2. PNG 파일 분석

   ![1588772261357](./images/1588772261357.png)

   ⇒ MD5sum : `AADEACE50997B1BA24B09AC2EF1940B7`