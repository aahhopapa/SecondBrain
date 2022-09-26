### 날짜 :  2022-08-27 09:01

### 인덱스 : [[3.1.5 Git]]

### 태그 : #Linux, #Ubuntu, #Git

----

### 메모 :

- #### 우분투에서 git 설치하기

1. 패키지 리스트를 업데이트
```shell
sudo apt-get install git
```

2.  깃을 설치
```shell
sudo apt install git
```

3. 설치된 깃 버전 확인
```shell
git --version
```

4. 깃으로 관리할 디렉토리로 이동하여 초기화 하기
```shell
cd /[깃으로-관리할-폴더]

git init
```


5. 깃에 사용자 정보 설정 하기
 프로젝트마다 다른 사용자 정보를 활용하려면 --global 옵션을 제외하고 실행한다
```shell
git config --global user.name [이름]

git config --global user.mail [메일 주소]
```

설정후 사용자 정보를 확인한다
```shell
git config --list
```

만약  설정한 사용자 정보를 다시 변경하려고 한다면 위의 명령문을 
변경하고 싶은 이름과 메일 주소로 다시 입력 하면 된다.

----
### 출처 :
- [깃저장소에 처음 추가하는 법-리모트](https://velog.io/@leyuri/Git-remote-%EB%A6%AC%EB%AA%A8%ED%8A%B8-%EC%A0%80%EC%9E%A5%EC%86%8C-%EC%A0%80%EC%9E%A5%EC%86%8C-%EC%B6%94%EA%B0%80%ED%95%98%EB%8A%94-%EB%B2%95)

- [git config 유저네임, 메일, 변경및 삭제하는법](https://webisfree.com/2018-07-26/git-config-%EC%84%A4%EC%A0%95-%ED%99%95%EC%9D%B8-%EB%B0%8F-%EB%B3%80%EA%B2%BD%ED%95%98%EA%B8%B0)

### 연결메모
-

 






