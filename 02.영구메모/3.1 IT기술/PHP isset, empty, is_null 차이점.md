### 날짜 :  2022-10-24 10:49

### 인덱스 : [[3.1.3.5 PHP]]

### 태그 : 

----

### 메모 :


| 값 | if($var) | isset | empty | is_null |
|------|---|---|---|---|
|$var=1|true|true|false|false|
|$var="";|false|true|true|false|
|$var="0";|false|true|true|false|
|$var=0;|false|true|true|false|
|$var=NULL;|false|false|true|true|
|$var|false|false|true|true|
|$var=array()|false|true|true|false|
|$var=array(1)|true|true|false|false|

----
### 출처 :
- https://qiita.com/shinichi-takii/items/00aed26f96cf6bb3fe62


### 연결메모
-








