### 날짜 :  2022-08-04 09:06

### 인덱스 : [[3.1.3.5.1 Symfony]]

### 태그 : #ec-cube, #controller, #costomize, #GET


----

### 메모 :

```php

namespace Customize\Controller;

use Sensio\Bundle\FrameworkExtraBundle\Configuration\Method;
use Sensio\Bundle\FrameworkExtraBundle\Configuration\Route;
use Symfony\Component\HttpFoundation\Response;

use Sensio\Bundle\FrameworkExtraBundle\Configuration\Template;

class SamplePageController
{
    /**
     * @Method("GET")
     * @Route("/sample2")
     * @Template("Sample/index.twig")
     */
    public function testMethod2()
    {
        return ['contollerParam' => 'EC-CUBE'];
    }
}

```


```php

/**
 * @Method("GET")
 * @Route("/sample3/{id}", name="sample_page")
 */
public function testMethod3($id)
{
	return new Response('Parameter is '.$id);
}

```

여기서 중요한것은 twig에 url 메소드의 "sample_page"와 php의 testMethod3 메소드의
name값이 일치 해야한다는 것이다.

```twig
{# Sample/index.twig #}

{% set param_value = contollerParam %}


<h3>Hello  {{ param_value }}!</h3>

<a href="{{ url("sample_page", { id : 2}) }}">Sample3ページへのリンク</a>
```

이렇게 코드를 실행 해서 sample2로 이동후

![[Pasted image 20220804102510.png]]
링크에 id값이 2가 세팅 되어있다

링크를 클릭해서 이동하면 
화면에서 설정한 값이 GET메소드를 통해 컨트롤러로 설정된것을 알 수 있다.
![[Pasted image 20220804103157.png]]


----
### 출처 :
- https://doc4.ec-cube.net/customize_controller


### 연결메모
-[[컨트롤러 커스텀 확장하기 2]]














