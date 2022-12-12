### 날짜 :  2022-12-12 11:00

### 인덱스 :

### 태그 :

<span style="color: red">강조</span> ==강조==

----

### 메모 :

### foreach 사용예제 1

```php
$array = array("1", "2", "3", "4", "5", "6", "7", "8", "9", "10");

foreach ($array as $arr) {
  dump($arr);
}
dump($array);
```

결과 :
dump($arr);
>"1" 
>"2" 
>. . .省略. . .
>"10" 
>}

dump($array);
>array (10) { 
>	[0]=> "1" 
>	[1]=> "2" 
>	. . .省略. . .
>	[9]=> "10" 
>}

### foreach 사용예제 2

```php
$array = array("1", "2", "3", "4", "5", "6", "7", "8", "9", "10");

foreach ($array as $key => $value) {
  echo "key: " . $key . "\n";
  echo "value: " . $array[$key] . "\n";
}
```

결과 :
>key: 0
>value: "1"
>key: 1
>value: "2"
>. . .省略. . .
>key: 9
>value: "10"
>


### foreach 사용예제 3

```php
$array = array("1", "2", "3", "4", "5", "6", "7", "8", "9", "10");
$index = 0;
foreach ($arr as $key => $val) {
  echo "index Value:".$index."\n";
  $index++;
}
```

결과 :
>index Value: 0
>index Value: 1
>index Value: 2
>. . .省略. . .
>index Value: 9



----
### 출처 :
- [key변수를 사용하여 PHP에서 foreach 인덱스 찾기](https://hyeon.pro/dev/php-foreach-%EC%9D%B8%EB%8D%B1%EC%8A%A4/#:~:text=foreach%20%EC%9D%B8%EB%8D%B1%EC%8A%A4%20%EC%B0%BE%EA%B8%B0-,key%20%EB%B3%80%EC%88%98%EB%A5%BC%20%EC%82%AC%EC%9A%A9%ED%95%98%EC%97%AC%20PHP%EC%97%90%EC%84%9C%20foreach%20%EC%9D%B8%EB%8D%B1%EC%8A%A4%20%EC%B0%BE%EA%B8%B0,%EB%8B%A4%EC%9D%8C%EA%B3%BC%20%EA%B0%99%EC%9D%B4%20%EC%82%AC%EC%9A%A9%EB%90%A9%EB%8B%88%EB%8B%A4.&text=%EB%B3%80%EC%88%98%20%EA%B0%92%EC%9D%80%20%EB%B0%B0%EC%97%B4%EC%9D%98%20%EA%B0%81%20%EC%9A%94%EC%86%8C%20%EA%B0%92%EC%9D%84%20%EC%A0%80%EC%9E%A5%ED%95%A9%EB%8B%88%EB%8B%A4.)


### 연결메모
-








