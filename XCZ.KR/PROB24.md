## PROB24 : Memoryyyyy Dumpppppp

<br>

1. 문제

   ![](C:\Users\YONGHA.LEE\AppData\Roaming\Typora\typora-user-images\1587560338177.png)

<br>

2. 파일 다운로드

   ![1587632354626](C:\Users\YONGHA.LEE\AppData\Roaming\Typora\typora-user-images\1587632354626.png)
   
   ​	<br>
   
   1) xczprob2.7z.001 파일 압축 해제![1587632384504](C:\Users\YONGHA.LEE\AppData\Roaming\Typora\typora-user-images\1587632384504.png)
   
   ​	⇒ 메모리 덤프 파일

<br>

3. 파일 분석

   - volatility 이용

   1) 이미지 시스템 분석

   ![1587632675197](C:\Users\YONGHA.LEE\AppData\Roaming\Typora\typora-user-images\1587632675197.png)

   → `vol.py -f "xczprob2" imageinfo`

   ⇒ WinXP 플러그인 사용
   
   <br>
   
   2) psxview
   
   - pslilst 및 psscan에서 확인한 프로세스 정보를 비교하여 나열함으로써, 은폐된 프로세스 정보 획득
   
   - pslist
     - 실행 중인 프로세스 정보 나열
   - psscan
     - 실행 중인 프로세스 정보와 함께 이미 종료된 프로세스 정보 나열
   
   <br>
   
   ![1587730880592](C:\Users\YONGHA.LEE\AppData\Roaming\Typora\typora-user-images\1587730880592.png)
   
   → `vol.py -f "xczprob2" psxview`
   
   → pslist, psscan 중 하나라도 False 값이 나오면 은폐된 프로세스라고 의심할 수 있음
   
   <br>
   
   3) connections
   
   - 활성화 상태의 네트워크 연결 정보 나열
   
   ![1587731614707](C:\Users\YONGHA.LEE\AppData\Roaming\Typora\typora-user-images\1587731614707.png)
   
   → `vol.py -f "xczprob2" connections`
   
   ⇒ PID 1124, 즉 nc.exe의 네트워크 연결 정보 존재
   
   ⇒ Port : 80
   
   <br>
   
   4) pstree
   
   - 실행 중인 프로세스의 상관 관계 정보 확인
   
   ![](C:\Users\YONGHA.LEE\AppData\Roaming\Typora\typora-user-images\1587731284633.png)
   
   → `vol.py -f "xczprob2" pstree`
   
   ⇒ nc.exe 프로세스 실행 중
   
   ⇒ Process Execute Time : 2012-11-02 09:06:48

<br>

-------------------

<br>

#### 인증키 구하기

<br>

Process Name_PID_Port_Process Execute Time(Day of the week-Month-Day-Hour:Min:Sec-Years

⇒ AuthKey : `nc.exe_1124_80_Fri-Nov-02-09:06:48-2012`

​	