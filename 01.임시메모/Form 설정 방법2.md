### 날짜 :  2022-08-18 17:30

### 인덱스 :

### 태그 : #ec-cube, #costomize, #Form

----

### 메모 :

\\app\\Customize\\Form\\Extension\\CustomizeOrderType.php
```php
$values = array_map(function ($age) {
    return $age."代";
}, range(10, 90, 10));

$form->add('abcd', ChoiceType::class, [
    'choices' => array_combine($values, $values) + ["それ以上" => "それ以上db"],
    'placeholder' => '指定なし'
]);
```

\\app\\Customize\\Entity\\OrderTrait.php
```php
public function getAbcd()
{
	return null;
}
```

결과 화면
![[20220818-03.PNG]]

> 

----
### 출처 :
-


### 연결메모
-















```php

```

> 

----
### 출처 :
-


### 연결메모
-














