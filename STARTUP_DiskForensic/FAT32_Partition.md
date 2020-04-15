## FAT32 파티션 복구



- 손상된 FAT32 파티션 복구
- 해당 파티션 정보는 가지고 있으나, 해당 파티션의 시작 부분이 손상되었을 경우



---------------



1. GUI 형태로 파티션 상태 확인

   - FTK Imager 이용

   ![](C:\Users\YONGHA.LEE\AppData\Roaming\Typora\typora-user-images\1586508448638.png)

   → Evidence Tree의 파티션 정보 확인 : Unrecognized

   ⇒ 파티션 정보 손상



2. 파티션 테이블 확인

   - HxD 이용

   ![1586508966240](C:\Users\YONGHA.LEE\AppData\Roaming\Typora\typora-user-images\1586508966240.png)

   → 파티션 테이블에 하나의 파티션 정보 존재

   → 0x80 : Boot Flag. 부팅 가능한 파티션

   → 0x0B : FAT32 파일시스템

   → [3F 00 00 00] : 파티션 시작 주소 (LBA 주소 지정 방식)

   

3. 파티션이 존재하는 섹터로의 이동

   ![1586509253836](C:\Users\YONGHA.LEE\AppData\Roaming\Typora\typora-user-images\1586509253836.png)

   → [3F 00 00 00] = 0000003F : 63 Sector

   ⇒ 파티션 시작 부분(BR) 손상

   

4. 파티션 정보 백업본 확인

   - FAT32 파일시스템 : 파티션 시작주소에서 6번째 섹터에 파티션 시작 부분(BR)의 백업본 존재

   ![1586509467073](C:\Users\YONGHA.LEE\AppData\Roaming\Typora\typora-user-images\1586509467073.png)

   → 69 : 63(파티션 시작 주소) + 6

   ⇒ 정상적인 BR 백업본 존재 확인



5. BR 수정

   ![1586509679378](C:\Users\YONGHA.LEE\AppData\Roaming\Typora\typora-user-images\1586509679378.png)



6. 복구 여부 확인

   ![1586509763199](C:\Users\YONGHA.LEE\AppData\Roaming\Typora\typora-user-images\1586509763199.png)

   → Evidence Tree의 파티션 정보 확인

   ⇒ 파티션 정보 정상적으로 복구