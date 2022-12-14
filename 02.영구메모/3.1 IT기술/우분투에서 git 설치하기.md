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


### 블로그 작성
- https://ahopapa.com/ko/%ec%9a%b0%eb%b6%84%ed%88%ac%ec%97%90%ec%84%9c-git-%ec%84%a4%ec%b9%98%ed%95%98%ea%b8%b0/


---
## 일본어


### Ubuntuでgitをインストールする方法

1. パッケージリストを更新
```shell
sudo apt-get install git
```

2. Gitをインストール
```shell
sudo apt install git
```

3. インストールした Git バージョン確認
```shell
git --version
```

4. Gitで管理するディレクトリに移動して初期化する
```shell
cd /[Gitで管理するディレクトリ]

git init
```


5. Gitにユーザー情報を設定する
  プロジェクトごとに異なるユーザー情報を利用するには、 --global オプションを除いて実行します。
```shell
git config --global user.name [名前]

git config --global user.mail [メールアドレス]
```

設定後、ユーザー情報を確認する
```shell
git config --list
```

**設定したユーザー情報をもう一度変更**したい場合は、上記(5)の文を
変更したい名前とメールアドレスに再入力すればよい。


---
### 블로그 기록

https://ahopapa.com/ubuntu-git-%e3%82%a4%e3%83%b3%e3%82%b9%e3%83%88%e3%83%bc%e3%83%ab-%e6%96%b9%e6%b3%95/