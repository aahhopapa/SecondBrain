### 날짜 :  2022-12-27 13:12

### 인덱스 :

### 태그 :

<span style="color: red">강조</span> ==강조==

----

### 메모 :

Windows xampp
```bash
Proxyの生成
php C:\xampp\htdocs\heiwado-ori\bin\console eccube:generate:proxies

1.キャッシュクリア
php C:\xampp\htdocs\heiwado-ori\bin\console cache:clear --no-warmup

2.SQL確認
php C:\xampp\htdocs\heiwado\bin\console eccube:schema:update --dump-sql

3.実行
php C:\xampp\htdocs\heiwado-ori\bin\console eccube:schema:update --dump-sql --force --no-proxy
php C:\xampp\htdocs\ec-cube\bin\console eccube:schema:update --dump-sql --force
```

Linux
```bash
Proxyの生成
sudo php /var/www/html/ec-cube/bin/console eccube:generate:proxies
キャッシュクリア
sudo php /var/www/html/ec-cube/bin/console cache:clear --no-warmup
SQL実行
sudo php /var/www/html/ec-cube/bin/console eccube:schema:update --dump-sql
sudo php /var/www/html/ec-cube/bin/console eccube:schema:update --dump-sql --force
```


----
### 출처 :
-


### 연결메모
-








