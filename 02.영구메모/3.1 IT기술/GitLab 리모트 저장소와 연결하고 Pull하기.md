### 날짜 :  2022-08-27 09:16

### 인덱스 : [[3.1.5 Git]]

### 태그 : #Linux

----

### 메모 :

- #### 리모트 저장소와 연결 하기 

![[GitLab 리모트 저장소와 연결하고 Pull하기.png.png]]
저장소 주소 확인: GitLab 

기존 워킹 디렉토리에 새 리모트 저장소를  추가
**git remote add <단축이름>**
```bash
git remote add origin https://방금-복사한-https주소-붙혀넣기
```
**origin** 이라는 이름으로 추가해주었다


**깃허브 원격저장소에 있는 프로젝트를 로컬저장소로 가져오는 방법은 3가지가 있다.**
1. git pull 
2. git fetch  
3. git clone

**git pull 이란?**
git pull = git fetch + git merge


```bash
git pull [원격 저장소의 이름] [원격 저장소에서 받아오고자 하는 브랜치의 이름]
```

git pull 명령어가 안되는 사람은 **"git pull origin master"** 명령어를 입력해보자!  
```bash
git pull pull origin master
```

pull 하려는데 이미 자료가 있어 이런 에러가 발생하는경우....
```bash
fatal: refusing to merge unrelated histories
```

밑의 코드를 입력하여 실행하면 된다
```bash
git pull origin master --allow-unrelated-histories
```

----
### 출처 :
- [git pull 하기](https://sin0824.tistory.com/11)
- [Git-fatal-refusing-to-merge-unrelated-histories-해결-방법](https://somjang.tistory.com/entry/Git-fatal-refusing-to-merge-unrelated-histories-%ED%95%B4%EA%B2%B0-%EB%B0%A9%EB%B2%95)
- [git commit 편집 에디터 바꾸기](https://siyoon210.tistory.com/29)
- [Git변경사항 확인하기 (log, diff)](https://yuja-kong.tistory.com/46)


### 연결메모
-








