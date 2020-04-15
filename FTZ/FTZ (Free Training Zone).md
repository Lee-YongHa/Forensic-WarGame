## FTZ (Free Training Zone)



- hacker school 에서 배포하는 무료 트레이닝 워게임(War-Game)

- level 1 ~ level 20

- 각 레벨의 사용자로 시스템에 로그인한 후, 주어진 문제를 풀어가며 다음 단계로 진행하는 워게임 서버

<br>  

-----------------------------------

<br>

```c
level1:x:3001:3001:Level 1:/home/level1:/bin/bash
level2:x:3001:3001:Level 2:/home/level2:/bin/bash
level3:x:3001:3001:Level 3:/home/level3:/bin/bash
level4:x:3001:3001:Level 4:/home/level4:/bin/bash
level5:x:3001:3001:Level 5:/home/level5:/bin/bash
level6:x:3001:3001:Level 6:/home/level6:/bin/bash
level7:x:3001:3001:Level 7:/home/level7:/bin/bash
level8:x:3001:3001:Level 8:/home/level8:/bin/bash
level9:x:3001:3001:Level 9:/home/level9:/bin/bash
level10:x:3001:3001:Level 19:/home/level10:/bin/bash
level11:x:3001:3001::/home/level11:/bin/bash
level12:x:3001:3001::/home/level12:/bin/bash
level13:x:3001:3001::/home/level13:/bin/bash
level14:x:3001:3001::/home/level14:/bin/bash
level15:x:3001:3001::/home/level15:/bin/bash
level16:x:3001:3001::/home/level16:/bin/bash
level17:x:3001:3001::/home/level17:/bin/bash
level18:x:3001:3001::/home/level18:/bin/bash
level19:x:3001:3001::/home/level19:/bin/bash
level20:x:3001:3001::/home/level20:/bin/bash
```

<br>

-------------------

<br>

#### 각 레벨 사용자의 file

- hint (파일)
  - 문제를 풀기 위한 힌트가 들어있는 파일
- public_html (디렉터리)
  - 권한을 획득하면 자랑할 수 있는 웹 문서의 공간
- tmp (디렉터리)
  - 공격에 필요한 소스코드를 작성하거나 연습할 수 있는 공간
- my-pass (실행파일)
  - 자신의 password를 확인할 때 사용하는 파일
