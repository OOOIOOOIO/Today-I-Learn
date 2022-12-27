> organization의 repository를 fork 후 origin/master로 commit / push를 했는데 master 브랜치에는 들어갔는데... main(default)에는 업데이트가 안되었다.. 하하.. 

## 해결법

```
git bash 접속

cd를 사용해 해당 로컬 repo로 이동

git remote -v 로 확인

git checkout master

git branck main master -f

git checkout main

git push origin main -f

을 실행해주면 된다!

```

<hr>

## 코드
![image](https://user-images.githubusercontent.com/74396651/209682634-ccb93674-0da1-4d8d-9c44-426b51edce2c.png)
