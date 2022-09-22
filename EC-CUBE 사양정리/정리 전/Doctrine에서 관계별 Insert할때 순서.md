### 날짜 :  2022-09-21 16:53

### 인덱스 :

### 태그 :

----

### 메모 :

관계도

상품상태<-상품
세일타입
<-상품클래스<-상품창고

<-주문상태
<-상품카테고리->카테고리

위의 관계를 글로 정리하면,

상품은 상품상태에 의존하고 있다. 
상품상태 1:N 상품 의 관계이다

상품클래스는 세일타입과 상품의 의존하고 있다.
세일타입 1:N 상품클래스
상품 1:N 상품클래스
즉, 상품클래스 안에 상품 정보와 세일타입 정보를 지니고 있다는 것이다.

상품창고는 상품클래스에 의존하고 있다.
상품클래스 1:N 상품창고

상품카테고리는 상품, 카테고리에 의존하고 있다.
상품 1:N 상품카테고리
카테고리 1:N 상품카테고리

---

ORM을 이용하여 데이터를 추가하려면

먼저 상품이 의존하고 있는 상품상태를 추가해주고
상품이 품고 있는 상품클래스와, 상품카테고리를 추가한다
```php
 $AnyProduct->setAnyProductStatus($AnyProductStatus);
 $AnyProduct->addAnyProductClass($AnyProductClass);
```

상품클래스의 경우 상품을 의존하고 있기에
```php
 $AnyProductClass->setAnyProduct($AnyProduct);
```
위와 같이 상품클래스에 상품 객체를 등록하게 되면 
```php
$this->entityManager->persist($AnyProduct);
$this->entityManager->flush();
```
상품만 등록하게되어도 자동적으로 상품클래스 등록도 등록하게 된다.

그런데 상품카테고리는 상품클래스 처럼 등록을 하려고 하면
에러가 발생한다.
![[Pasted image 20220922142817.png]]

상품카테고리 카테고리 엔티티를 보면 알수 있는데
product_id 와 category_id 를 키 필드로 사용하고 있다.

```php
class AnyProductCategory extends \Eccube\Entity\AbstractEntity
{
    /**
     * @var int
     *
     * @ORM\Column(name="any_product_id", type="integer", options={"unsigned":true})
     * @ORM\Id
     * @ORM\GeneratedValue(strategy="NONE")
     */
    private $any_product_id;

    /**
     * @var int
     *
     * @ORM\Column(name="any_category_id", type="integer", options={"unsigned":true})
     * @ORM\Id
     * @ORM\GeneratedValue(strategy="NONE")
     */
    private $any_category_id;
}
```

그런 이유에서 등록 순서가
상품 객체를 먼저 등록해주어야된다.

```php
$AnyProductCategory->setAnyProduct($AnyProduct);
$AnyProductCategory->setAnyProductId($AnyProduct->getId());
```

상품객체와 상품아이디도 다 등록해주어야된다.
상품아이디만 등록하면 이런 에러가 발생한다
![[Pasted image 20220922153618.png]]





----
### 출처 :
-


### 연결메모
-








