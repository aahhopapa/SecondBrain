### 날짜 :  2022-10-11 10:26

### 인덱스 : [[3.1.3.5.1 Symfony]]

### 태그 :

----

### 메모 :

관리 화면의 메뉴는 eccube_nav.yaml 에서 정의하고 있다.

app\\config\\eccube\\packages\\eccube_nav.yaml
```yaml
parameters:
    eccube_nav:
```

위의 코드에서 알수 있듯이 eccube_nav: 밑에 정의 되있는 파라미터가
메뉴가 된다.

파라미터에 정의된 순서대로 표시되기에 원하는 위치에 새로 추가할 메뉴를 적어주자
```yaml
parameters:
    eccube_nav:
    #
    # 생략
    #
        banner:
            name: admin.banner.banner_management
            icon: fa-file-image-o
            children:
                banner_master:
                    name: admin.banner.banner_list
                    url: admin_banner
                banner_edit:
                    name: admin.banner.banner_registration
                    url: admin_banner_new
```
배너라는 메뉴를 추가해 주었다.

다음에는 화면에 출력할 라벨을 설정하기 위해 messges.ja.yaml 을 만들어준다.
app\\Customize\\Resource\\locale\\messages.ja.yaml

```yaml
#------------------------------------------------------------------------------------
# バナー
#------------------------------------------------------------------------------------
admin.banner.banner_management: バナー管理
admin.banner.banner_list: バナー 一覧
admin.banner.banner_registration: バナー登録

```

이렇게 추가 해주면 메뉴를 표시할 기본적인 셋팅은 마쳤다.
마지막으로 컨트롤러와 twig만 만들면 관리화면에 추가하는것은 끝이다.

app\\Customize\\Controller\\Admin\\Banner\\BannerAdminController.php
```php
<?php

namespace Customize\Controller\Admin\Banner;

use Eccube\Controller\AbstractController;
use Eccube\Event\EventArgs;
use Knp\Component\Pager\Paginator;
use Sensio\Bundle\FrameworkExtraBundle\Configuration\Template;
use Symfony\Component\HttpFoundation\Request;
use Symfony\Component\HttpKernel\Exception\BadRequestHttpException;
use Symfony\Component\HttpKernel\Exception\NotFoundHttpException;
use Symfony\Component\Routing\Annotation\Route;
use Symfony\Component\Security\Http\Authentication\AuthenticationUtils;
use Symfony\Component\Security\Core\Authentication\Token\Storage\TokenStorageInterface;
use Symfony\Component\Security\Core\Encoder\EncoderFactoryInterface;


class BannerAdminController extends AbstractController
{
    /**
     * ▼　　／
     *
     * @Route("/%eccube_admin_route%/banner", name="admin_banner")
     * @Template("@admin/Banner/index.twig")
     */
    public function index(Request $request)
    {
        //$Shopstores = $this->bannerRepository->findBy([], ['id' => 'DESC']);

        $builder = $this->formFactory->createBuilder();

        $event = new EventArgs(
            [
                'builder' => $builder,
                // 'Shopstores' => $Shopstores,
            ],
            $request
        );
        
        $form = $builder->getForm();

        return [
            'form' => $form->createView()
        ];
    }
}
```

\\app\\template\\admin\\Banner\\index.twig
```twig
{% extends '@admin/default_frame.twig' %}

{% set menus = ['banner', 'banner_master'] %}

{% block title %}{{ 'admin.banner.banner_list'|trans }}{% endblock %}
{% block sub_title %}{{ 'admin.banner.banner_management'|trans }}{% endblock %}

{% form_theme form 'Form/bootstrap_4_layout.html.twig' %}

{% block main %}
    <div class="c-contentsArea__cols">
        <div class="c-contentsArea__primaryCol">
            <div class="c-primaryCol">
                <div class="card rounded border-0 mb-4">
                    <div class="card-body p-0">
                        <form name="form1" id="form1" method="post" action="">
                            <table class="table table-sm">
                                <thead>
                                <tr>
                                </tr>
                                </thead>
                                <tbody>
                                </tbody>
                            </table>
                        </form>
                    </div>
                </div>
            </div>
        </div>
    </div>
{% endblock %}


```

Twig에 추가한 set 파라미터와 eccube_nav.yaml 에 추가해준 Children의 파라메터 명과 일치하는것을
확인 해야한다.

\\app\\template\\admin\\Banner\\index.twig
```twig
{% set menus = ['banner', 'banner_master'] %}
```

app\\config\\eccube\\packages\\eccube_nav.yaml
```yaml
#
# 생략
#
children:
	banner_master:
		name: admin.banner.banner_list
		url: admin_banner
	banner_edit:
		name: admin.banner.banner_registration
		url: admin_banner_new
```

화면에 출력 한 결과

![[Pasted image 20221011105644.png]]




----
### 출처 :
-


### 연결메모
-








