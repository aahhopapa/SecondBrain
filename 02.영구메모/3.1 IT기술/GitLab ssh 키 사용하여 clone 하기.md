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





