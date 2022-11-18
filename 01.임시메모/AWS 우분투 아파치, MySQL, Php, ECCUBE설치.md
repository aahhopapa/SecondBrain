### 날짜 :  2022-11-17 11:46

### 인덱스 :

### 태그 :

<span style="color: red">강조</span>

----

### 메모 :

### AWS 우분투 인스턴스생성


### AWS 인바운드 포트열기
https://juju-coding.tistory.com/25

### Ubuntu 20.04에 Apache2, Mysql, PHP 설치
https://t-okk.tistory.com/153

### Mysql 설정

[Failed! Error: SET PASSWORD ... が出る。mysql_secure_installationでrootパスワードを設定できない。 - 技術的な何か。 (level69.net)](https://level69.net/archives/30666)

https://m.blog.naver.com/software705/221337666338
https://blogshine.tistory.com/322

루트계정 권한부여
https://1mini2.tistory.com/87
접속 안될시 해결책 - 
mysql 재시작 (우분투 명령어)
>  service mysql restart

### ECCUBE설치
[ECCUBE 설치 참고 사이트](https://self-development.info/%E3%82%AA%E3%83%BC%E3%83%97%E3%83%B3%E3%82%BD%E3%83%BC%E3%82%B9%E3%81%AEec%E3%82%B5%E3%82%A4%E3%83%88%E3%81%A7%E3%81%82%E3%82%8Bec-cube%E3%81%AE%E3%82%A4%E3%83%B3%E3%82%B9%E3%83%88%E3%83%BC%E3%83%AB/)

ECCUBE다운로드
> wget https://downloads.ec-cube.net/src/eccube-4.1.0.zip


루트 권한자로 변경
> sudo su

압축풀기
> unzip eccube-4.1.0.zip

재시작
> sudo reboot

ec-cube 필요 라이버러리 설치
> sudo apt install -y php-pdo-pgsql
> sudo a2enmod rewrite

아파치 재시작
> sudo systemctl restart apache2


----
### 출처 :
-


### 연결메모
-








