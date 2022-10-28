### 날짜 :  2022-08-18 18:06

### 인덱스 :

### 태그 : #ec-cube, #costomize, #Form, #Extention

----

### 메모 :

흐름도
class_categories_as_json

\\src\\Eccube\\Twig\\Extension\\EccubeExtension.php
```php
/**
 * Get the ClassCategories as JSON.
 *
 * @param Product $Product
 *
 * @return string
 */
public function getClassCategoriesAsJson(Product $Product)
{
    $Product->_calc();
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
        $class_categories[$class_category_id1]['#'.$class_category_id2] = [
            'classcategory_id2' => $class_category_id2,
            'name' => $class_category_name2,
            'stock_find' => $ProductClass->getStockFind(),
            'price01' => $ProductClass->getPrice01() === null ? '' : number_format($ProductClass->getPrice01()),
            'price02' => number_format($ProductClass->getPrice02()),
            'price01_inc_tax' => $ProductClass->getPrice01() === null ? '' : number_format($ProductClass->getPrice01IncTax()),
            'price02_inc_tax' => number_format($ProductClass->getPrice02IncTax()),
            'price01_with_currency' => $ProductClass->getPrice01() === null ? '' : $this->getPriceFilter($ProductClass->getPrice01()),
            'price02_with_currency' => $this->getPriceFilter($ProductClass->getPrice02()),
            'price01_inc_tax_with_currency' => $ProductClass->getPrice01() === null ? '' : $this->getPriceFilter($ProductClass->getPrice01IncTax()),
            'price02_inc_tax_with_currency' => $this->getPriceFilter($ProductClass->getPrice02IncTax()),
            'product_class_id' => (string) $ProductClass->getId(),
            'product_code' => $ProductClass->getCode() === null ? '' : $ProductClass->getCode(),
            'sale_type' => (string) $ProductClass->getSaleType()->getId(),
        ];
    }

    return json_encode($class_categories);
}
```

\\src\\Eccube\\Twig\\Extension\\EccubeExtension.php
```php
new TwigFunction('class_categories_as_json', [$this, 'getClassCategoriesAsJson']),
```


\\src\\Eccube\\Resource\\template\\default\\Product\\list.twig
```js
eccube.productsClassCategories = {
    {% for Product in pagination %}
    "{{ Product.id|escape('js') }}": {{ class_categories_as_json(Product)|raw }}{% if loop.last == false %}, {% endif %}
    {% endfor %}
};
```


\\html\\template\\default\\assets\\js\\eccube.js
```js
if (eccube.hasOwnProperty('productsClassCategories')) {
    // 商品一覧時
    classcat2 = eccube.productsClassCategories[product_id][classcat_id1];
}
```


\\src\\Eccube\\Resource\\template\\default\\Product\\list.twig
```twig
{% if form.classcategory_id1 is defined %}
    <div class="ec-select">
        {{ form_widget(form.classcategory_id1) }}
        {{ form_errors(form.classcategory_id1) }}
    </div>
    {% if form.classcategory_id2 is defined %}
        <div class="ec-select">
            {{ form_widget(form.classcategory_id2) }}
            {{ form_errors(form.classcategory_id2) }}
        </div>
    {% endif %}
{% endif %}
```



----
### 출처 :
-


### 연결메모
-















```php

```

> 

----
### 출처 :
-


### 연결메모
-














