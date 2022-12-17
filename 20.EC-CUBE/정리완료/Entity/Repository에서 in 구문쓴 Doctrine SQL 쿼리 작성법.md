### 날짜 :  2022-12-13 11:38

### 인덱스 : [[3.1.3.5.1 Symfony]]

### 태그 : #Doctrine

----

### 메모 :

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








