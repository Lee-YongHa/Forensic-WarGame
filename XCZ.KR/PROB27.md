## PROB27 : XCZ Company Hacking Incident

<br>

1. 문제

   ![1587732392826](./images/1587732392826.png)

<br>

2. 파일 다운로드

   ![1587732379576](./images/1587732379576.png)
   
   ​	<br>
   
   1) Prob27.7z 파일 압축 해제![1587733318339](./images/1587733318339.png)

<br>

3. 파일 분석

   1) XCZ/Recent 폴더 분석

   ![1587733387378](./images/1587733387378.png)

   ​	→ confidential.doc : 기밀 파일로 의심되는 파일 발견

   <br>

   2) XCZ/Local Settings/Application Data/Identities/{711FB31B-9466-40FA-864A-847B752DD815}/Microsoft 폴더 분석
   
   ![1587733620290](./images/1587733620290.png)
   
   ​	→ Outlook : Microsoft의 전자 메일 프로그램
   
   ​	⇒ 외부 유출 과정에서 사용됐을 것으로 의심
   
   ​	<br>
   
   ![1587733721653](./images/1587733721653.png)
   
   ​	→ dbx : Outlook Express에 의해 생성 된 폴더에 주어진 확장자. 특정 사서함에 대한 전자 메일 메시지를 포함
   
   <br>
   
   3) dbx 파일 분석
   
   - MiTeC Mail View 이용
   
     - Outlook Express Recovery Toolbox
   
     ![1587734530208](./images/1587734530208.png)
   
     → Folders.dbx, Offline.dbx 파일은 열리지 않음. Inbox.dbx에는 메일이 존재하지 않음
   
     → Outbox.dbx에 BOSS에게 보낸 메일 존재. confidential.doc 파일이 첨부되어 있음
   
   <br>
   
   4) confidential.doc 파일 분석
   
   ![1587734663120](./images/1587734663120.png)
   
   → 마지막 줄에 보이지 않는(글씨 색이 투명인) 글이 존재
   
   <br>
   
   ![1587734708288](./images/1587734708288.png)
   
   → 글씨 색을 바꿔주면 키가 보임
   
   ⇒ AuthKey : `Out10OkExpr3s5M4i1`