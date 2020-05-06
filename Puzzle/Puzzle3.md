## Puzzle #3: Ann's AppleTV

From : http://forensicscontest.com/2009/12/28/anns-appletv

<br>

1. 문제

   ![](./images/1588772520167.png)
   
   ​	→ 고정 IP : 192.168.1.10

<br>

2. 파일 다운로드

   ![](./images/1588772571854.png)

<br>

--------------

<br>

#### 1. What is the MAC address of Ann’s AppleTV?

<br>

1. 파일 분석

   - Wireshark 이용

   1) ip.addr 필터링

   ![](./images/1588772983073.png)

   ⇒ MAC address : `00:25:00:fe:07:c41`


<br>

----------

<br>

#### 2. What User-Agent string did Ann’s AppleTV use in HTTP requests?

<br>

1. User-Agent
- 사용자를 대신해서 인터넷에 접속하는 소프트웨어
   - 인터넷에 접속할 때 사용자에 관한 정보 전송
  - 브라우저, OS(운영체제) 등

<br>

2. 파일 분석

   1) HTTP stream

   ![](./images/1588774362113.png)

   ⇒ User-Agent : `AppleTV/2.4`

<br>

----------

<br>

#### 3. What were Ann’s first four search terms on the AppleTV (all incremental searches count)?

<br>

1. 파일 분석

   1) 첫번째 방법 : File - Export Objects - HTTP

   ![](./images/1588774545167.png)

   ⇒ First four search terms : `h, ha, hac, hack`

   <br>

   2) 두번째 방법 : String 검색

   ![1588774909330](./images/1588774909330.png)

   → http.request.method == "GET"
   
   	- http 요청 방식이 GET인 것
   
   <br>
   
   ![1588775065014](./images/1588775065014.png)
   
   → http.request.method == "POST"는 존재하지 않음
   
   <br>
   
   ![](./images/1588775129296.png)
   
   → http.request.method == "GET" 필터링 상태에서 string 'incrementalsearch' 검색
   
   ⇒ First four search terms : `h, ha, hac, hack`

<br>

----------

<br>

#### 4. What was the title of the first movie Ann clicked on?

<br>

1. 파일 분석

   1) HTTP 200 OK

   		- 요청이 성공했음을 나타내는 성공 응답 상태 코드

   ![1588776015192](./images/1588776015192.png)

   → 'hack'을 검색한 이후의 패킷에 대해 분석

   → 279 : 'hack' 단어 검색에 대한 HTTP 200 OK, 즉 성공 응답

   → 282 : 281의 GET, 즉 Ann이 클릭 시 발생한 요청에 대한 성공 응답

   <br>

   ![](./images/1588776298188.png)

   → 312 : 클릭 내용에 대한 결과 값을 받아오는 요청에 대한 성공 응답

   → eXtensible Markup Language을 통해 XML 코드 확인

   - Copy - as Printable Text

   <br>
   
   ![](./images/1588776455842.png)
   
   ⇒ Title : `Hackers`

<br>

------

<br>

#### 5. What was the full URL to the movie trailer (defined by “preview-url”)?

<br>

1. XML 분석

   ![](./images/1588776461649.png)
   
   ⇒ URL : `http://a227.v.phobos.apple.com/us/r1000/008/Video/62/bd/1b/mzm.plqacyqb..640x278.h264lc.d2.p.m4v`

<br>

----------

<br>

#### 6. What was the title of the second movie Ann clicked on?

<br>

1. 파일 분석

   1) File - Export Objects - HTTP
   
   ![](./images/1588777546337.png)
   
   → 두번째 검색 단어 : sneak
   
   <br>
   
   2) String 검색
   
   ![1588777644934](./images/1588777644934.png)
   
   → 1168 패킷에서 sneak 단어 검색
   
   <br>
   
   3) HTTP 200 OK
   
   ![1588777742612](./images/1588777742612.png)
   
   → 1168  이후의 패킷에 대해 분석
   
   → 1171 : 'sneak' 단어 검색에 대한 HTTP 200 OK, 즉 성공 응답
   
   → 1174 : 1173의 GET, 즉 Ann이 클릭 시 발생한 요청에 대한 성공 응답
   
   → 1186 : 클릭 내용에 대한 결과 값을 받아오는 요청에 대한 성공 응답
   
   → eXtensible Markup Language을 통해 XML 코드 확인
   
   <br>
   
   4) XML 분석
   
   ![1588777841005](./images/1588777841005.png)
   
   ⇒ Second title : `Sneakers`

<br>

--------

<br>

#### 7. What was the price to buy it (defined by “price-display”)?

1. XML 분석

   ![1588777884467](./images/1588777884467.png)

   ⇒ Price : `$9.99`

<br>

------

<br>

#### 8. What was the last full term Ann searched for?

<br>

1. 파일 분석

   1) File - Export Objects - HTTP

   ![](./images/1588777959229.png)

   ⇒ Last term : `iknowyouwatchingme`

