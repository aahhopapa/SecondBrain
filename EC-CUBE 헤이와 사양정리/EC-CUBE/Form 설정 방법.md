### 날짜 :  2022-08-18 14:08

### 인덱스 :

### 태그 : #ec-cube, #costomize, #Form

----

### 메모 :


\\app\\Customize\\Form\\Extension\\CustomizeOrderType.php
```php
$form->add('store_address', ChoiceType::class, [
            'choices' => $ShopStores,
            'choice_label' => "shopStoress",
            'required' => false,
            'placeholder' => false,
            'mapped' => false,
        ]);
```


> 'choice_label' => "shopStoress",

여기서 초이스라벨은 엔티티의 이름과 연결된다

\\app\\Customize\\Entity\\ShopStore.php
```php
/**
 * getShopStore 
 * Form Typeに使われるメソッド
 *
 * @return string
 */
public function getShopStoress()
{
	return $this->getName().'add moji'.;
}

```

여기서 getName() 이외에도 셀렉트박스에 출력하고 싶은 글로 수정하면 된다

----

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
![[20220818-03.png]]

----
### 출처 :
-　http://a-zumi.net/ec-cube4-craueformflowbundle/


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














