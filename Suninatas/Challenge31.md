## Challenge 31

<br>

1. 문제

   ![](./images/1587310287281.png)

<br>

2. 파일 다운로드

   ![](./images/1587310329371.png)

   ​	→ PDF 파일 다운로드

<br>

3. 파일 분석

   - PDF Steam Dumper 이용

     > 난독화 PDF 분석 도구
>
     > 모든 오브젝트 및 파일 오프셋, 헤더 등 스트림 상세 내역 분석 가능

     <br>
     
     1) 자바스크립트 변환	
     
     ![1587312364789](./images/1587312364789.png)
     
     → 37번 오브젝트에서 자바스크립트 발견
     
     <br>
     
     ![1587312440191](./images/1587312440191.png)
     
     → PDF Stream Dumper의 기능인 Javascript_UI(JS UI) 기능을 이용해 자바스크립트 포맷으로 변환
     
     <br>
     
     ![1587384285707](./images/1587384285707.png)
     
     → Base64로 11번 Decoding을 실행
     
     ⇒ 키가 아님
     
     <br>
     
     2) PDF 파일 추출
     
     ![](./images/1587384996312.png)
     
     → 39번 오브젝트에서 PDF 헤더 발견 : PDF 1.7 사양을 사용함
     
     <br>
     
     - PDF 파일 구조
     
       ![](./images/1587385046060.png)
     
     ​										→ Header : PDF의 시그니처와 PDF 사양의 버전을 정의
     
     ​										→ Body : 실제 내용을 포함하는 오브젝트들로 구성
     
     ​										→ Cross-reference table : 다른 오브젝트에 빠르게 엑세스하기 위한 PDF 뷰어용 테이블
     
     ​										→ Trailer : PDF 파일의 기타 메타 정보를 정의
     
     <br>
     
     ![1587385536985](./images/1587385536985.png)
     
     → Save Decompressed Stream 기능을 이용해 PDF 파일 추출

​			<br>

4. 추출된 PDF 파일 분석

   ![1587386452301](./images/1587386452301.png)

   ​	<br>

   ![1587386502803](./images/1587386502803.png)	

   → 잠금되어 있음

   <br>

   ![1587386927307](./images/1587386927307.png)

   ​	→ https://smallpdf.com/kr 이용해 PDF 파일 잠금 해제

   <br>

   ![1587387017424](./images/1587387017424.png)

   ⇒ Flag : SunINatAsGOodWeLL!@#$

<br>

-----------------

<br>

#### 인증키 구하기

<br>

lowercase(MD5(Flag))

→ MD5(SunINatAsGOodWeLL!@#$)

![](./images/1587387170213.png)

→ lowercase(13d45a1e25471e72d2acc46f8ec46e95)

⇒ AuthKey : `13d45a1e25471e72d2acc46f8ec46e95`

