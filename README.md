# git 명령어 정리

## 환경설정

- **user name**
 ```bash
 git config --global user.name "lee" 
 ```

- **user email**
```bash
 git config --global user.email "lee@abc.com"
```

- **vscode를 editor로 설정하기**
```bash
 git config --global core.edit "code --wait" 
```

- **환경설정파일 edit로 열기**
```bash
 git config --global --edit 또는
 git config --global -e 
```
 
- **명령어 단축별명 설정**
```bash
 git config --global alias.st status  (`git status`를 `git st`로 실행할 수 있음)
```
 
- **crlf(개행문자) 옵션설정 하기**
```bash
  git config --global core.autocrlf true
```

## 1. 초기화 (init)

- **git을 사용할 폴더로 들어와서 init 명령실행하면 git설정파일 설치**
```bash
 git init  
```
  
## 1-1. 그대로 복사(Clone)하기

- **clone 명령을 실행하면 원격repository를 그대로 복사하여 git을 사용할 수 있도록 설정이 완료된 상태가 됨**
```bash
# 원격 repository명과 동일한 이름의 폴더 생성한 후 복사함
 git clone github주소  
```

## 2. 파일을 Stage에 추가하기
```bash
git add . 또는  

git stage . 

```

## 3. 상태정보 확인

```bash
# commit전 파일 stage, 수정 정보확인
git status 

# commit log기록 확인
git log 
```

## 4. Commit하기, Commit 수정하기

```bash
#commit 실행하기
​ git commit -m "메시지내용"

# 직전commit 수정하기
# 파일 수정등 작업을 한 후, 'git add .'명령실행후 --amend 옵션실행
# -m 옵션없이 실행하면 메시지 수정을 위한 edit창이 열리고, 메시지수정후 저장하면 됨
# 파일 수정없이 단순히 커밋 메시지를 수정하는 경우도 사용가능
 git commit --amend  또는
 git commit --amend -m "amend message"

```

## 5. Branch관리 

```bash
# master(초기값)을 main으로 변경
 git branch -M main 

# 새브랜치 만들기
 git branch newBranch

# 브랜치목록
 git branch -l 
# 브랜치전체목록 (remote + local)
 git branch -a 

# 합쳐진 브랜치삭제
 git branch -d branchName
# 안 합쳐진 브랜치도 강제삭제
 git branch -D branchName

# 작업브랜치 변경
 git switch 브랜치명

# 새브랜치만들면서 작업브랜치변경
 git switch -c newBranchName 
 
# 작업브랜치 checkout(선택)
# switch와 유사하나 커밋번호도 선택할 수 있음
# 현재 진행중인 브랜치 커밋을 수정하지 않고 특정커밋부터 별도의 작업을 할 경우,
# 커밋번호 또는 Head(마지막커밋위치)기준 상대위치를 선택하면 Head가 현브랜치에서 분리되어, 커밋번호 위치에 이름없는 브랜치가 생성됨
# 그 상태에서 생성한 커밋작업을 별도 브랜치로 저장하고 싶다면, git switch -c newBranchName 명령실행하면 됨
 git checkout 브랜치명 (switch와 동일)
 git checkout e84e013(커밋번호)
 git checkout HEAD (현재 작업브랜치에서 Head 분리)
 
# 브랜치 특정 commit으로 이동
# 이동시킬 브랜치는 작업브랜치로 선택된 상태가 아니여야 함
 git branch -f main e84e013 (main을 커밋번호 위치로 이동시킴)
 git branch -f main head~3 (main을 head로 부터 3단계 전단계로 이동시킴)
  

```

## 6. tag 만들기 (선택사항)

```bash
# 특정위치에 태그달기, 커밋번호 생략시 현재 커밋위치에 tag생성
 git tag -a "tag명" -m "내용" 커밋번호(or 브랜치명)
 또는
 git tag  tag명 -m "내용" 커밋번호(or 브랜치명)

# tag list확인
​ git tag -l 

# tag 삭제
​ git tag -d "tag명"

```

## 7. 원격서버 주소설정

```bash
​ git remote add origin https://github.com/깃주소.git 
# origin: 사용자가 관리할 원격서버(remote)이름으로 임의지정가능

# 설정된 remote 주소얻기
​ git remote get-url origin

# 원격서버(remote)이름과 주소확인하기
​ git remote -v

# 원격서버 삭제
​ git remote remove origin

```

## 8. github에 push(업로드)하기

```bash
 # push하기
 git push -u origin main  
 # (origin: 나의remote명) (main: 브랜치명)
  
 # tag push하기
 git push --tag origin main

```

## 9. github에서 pull(다운로드 + merge)하기

```bash

# 나의remote명 주소 확인
 git remote -v //

# remote명과 원격서버 주소추가  
 git remote add origin 서버git주소.git //

 git pull origin master  
# (origin: 나의remote명) (master: 서버branch명)

```

## 10. 새로운 브랜치 만들기

```bash
 git switch -c newBranchName

```

## 11. main브랜치에 다른브랜치 합치기

```bash
 git switch main  //main브랜치로 변경
 git merge newBranchName

```
### <충돌메시지 발생시 처리>
- 브랜치 병합시 한개의 파일을 각각의 브랜치에서 수정을 할 경우 자동으로 합치지 못하고 충돌메시지를 발생시키되는데, 
  충돌발생파일을 열면 아래와 같이 충돌발생된 부분이 표시됩니다.

```bash
<<<<<<< HEAD
aaaaa
=======
bbbbb
>>>>>>> newBranchName
```

- 충돌발생 부분은 어떤코드를 삭제할지 모두 남길지 판단하여 필요없는 부분(<<<<<<< HEAD, ===========, >>>>>>> newBranchName, 충돌코드 등)은 삭제한 후 다시 아래와 같은 방식으로 commit을 실행하면 브랜치합치기가 완료됩니다.

```bash
 git add .
 git commit -m "merge 메시지입력" 또는
 git commit  
 # 실행 후 edit 창 뜨면 메시지 수정후 저장 및 닫기
```

## 12. commit 삭제 (reset)
 - commit을 삭제하면 내용도 함께 삭제(변경)되니 주의필요
 - reset 명령으로 지정한 위치로 head위치를 변경시켜서 commit을 삭제하게 됨
 - 
```bash
 # HEAD는 마지막 커밋을 가르키며, ~개수만큼 전단계의 commit위치 가르키게 되어 ~개수 만큼 commit이 삭제됨
 git reset --hard HEAD~~

 # 방금 reset하여 삭제한 commit 복구하기
 # reset전의 커밋은 ORIG_HEAD임
 git reset --hard ORIG_HEAD                            
 
 #또는 방금삭제한 커밋번호 앞7~8자리를 복사하여 복구하기
 git reset --hard 8dbd5ac2(방금삭제한 커밋번호)
 
```

## 13. commit 삭제 -- 삭제이력남기기 (revert)
 - revert명령으로 commit을 취소하면 삭제log이력이 남으나, 
   자료도 함께 삭제되는 것은 reset과 동일하니 주의가 필요합니다.
 - 명령실행하면 edit창이 열리고, 수정메시지를 입력후 창을 닫으면 됩니다.

```bash
# 마지막커밋(Head) 취소하기
 git revert head 

# 실수로 삭제한 경우 복구하기
# 'git log' 실행하여 revert직전 커밋번호를 앞7~8자리 정도 복사한 후 실행
git reset --hard 25d2c3ce(커밋번호) 

```

## 14. commit 복구
 - 실수로 commit을 삭제한 경우 사용

```bash
# reset전의 커밋은 ORIG_HEAD임
​ git reset --hard ORIG_HEAD  

# 커밋번호를 알 경우
​ git reset --hard 8dbd5ac2(방금삭제한 커밋번호)

```

## 15. commit 합치기 (rebase -i)

- 여러개의 commit을 합치고 싶으면 rebase -i 명령어를 사용합니다.

```bash
# 마지막 2개 커밋을 합칠때 아래와 같이 명령을 실행하면 아래와 같이 edit 창이 열립니다.
git rebase -i HEAD~~   

# ~개수만큼 pick 문장이 (여기서는 2개) 나타나고,  2번째 줄 pick을 squash로 변경하고 저장후 edit창을 닫습니다.
```

```bash
 pick 8bb3765 style html 추가
 squash 52dd91b aaa 추가 수정
 
 .....
 
```

- 그러면 합쳐진 commit에 새롭게 추가할 메시지를 입력하는 아래와 같은 edit창이 열리고, 상황에 맞는 메시지를 입력후 창을 닫으면 
commit 합치기가 완료됩니다.

```bash
#This is a combination of 2 commits.
#This is the 1st commit message:
rebase commit 합치기 실행 

#This is the commit message #2:
add ggg등등

```

## 16. rebase 명령취소(rebase --abort)

```bash
 git rebase --abort  //rebase 진행중일 때 취소가능

```
## 17. 명령어 도움말 조회

```bash
 git 명령어 -h

```

## 상세 명령어 설명은 git document(https://git-scm.com/docs) 참고
## 게임을 통해 배우는 git (https://learngitbranching.js.org/?locale=ko)

