# Git 명령어
### 저장소 연결
- <code>git init</code> : 저장소 초기화
  - 참고 : [저장소 초기화 : git init, git clone][https://www.lainyzine.com/ko/article/git-init-how-to-initialize-git-repository/] 
- <code>git clone</code> 원격저장소URL : 원격 저장소를 로컬에 복사하기 

### 상태 확인
- <code>git status</code> : 깃 상태(체크아웃된 브랜치 이름, 커밋 내역)(작업 디렉토리와 스테이징 영역의 상태 확인) 확인  
  - Changes to be committed 밑에 초록색으로 적힌 목록은 Tracked 상태이면서 Staged 상태인 파일을 가리킴 
  - Untracked files 밑에 빨간색으로 적힌 목록은 Untracked 상태의 파일을 가리킴 
  - Changes not staged for commit 밑에 modified가 명시된 빨간 리스트는 Tracked 상태이며 modified 상태지만 not staged 상태의 파일을 가리킴 
  - Changes staged for commit 밑에 modified가 명시된 초록 리스트는 modified 상태는 Staged 상태의 파일을 가리킴 
  - 참고 : [깃 명령어][https://dololak.tistory.com/304] 
- <code>git log</code> : 커밋 리스트 보기 
- <code>git diff</code> : 변경 내용 확인 
- <code>git --version</code> : 깃 버전 확인 

### add : 작업 디렉토리 -> 스테이징 영역
- <code>git add</code> : 작업 디렉토리에 있는 모든 또는 일부 변경 내용을 스테이징 영역으로 이동시킴 
  - <code>git add .</code> : 현재 디렉토리의 모든 변경 내용을 스테이징 영역으로 넘김 
  - <code>git add -A</code> : 작업 디렉토리의 모든 변경 내용을 스테이징 영역으로 넘김 
  - ~~<code>git add -p</code> : 각 변경 사항을 터미널에서 확인해가며 선별적으로 스테이징 영역으로 넘김 (안됨)~~ 

### reset : 스테이징 영역 -> 작업 디렉토리 (변경 내용 소멸)
- <code>git reset</code> : 스테이징 영역으로 보낸 작업내역을 수정 이전으로 원상복구 
  - 작업 디렉토리까지도 변경 전 상태로 되돌림 
  
### commit : 스테이징 영역 -> 원격 저장소
- <code>git commit -m "내용"</code> : '내용'이라는 커밋 로그로, 스테이징 영역에서 깃 저장소로 커밋(기록한 걸 위임시킴) 진행 
- <code>git commit --amend -m "커밋 로그"</code> : 직전의 commit에 현재 작업 내용을 포함시켜 다시 commit 
  - 커밋 직후 또 커밋해야 될 때, 그 내용이 너무 사소하여 새로 커밋하기 민망할 때 이용 (기존의 commit에 새로운 commit 덮어쓰기) 

### branch : 버전 관리를 위한 파일 분기
- <code>git branch</code> : 현재 등록된 브랜치의 리스트 확인 
  - <code>git branch --merged</code> : 이미 Merge한 브랜치 목록 확인 (리스트에서 *이 붙은 브랜치는 -d 옵션으로 삭제 가능) 
  - <code>git branch --no-merged</code> : 현재 chekout한 브랜치에 merge하지 않은 브랜치 목록 확인 (해당 리스트의 브랜치들은 -d로 삭제 불가) 
- <code>git branch 생성브랜치명 분기브랜치명</code> : 분기브랜치명에서 브랜치 생성 
```
  git branch RB_1.0 master 
```
- <code>git branch -d</code> 브랜치명 : 로컬 브랜치 삭제 
- <code>git branch -D</code> 브랜치명 : 로컬 브랜치 강제 삭제 (merge하지 않은 브랜치도 삭제 가능) 
- <code>git branch -m</code> 기존브랜치명 변경브랜치명 : 브랜치명 변경 
```
  git branch -m master main 
```
### checkout : 브랜치 간의 이동 (분기 시점 변경)
- <code>git checkout 이동할브랜치명</code> : 현재 위치한 브랜치에서 다른 브랜치로 이동 
- <code>git checkout -b 생성브랜치명</code> : 새로운 브랜치 생성 및 해당 브랜치로 이동 

### merge : 브랜치 간 병합
- <code>git merge main</code> : 로컬 main을 현 브랜치에 병합하여 (현 브랜치 내용 변경) 

### pull/push
- <code>git pull</code> : 원격 저장소 내용 로컬로 가져오기 (원격 저장소와 로컬 저장소의 상태를 동일하게 만듦)
  - <code>git pull origin main --allow-unrelated-histories</code>
  - refusing to merge unrelated histories 오류가 뜰 때 이용  
  - git은 서로 관련 기록이 없는 이질적인 두 프로젝트를 병합하는 것을 거부하는데 이를 허용하는 옵션  
- <code>git push origin main</code> : 커밋한 내역을 origin(원격 저장소)의 main 브랜치에 보냄 
  - origin의 브랜치 이름이 main인지 master인지 확인하기 (2021년쯤부턴 깃헙 origin default는 main)
  - 이 명령어를 사용해야 commit한 내역이 원격 저장소에 올라감