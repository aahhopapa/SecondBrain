### 날짜 :  2022-11-18 13:24

### 인덱스 :

### 태그 : #aahhopapa

<span style="color: red">강조</span>

----

### 메모 :

우분투일 결우 설정파일이 해당 폴더에 존재한다
> cd /etc/apache2/

conf파일 수정
>  sudo vi apache2.conf

AllowOverride가 None이므로 All로 설정
```shell
<Directory />
        Options FollowSymLinks
        AllowOverride All
        Require all denied
</Directory>

<Directory /usr/share>
        AllowOverride All
        Require all granted
</Directory>

<Directory /var/www/>
        Options Indexes FollowSymLinks
        AllowOverride All
        Require all granted
</Directory>
```

디렉토리 태그의 AllowOverride를 전부 다 All로 변경해준다
> AllowOverride None -> AllowOverride All

ECCUBE폴더로 이동
>  cd /var/www/html/

htacess파일을 수정해준다
> sudo vi .htaccess

 "RewriteEngine On" 바로 아래에 "RewriteBase /"를 추가한다.
> RewriteBase /

```shell
<IfModule mod_rewrite.c>
    #403 Forbidden対応方法
    #ページアクセスできない時シンボリックリンクが有効になっていない可能性あります、
    #オプションを追加してください
    #Options +FollowSymLinks +SymLinksIfOwnerMatch

    RewriteEngine On
    RewriteBase /
    # Acceptヘッダがimage/webpを含む場合
    RewriteCond %{HTTP_ACCEPT} image/webp

. . . 생략 . . .

```

----
### 출처 :
- https://teratail.com/questions/146235
- https://techmemo.biz/ec-cube/url-removal-index-php/

### 연결메모
-








