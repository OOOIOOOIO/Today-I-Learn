.gitignore가 제대로 작동하지 않아서 ignore 처리된 파일이 자꾸 changes에 나올 때가 있다.
git의 캐시 문제 때문이기에 아래 명령어로 캐시 내용을 전부 삭제후 다시 add All해서 커밋하면 된다.

```
해당 git 레포지토리로 이동 후

git rm -r --cached .
git add .
git commit -m "clear git cache"

```

![image](https://user-images.githubusercontent.com/74396651/199991109-cf262730-4133-4cb4-bb81-b58e4974d1d8.png)
