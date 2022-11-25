### 날짜 :  2022-09-15 19:33

### 인덱스 : [[3.1.3.5.1 Symfony]]

### 태그 : #Doctrine

----

### 메모 :

단순히 Anything이란 객체에 AnythingDetail객체를 만들어
한번에 insert하는 단순한 처리이다.

```php
/**
 * @Route("/doctrine/1", methods={"GET"})
 */
public function doctrineTest1()
{

    $Anything = new \Customize\Entity\Anything();
    $AnythingDetail_1 = new \Customize\Entity\AnythingDetail();
    $AnythingDetail_1->setAnyDetailInput('di_1'.$this->current);
    $AnythingDetail_1->setAnyDetailSelect('ds_1'.$this->current);
    
    $AnythingDetail_2 = new \Customize\Entity\AnythingDetail();
    $AnythingDetail_2->setAnyDetailInput('di_2'.$this->current);
    $AnythingDetail_2->setAnyDetailSelect('ds_2'.$this->current);
    
    $AnythingDetail_3 = new \Customize\Entity\AnythingDetail();
    $AnythingDetail_3->setAnyDetailInput('di_3'.$this->current);
    $AnythingDetail_3->setAnyDetailSelect('ds_3'.$this->current);

    $Anything->setAnyInput('ai'.$this->current);
    $Anything->setAnySelect('as'.$this->current);
    $Anything->addAnythingDetail($AnythingDetail_1);
    $Anything->addAnythingDetail($AnythingDetail_2);
    $Anything->addAnythingDetail($AnythingDetail_3);

    $this->entityManager->persist($Anything);
    $this->entityManager->flush();

    return new Response(
        '<html><body>doctrine test 1</body></html>'
    );
}
```

하지만 이렇게 실행하면 오류가 난다.
![[Doctrine에서 Entity정의 할때 cascade 사용.png]]


해결방법은 Anything.php 에서 AnythingDetail 과 관계 설정에서 cascade 를 추가 하면 된다.
> cascade={"persist", "remove"}

==cascade는 종속==이라는 의미이다.

Anything.php
```php
@ORM\OneToMany(targetEntity="Customize\Entity\AnythingDetail", mappedBy="Anything", cascade={"persist", "remove"})
```





> 

----
### 출처 :
-


### 연결메모
- [[Doctrine에서 관계별 Insert할때 순서]]








