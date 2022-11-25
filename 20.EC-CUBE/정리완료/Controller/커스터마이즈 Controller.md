### 날짜 :  2022-08-17 14:13

### 인덱스 : [[3.1.3.5.1 Symfony]]

### 태그 : #ECCUBE, #controller, #costomize, #GET


----

### 메모 :

먼저 커스텀 컨트롤러 하나 만들자
app/Customize/Contoller/
StoreEntryController.php를 하나 만들고
```php
<?php

namespace Customize\Controller;

use Sensio\Bundle\FrameworkExtraBundle\Configuration\Method;
use Sensio\Bundle\FrameworkExtraBundle\Configuration\Route;
use Symfony\Component\HttpFoundation\Response;

use Sensio\Bundle\FrameworkExtraBundle\Configuration\Template;


class StoreEntryController
{

    /**
     * 店舗登録画面.
     * @Method("GET")
     * @Route("/store_entry")
     * @Template("StoreEntry/index.twig")
     */
    public function testMethod()
    {
        return [];
    }

}

```

app/template/default 에서 
(.env 파일에 ECCUBE_TEMPLATE_CODE=default로 되어있는경우 default가 기본 폴더 경로가 됨)
StoreEntry 폴더를 만들어주고 거기다가 index.twig를 만들어준다

```twig
{# index.twig #}

<h1>店舗登録画面</h1>
```

실행하는데 화면에 적용이 안될경우
CMD를 열어서 
프록시와 캐시 클리어 커맨드를 실행해준다
>Proxyの生成
>php C:\xampp\htdocs\ec-cube\bin\console eccube:generate:proxies

>キャッシュクリア
>php C:\xampp\htdocs\ec-cube\bin\console cache:clear --no-warmup

다시 브라우저를 통해서 확인해보면 잘나오는걸 확인 할수있다
![[20220817-02.png]]



----
### 출처 :
-


### 연결메모
- [[EC-CUBE 회원 등록화면 기존 소스]]














