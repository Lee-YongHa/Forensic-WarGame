## PROB36 : File Deleted

<br>

1. 문제

   ![1588061704791](./images/1588061704791.png)

<br>

2. 파일 다운로드

   ![1588061821621](./images/1588061821621.png)
   
   ​	<br>
   
   1) file_deleted.7z 파일 압축 해제
   
   ![1588062184360](./images/1588062184360.png)

<br>

3. 파일 분석

   1) Recent(최근 파일) 분석

   ![1588062272859](./images/1588062272859.png)

   → s3c37t.avi.lnk : 수상한 동영상 파일 발견

   ⇒ 해당 파일 추출

   <br>
   
   2) s3c3r7.avi 분석
   
   ​	![1588062390495](file://C:/Users/YONGHA.LEE/AppData/Roaming/Typora/typora-user-images/1588062390495.png?lastModify=1588062404)
   
   ​		→ 파일 속성으로 원본 파일의 경로 획득
   
   ​		⇒ 원본 경로 : H:\study\s3c3r7.avi
   
   <br>

4. LNK

   > 링크 파일. 윈도우 운영체제에서 바로가기를 생성하는데 사용되는 포맷

   1) LNK File Format

   ![1588064539918](./images/1588064539918.png)

   ​	<br>

   2) SHELL_LINK_HEADER 구조![](./images/1588065191219.png)

   ​	

4) LINKINFO 구조![1588064773727](./images/1588064773727.png)

<br>

- VolumeID 구조

  ![1588064808338](./images/1588064808338.png)

<br>

5. s3c3r7.avi.lnk 파일 분석

   - 010 Editor 이용

   1) SHELL_LINK_HEADER 분석

   ![1588065152876](./images/1588065152876.png)

   ⇒ 만들어진 시간 : 20131016135210 (GMT+9 적용)

   ⇒ 마지막 실행된 시간 : 20131016232450 (GMT+9 적용)

   ⇒ 쓰인 시간 : 20131016193747 (GMT+9 적용)

   <br>

   2) LINKINFO - VolumeID 분석

   ![](./images/1588065539827.png)

   ⇒ 볼륨 시리얼 : D0A8-02A9

<br>

------

<br>

#### 인증키 구하기

<br>

lowercase(md5(원본 경로\_만들어진 시간\_마지막 실행된 시간\_쓰인 시간\_볼륨 시리얼))

→ H:\study\s3c3r7.avi_20131016135210_20131016232450_20131016193747_D0A8-02A9

→ md5(H:\study\s3c3r7.avi_20131016135210_20131016232450_20131016193747_D0A8-02A9)

![1588072467355](./images/1588072467355.png)

→ lowercase(66f67cd42c58763fd8d58eed6b5bfdba)

⇒ AuthKey : `66f67cd42c58763fd8d58eed6b5bfdba`

