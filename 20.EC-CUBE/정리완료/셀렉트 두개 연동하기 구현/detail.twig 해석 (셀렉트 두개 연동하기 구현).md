### 날짜 :  2022-09-14 14:19

### 인덱스 : [[3.1.3.5.1 Symfony]]

### 태그 : #ECCUBE

----

### 메모 :

하려고 하는 작업은 첫번째 셀렉트박스를 선택하면
그것과 연관된 데이터로 구성된 두번째 셀렉트박스가 만들어진다.
![[셀렉트문 두개 구현.png]]

처음에는 비동기 통신으로 구현하는줄 알았으나
EC-CUBE의 소스를 보니 비동기 통신이 아닌 셀렉트박스 정보가 담긴 
다차원배열로 만들어진 데이터를 Json으로 뿌려주는 역활만 하고 있었다.

기존 EC-CUBE의 detail.twig화면에 만들어진것을 해석하였다.



ProductRepository.php
```php
/**
 * Find the Product with sorted ClassCategories.
 *
 * @param integer $productId
 *
 * @return Product
 */
public function findWithSortedClassCategories($productId)
{
    $qb = $this->createQueryBuilder('p');
    $qb->addSelect(['pc', 'cc1', 'cc2', 'pi', 'pt'])
        ->innerJoin('p.ProductClasses', 'pc')
        ->leftJoin('pc.ClassCategory1', 'cc1')
        ->leftJoin('pc.ClassCategory2', 'cc2')
        ->leftJoin('p.ProductImage', 'pi')
        ->leftJoin('p.ProductTag', 'pt')
        ->where('p.id = :id')
        ->andWhere('pc.visible = :visible')
        ->setParameter('id', $productId)
        ->setParameter('visible', true)
        ->orderBy('cc1.sort_no', 'DESC')
        ->addOrderBy('cc2.sort_no', 'DESC');

    $product = $qb
        ->getQuery()
        ->getSingleResult();

    return $product;
}
```


EccubeExtension.php
```php
/**
 * product_idで指定したProductを取得
 * Productが取得できない場合、または非公開の場合、商品情報は表示させない。
 * デバッグ環境以外ではProductが取得できなくでもエラー画面は表示させず無視される。
 *
 * @param $id
 *
 * @return Product|null
 */
public function getProduct($id)
{
    try {
        $Product = $this->productRepository->findWithSortedClassCategories($id);

        if ($Product->getStatus()->getId() == ProductStatus::DISPLAY_SHOW) {
            return $Product;
        }
    } catch (\Exception $e) {
        return null;
    }

    return null;
}
```

셀렉트 박스의 초기값을 설정하는 폼이다.
AddCartType.php
```php
public function buildForm(FormBuilderInterface $builder, array $options)
{
/* @var $Product \Eccube\Entity\Product */
$Product = $options['product'];
$this->Product = $Product;
$ProductClasses = $Product->getProductClasses();

	if ($Product && $Product->getProductClasses()) {
	    if (!is_null($Product->getClassName1())) {
	        $builder->add('classcategory_id1', ChoiceType::class, [
	            'label' => $Product->getClassName1(),
	            'choices' => ['common.select' => '__unselected'] + $Product->getClassCategories1AsFlip(),
	            'mapped' => false,
	        ]);
	    }
	    if (!is_null($Product->getClassName2())) {
	        $builder->add('classcategory_id2', ChoiceType::class, [
	            'label' => $Product->getClassName2(),
	            'choices' => ['common.select' => '__unselected'],
	            'mapped' => false,
	        ]);
	    }
	}
}
```
코드를 살펴보면 두번째 셀렉트박스에는 unselected 만 설정하고 있음을 알수있다.
즉 두번째 셀렉트 박스의 값은 다른 곳에서 처리 한다.

ProductController.php
```php

/**
 * 商品詳細画面.
 *
 * @Route("/products/detail/{id}", name="product_detail", methods={"GET"}, requirements={"id" = "\d+"})
 * @Template("Product/detail.twig")
 * @ParamConverter("Product", options={"repository_method" = "findWithSortedClassCategories"})
 *
 * @param Request $request
 * @param Product $Product
 *
 * @return array
 */
 
 public function detail(Request $request, Product $Product)
{

    $builder = $this->formFactory->createNamedBuilder(
    '',
    AddCartType::class,
    null,
    [
        'product' => $Product,
        'id_add_product_id' => false,
    ]);

    return [
	    'form' => $builder->getForm()->createView(),
	    'Product' => $Product,
	];
}



```

컨트롤러를 보면
```php
@ParamConverter("Product", options={"repository_method" = "findWithSortedClassCategories"})
```
어노테이션 ParamConverter를 이용해 product_id를 Product객체로 변경하는 처리를 하여 컨트롤러에 전달하고 있었다.


eccube.js
```js
(function(window, undefined) {

    // 名前空間の重複を防ぐ
    if (window.eccube === undefined) {
        window.eccube = {};
    }

    var eccube = window.eccube;
    // グローバルに使用できるようにする
    window.eccube = eccube;

})(window);
```


default_frame.twig
```html
<script src="{{ asset('assets/js/eccube.js') }}"></script>
```

detail.twig
```js
eccube.classCategories = {{ class_categories_as_json(Product)|raw }};
```

여기 detail.twig에서  __eccube. 는 default_frame.twig 에서 eccube.js를 정의하고 있고 eccube.js 는 「グローバルに使用できる」라고 적혀있는것 처럼
eccube는 어디서든 사용할수 있도록 상수로 지정된것을 알수있다

detail.twig 에서 __{{ class_categories_as_json(Product)|raw }}__ 는 어디서 설정하는지 찾아 보면 EccubeExtension.php 파일에서 지정 하고 있음을 알수 있다.

EccubeExtension.php
```php
use Twig\Extension\AbstractExtension;

public function getFunctions()
{
return [
	new TwigFunction('class_categories_as_json', [$this, 'getClassCategoriesAsJson']),
	];
}
```
Twig의 익스텐션 기능을 이용해서 class_categories_as_json 함수를 정의 해서 
detail.twig에서 사용하고 있는 것이였다.
> use Twig\Extension\AbstractExtension;

EccubeExtension에서 정의한 함수는 getClassCategoriesAsJson 메소드에서 실제 구현되고 있다.

실제 구현되고 있는 코드를 보면 이렇다.
EccubeExtension.php
```php
public function getClassCategoriesAsJson(Product $Product)
{
	$class_categories = [
		'__unselected' => [
			'__unselected' => [
				'name' => trans('common.select'),
				'product_class_id' => '',
			],
		],
	];

	foreach ($Product->getProductClasses() as $ProductClass) {
		/** @var ProductClass $ProductClass */
		if (!$ProductClass->isVisible()) {
			continue;
		}
		/* @var $ProductClass \Eccube\Entity\ProductClass */
		$ClassCategory1 = $ProductClass->getClassCategory1();
		$ClassCategory2 = $ProductClass->getClassCategory2();
		if ($ClassCategory2 && !$ClassCategory2->isVisible()) {
			continue;
		}
		$class_category_id1 = $ClassCategory1 ? (string) $ClassCategory1->getId() : '__unselected2';
		$class_category_id2 = $ClassCategory2 ? (string) $ClassCategory2->getId() : '';
		$class_category_name2 = $ClassCategory2 ? $ClassCategory2->getName().($ProductClass->getStockFind() ? '' : trans('front.product.out_of_stock_label')) : '';
		

		$class_categories[$class_category_id1]['#'] = [
			'classcategory_id2' => '',
			'name' => trans('common.select'),
			'product_class_id' => '',
		];
		$class_categories[$class_category_id1]['###'.$class_category_id2] = [
			'classcategory_id2' => $class_category_id2,
			'name' => $class_category_name2,
		];
	}

	return json_encode($class_categories);
}
```

AddCartType에서 설정하지 않은 셀렉트박스2의 값은 EccubeExtension에서 설정하여
json값으로 넘기고 있었다.

foreach문을 통해 아래와 같은 2차배열을 만들어서 
셀렉트박스1의 데이터 안에 셀렉트박스2 데이터들을 넣은것을 알수 있다.
```php
$class_categories[$class_category_id1]['#'] 
```

```php
$class_categories[$class_category_id1]['###'.$class_category_id2]
```

![[셀렉트문 두개 구현2.png]]

즉, AddCartType에서 설정한 셀렉트박스1의 값, EccubeExtension에서 설정한 셀렉트박스1,2 의 값
이렇게 두곳에서 초기에는 가지고 있는 것을 알게되었다.
이후, 화면에서 셀렉트박스1이 선택되면 JS를 통해 json으로 접근하여 EccubeExtension에서 설정한 셀렉트박스2의 값을 읽어 오고 있었다.


실제 실행 JS코드는  eccube.js에 실현되어 있다.

eccube.js
```js
/**
 * Initialize.
 */
$(function() {
    // 規格1選択時
	$('select[name=classcategory_id1]')
	.change(function() {
		var $form = $(this).parents('form');
		var product_id = $form.find('input[name=product_id]').val();
		var $sele1 = $(this);
		var $sele2 = $form.find('select[name=classcategory_id2]');
		// 規格1のみの場合
		if (!$sele2.length) {
			//eccube.checkStock($form, product_id, $sele1.val(), null);
			// 規格2ありの場合
		} else {
			eccube.setClassCategories($form, product_id, $sele1, $sele2);
		}
	});
	
	// 規格2選択時
	$('select[name=classcategory_id2]')
	.change(function() {
		var $form = $(this).parents('form');
		var product_id = $form.find('input[name=product_id]').val();
		var $sele1 = $form.find('select[name=classcategory_id1]');
		var $sele2 = $(this);
		//eccube.checkStock($form, product_id, $sele1.val(), $sele2.val());
	});
});
```

「規格2ありの場合」로 else문으로 들어가서 클래스카테고리들을 세팅하는 메소드를 부르고있다.

eccube.js
```js
/**
 * 規格2のプルダウンを設定する.
 */
eccube.setClassCategories = function($form, product_id, $sele1, $sele2, selected_id2) {
    if ($sele1 && $sele1.length) {
        var classcat_id1 = $sele1.val() ? $sele1.val() : '';
        if ($sele2 && $sele2.length) {
            // 規格2の選択肢をクリア
            $sele2.children().remove();

            var classcat2;

            if (eccube.hasOwnProperty('productsClassCategories')) {
                // 商品一覧時
                classcat2 = eccube.productsClassCategories[product_id][classcat_id1];
            } else {
                // 詳細表示時
                classcat2 = eccube.classCategories[classcat_id1];
            }

            // 規格2の要素を設定
            for (var key in classcat2) {
                if (classcat2.hasOwnProperty(key)) {
                    var id = classcat2[key].classcategory_id2;
                    var name = classcat2[key].name;
                    var option = $('<option />').val(id ? id : '').text(name);
                    if (id === selected_id2) {
                        option.attr('selected', true);
                    }
                    $sele2.append(option);
                }
            }
        }
    }
};
```

셀렉트박스1이 변경될때 마다 
// 規格2の選択肢をクリア
셀렉트박스2 값들을 클리어 시킨다

그 다음
else문 // 詳細表示時 으로 들어가
detail.twig 제일 첫 구문의 eccube.classCategories 에서 설정한 값이  셋팅된다.

detail.twig
```html
<div class="ec-productRole__actions">
	<div class="ec-select">
	    {{ form_widget(form.classcategory_id1) }}
	    {{ form_errors(form.classcategory_id1) }}
	</div>
	<div class="ec-select">
	    {{ form_widget(form.classcategory_id2) }}
	    {{ form_errors(form.classcategory_id2) }}
	</div>
</div>
```



----
### 요약





----
### 출처 :
-


### 연결메모
-








