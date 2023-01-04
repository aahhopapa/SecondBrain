### 날짜 :  2022-08-27 09:13

### 인덱스 : [[3.1.5 Git]]

### 태그 : #Linux, #Git

----

### 메모 :
## .ignore 파일 만들기

### 리눅스 셀스크립트로 .ignore 파일 작성 하기

```shell
vim .gitignore
```
이제 [ 입력모드 ]로 들어가서 Git 에게 무시받을 정보(확장자, 폴더 등)를 입력해보자.
 [ i ] 누르면 입력모드가 된다.

ignore할 파일 혹은 폴더를 작성
-   ESC : 입력모드 나가기
-   :wq : 저장 후 나가기

작성한 ignore파일 확인하기
```shell
cat .gitignore
```



----
### 출처 :
- [리눅스 git .ignore 추가 ](https://gbsb.tistory.com/11).


### 연결메모
-

### 블로그 기록
- https://ahopapa.com/ko/git-ignore-%ed%8c%8c%ec%9d%bc-%eb%a7%8c%eb%93%a4%ea%b8%b0/


---

## 일본어

## .ignore ファイルの作成（Linux）​

### Linuxシェルスクリプトで.ignoreファイルを作成する
```shell
vim .gitignore
```

それでは、[入力モード]に入り、
Gitに無視される情報（拡張子、フォルダなど）を入力してみましょう。
[i]押すと入力モードになります。

***ESC         : 入力モードを終了する***
***:wq         : 保存して終了する***

作成したignoreファイルを確認する
```shell
cat .gitignore
```

---------

### 블로그 기록
- https://ahopapa.com/git-ignore-%e3%83%95%e3%82%a1%e3%82%a4%e3%83%ab-%e4%bd%9c%e6%88%90/