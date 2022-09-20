### 날짜 :  2022-09-12 13:38

### 인덱스 :

### 태그 : #Doctrine

----

### 메모 :


ProductRepositoryExtension.php
```php
if (!empty($searchData['group_id']) && $searchData['group_id']) {
    $qb
        ->leftJoin('p.ProductGroup', 'psg')
        ->andwhere(
            $qb->expr()->orX(
                $qb->expr()->isNull('psg.Group')
                ,
                $qb->expr()->eq('psg.Group',':group_id')
                )
            )
        ->setParameter('group_id', $searchData['group_id']);
}
```



----
### 출처 :
-


### 연결메모
-








