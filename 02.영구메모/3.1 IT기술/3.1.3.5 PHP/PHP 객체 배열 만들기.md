### 날짜 :  2022-12-12 11:00

### 인덱스 :

### 태그 :

<span style="color: red">강조</span> ==강조==

----

### 메모 :

### 객체 배열 만들는 방법 1

```php
$x = (object) [
	'a' => 'test', 
	'b' => 'test2', 
	'c' => 'test3'
];
```

결과 :
>object(stdClass)#1 (3) { 
>	["a"]=> string(4) "test" 
>	["b"]=> string(5) "test2" 
>	["c"]=> string(5) "test3" 
>}


### 객체 배열 만들는 방법 2

```php
$object = new stdClass(); 
$object->property = 'Here we go';
```

결과 :
> object(stdClass)#2 (1) { 
> 	["property"]=> string(10) "Here we go" 
> }


### 객체 배열 만들는 방법 3

person 객체 만들기
```php
class Person
{
    public $name;
    public $age;
    
    function  birthday($age){
    	$age = $age + 1;
        return $age;
    }
}

$person1 = new Person();
$person1->name = 'David';
$person1->age = '23';

$person2 = new Person();
$person2->name = 'Nuno';
$person2->age = '21';
$person2->age = $person2->birthday($person2->age);
```

person 객체 어레이 추가
```php
$person_array = array();
$person_array[] = $person1;
$person_array[] = $person2;
```


----
### 출처 :
- [Php 객체 배열 만들기](https://ko.code-paper.com/php/examples-php-create-object-array)


### 연결메모
-








