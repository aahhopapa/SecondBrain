### 날짜 :  2022-09-12 13:38

### 인덱스 :

### 태그 : #Doctrine

----

### 메모 :

isset()메소드는 배열의 키값이 있는지 확인한다.
아래의 경우 $searchData { 'sale_type' : "123" } 배열에 123의 값을 가진 sale_type 가 있으므로
true를 반환하게 된다.
```php
isset($searchData['sale_type'])
```


OrderRepositoryExtension.php
```php
if (isset($searchData['sale_type']) && $salecount = count($searchData['sale_type'])) {
    $SaleType = $searchData['sale_type'];
    if ($SaleType) {
        $qb
        ->andWhere($qb->expr()->in('pc.SaleType', ':SaleType'))
        ->setParameter('SaleType', $SaleType);
    }
}
```



----
### 출처 :
-


### 연결메모
-








