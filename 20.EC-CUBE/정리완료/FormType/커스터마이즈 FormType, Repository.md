### 날짜 :  2022-08-18 09:48

### 인덱스 : [[3.1.3.5.1 Symfony]]

### 태그 : #ECCUBE, #costomize, #FormType


----

### 메모 :
폼타입을 만들어보자
폼 커스터 마이즈는 기존 폼을 확장하는 방법과 새로 만드는 방법이 있다
이번에는 새로 만드는 방법으로 해보겠다

\\app\\Customize\\Form\\StoreEntryType.php
```php
<?php

namespace Customize\Form;

use Eccube\Common\EccubeConfig;
use Symfony\Component\Form\AbstractType;
use Symfony\Component\Form\Extension\Core\Type\TextType;
use Symfony\Component\Form\FormBuilderInterface;
use Symfony\Component\OptionsResolver\OptionsResolver;
use Symfony\Component\Validator\Constraints as Assert;

class StoreEntryType extends AbstractType
{
    /**
     * @var EccubeConfig
     */
    protected $eccubeConfig;

    /**
     * @param EccubeConfig $eccubeConfig
     */
    public function __construct(EccubeConfig $eccubeConfig)
    {
        $this->eccubeConfig = $eccubeConfig;
    }

    /**
     * {@inheritdoc}
     */
    public function buildForm(FormBuilderInterface $builder, array $options)
    {
        $builder
            ->add('name', TextType::class, [
                'required' => false,
                'constraints' => [
                    new Assert\Length([
                        'max' => $this->eccubeConfig['eccube_stext_len'],
                    ]),
                ],
            ]);
    }

}

```


>eccubeConfig['eccube_stext_len']

코드 중에 설정파일은
\\app\\config\\eccube\\packages\\eccube.yaml 에서 설정 가능


리포지토리에서 폼에 새롭게 추가할 함수도 하나 만들어주자
\\app\\Customize\\Repository\\StoreEntryRepository.php
```php
public function newStore()
{
	$Store = new \Customize\Entity\StoreEntry();
	return $Store;
}
```

폼과 리포지토리를 맞추었으니
컨트롤러를 새롭게 수정해주자

```php
<?php

namespace Customize\Controller;

use Sensio\Bundle\FrameworkExtraBundle\Configuration\Method;
use Sensio\Bundle\FrameworkExtraBundle\Configuration\Route;
use Symfony\Component\HttpFoundation\Response;

use Sensio\Bundle\FrameworkExtraBundle\Configuration\Template;

use Eccube\Controller\AbstractController;
use Customize\Form\StoreEntryType;
use Customize\Repository\StoreEntryRepository;


class StoreEntryController extends AbstractController
{

    /**
     * @var StoreEntryRepository
     */
    protected $storeEntryRepository;

    /**
     * EntryController constructor.
     *
     * @param StoreEntryRepository $storeEntryRepository
     */
    public function __construct(
        StoreEntryRepository $storeEntryRepository
    ) {
        $this->storeEntryRepository = $storeEntryRepository;
    }

    /**
     * 店舗登録画面.
     * @Method("GET")
     * @Route("/store_entry", name="store_entry", methods={"GET", "POST"})
     * @Template("StoreEntry/index.twig")
     */
    public function testMethod()
    {
        $Store = $this->storeEntryRepository->newStore();

        /* @var $builder \Symfony\Component\Form\FormBuilderInterface */
        $builder = $this->formFactory->createBuilder(StoreEntryType::class, $Store);

        /* @var $form \Symfony\Component\Form\FormInterface */
        $form = $builder->getForm();

        return  [
            'form' => $form->createView(),
        ];
    }

}

```

마지막으로 twig도 수정해주면 된다
```twig
{# index.twig #}
{% extends 'default_frame.twig' %}

{% set body_class = 'registration_page' %}

{#
{% form_theme form 'Form/form_div_layout.twig' %}
#}

{% block javascript %}
    <script src="//yubinbango.github.io/yubinbango/yubinbango.js" charset="UTF-8"></script>
{% endblock javascript %} 

{% block main %}
    <div class="ec-registerRole">
        <div class="ec-pageHeader">
            <h1>{{ '店舗登録画面'|trans }}</h1>
        </div>
        <div class="ec-off1Grid">
            <form method="post" action="{{ url('store_entry') }}" novalidate class="h-adr">
                <div class="ec-borderedDefs">
                    <dl>
                        <dt>
                            {{ form_label(form.name, '店舗名', { 'label_attr': { 'class': 'ec-label' }}) }}
                        </dt>
                        <dd>
                            <div class="ec-halfInput{{ has_errors(form.name) ? ' error' }}">
                                {{ form_widget(form.name) }}
                                {{ form_errors(form.name) }}
                            </div>
                        </dd>
                    </dl>
                </div>
            </form>
        </div>
    </div>
{% endblock %}
```

이렇게 다 수정했다면
새로운 폼이 설정된 화면이 출력될것이다
![[20220818-02.PNG]]


----
### 출처 :
-　https://symfony.com/doc/current/forms.html#building-forms


### 연결메모
-














