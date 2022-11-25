### 날짜 :  2022-09-12 13:38

### 인덱스 : [[3.1.3.5.1 Symfony]]

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

where 구문안에 넣어주면 된다.
> $qb->expr()->orX( 조건1 , 조건2 ))

----
### 출처 :
-


### 연결메모
- [[Doctrine에서 where문에 in 넣는 법]]








