### 날짜 :  2022-08-24 16:01

### 인덱스 : [[3.1.5.3.2 GitLab]]

### 태그 : #GitLab

----

### 메모 :

먼저 C:/Users/유저명/.ssh에 들어가서 pem키가 있어야 한다
없는 경우 ssh를 만들어 줘야한다 (만드는 방법은 밑에 출처를 참고 한다)

***1. gitbash에 아래 명령어 입력한다***
```shell
eval $(ssh-agent)
```
Agent pid 가 나오면 성공

***2. 깃랩 project 첫 페이지로 가서 clone 버튼을 누르면 clone with ssh 가 뜬다.***
gitbash에서 다음 명령어 입력한다
```shell
git clone [깃랩-저장소-ssh-주소]
```
git clone 성공

![[GitLab ssh 키 사용하여 clone 하기.png.png]]

----
### 출처 :
- https://catloaf.tistory.com/37


### 연결메모
- 

### 블로그 작성
- https://ahopapa.com/ko/gitlab-%ea%b9%83%eb%9e%a9-ssh-%ed%82%a4-%ec%82%ac%ec%9a%a9%ed%95%98%ec%97%ac-clone-%ed%95%98%ea%b8%b0/


----
## 일본어 

pemキーが必要なので
まず、C:/Users/ユーザー名/.sshに入り、あるか確認します。
ない場合はsshを作成する必要があります。（作成方法は下のソースを参照してください）

***1. gitbashに以下のコマンドを入力する***
```shell
eval $(ssh-agent)
```
Agent pid が出たら成功

***2. GITLABのプロジェクトページにあるcloneボタンを押すとclone with sshが表示されます。***

gitbashで次のコマンドを入力する
```shell
git clone [깃랩-저장소-ssh-住所]
```

git clone 成功