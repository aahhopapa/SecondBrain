### 날짜 :  2022-09-12 13:38

### 인덱스 : [[3.1.3.5.1 Symfony]]

### 태그 : #Doctrine

----

### 메모 :

isset() 메소드는 배열의 키값이 있는지 확인한다.
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

리포지토리에서 in 구문쓴 Doctrine SQL 쿼리 작성법

ShopStoreRepository.php
```php
    public function getQueryBuilderByStoreNumber($searchData)
    {
        $qb = $this->createQueryBuilder('s')
        ->select('s');
        
        $qb
        ->andWhere($qb->expr()->in('s.number', ':number'))
        ->andWhere($qb->expr()->in('s.Group', ':group_id'))
        ->setParameter('number', $searchData['number'])
        ->setParameter('group_id', $searchData['group_id']);
        $query = $qb->getQuery();
        $result = $query->getResult();
        return $result;
    }
```

위에 작성한 리포지토리 메소드의 파라메터를 넣어 전달한다.
CustomizeOrderType.php
```php
$ShopStores = $this->shopStoreRepository->getQueryBuilderByStoreNumber([
    'number' => $preShopStoreNumberArray,
    'group_id' => $groupIdArray
]);
```

----
### 출처 :
-


### 연결메모
- [[PHP isset, empty, is_null 차이점]]
- [[Doctrine에서 Entity정의 할때 cascade 사용]]








