## Git 커맨드라인 명령어

- git help
- git config --global user.name "my name here"
- git config --global user.email "my@email.com"
- git init
- git clone /로컬저장소경로
- git clone user@host:/원격저장소 경로
- git add <file name>
- git rm --cached <filename>    // 깃 add한 파일 취소하기(폴더일 경우 -r 옵션 추가)
- git commit -m "commit message"
- git remote add origin <원격서버 주소>
- git remote add rename <원래 이름> <바꿀 이름>
- git push origin master(branch name)
- git checkout
- git checkout -b <branch name>
- git checkout <branch name>
- git branch -d <branch name>
- git push origin <branch name>
- git push -u <name> <name>
- git pull
- git merge <branch name>
- git add <file name>
- git diff <원래 브렌치> <비교대상 브렌치>
- git tag 1.0.0 1b2e1d63ff
- git log
- git status
- git checkout -- <file name>
- git fetch origin
- git reset --hard origin/master

- git rm        //Remove files from the working tree and from the index
- git bisect    //Find by binary search the change that introduced a bug
- git show      //Show various types of objects
- git rebase    //Forward-port local commits to the updated upstream head
- git move
- git grep

