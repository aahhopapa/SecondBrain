### 날짜 :  2022-08-24 09:48

### 인덱스 : [[3.1.3.5.1 Symfony]]

### 태그 : #ECCUBE, #costomize, #FormType


----

### 메모 :

\\app\\Customize\\Form\\StoreEntryType.php
```php
use Eccube\Form\Type\AddressType;
```
기존 EC-CUBE의 AddressType를 사용한다고 선언한다

```php
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
		])
		->add('address', AddressType::class);
}

```

AddressType을 빌더에 추가 한다
```php
    ->add('address', AddressType::class);
```


![[20220824-01.png]]


----
### 출처 :
-　https://symfony.com/doc/current/forms.html#building-forms


### 연결메모
-














