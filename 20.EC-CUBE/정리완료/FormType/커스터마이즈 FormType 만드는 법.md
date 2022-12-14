### 날짜 :  2022-08-25 09:04

### 인덱스 : [[3.1.3.5.1 Symfony]]

### 태그 : #Form

----

### 메모 :

## 커스터마이즈 FormType 만들기

해당 코드는 심포니 공식문서에 나오는 __PostalAddressType__ 을 예제를 참고 하였다.

먼저 __PostalAddressType__ 클래스를 만들고 __buildForm()__ 와 __configureOptions()__ 을 작성한다
__configureOptions()__ 은 타입의 옵션을 Resolve하는 메소드 이다
```php
class PostalAddressType extends AbstractType
{
	public function buildForm(FormBuilderInterface $builder, array $options): void {
		. . .
	}

	public function configureOptions(OptionsResolver $resolver): void {
		. . .
	}
}
```

 __configureOptions()__ 에서  새롭게 만들 폼의 옵션을 디폴트에 정의 해주자.
 해당 코드에서는 __allowed_states__ 와 __is_extended_address__ 라는 폼 옵션을 추가 했다.
```php
$resolver->setDefaults([
    'allowed_states' => null,
    'is_extended_address' => false,
]);

```

추가한 옵션을 __buildForm()__ 에서 사용하기 위해서 아래의 코드와 같이 
옵션 어레이에 __configureOptions()__ 에서 선언한 디폴트 이름으로 사용할수 있다.
만약 __configureOptions()__ 에서 디폴트로 선언해 주지 않는다면 에러가 발생한다.
```php
public function buildForm(FormBuilderInterface $builder, array $options): void
{
	$builder->add('state', ChoiceType::class, [
	    'choices' => $options['allowed_states'],
	]);
}

```

__configureOptions()__ 안에서 __setNormalizer()__ 통해 값들을 재 정의 할수 있다.
기본의 ChoiceType은 key가 0..1...2 숫자 배열로 지정 되버린다
그래서 __array_combine()__ 통해 셀렉트박스에서 표시할 값을 재 정의 하는 것이다. 
```php
$resolver->setNormalizer('allowed_states', static function (Options $options, $states) {
	$statesArray = array_combine(array_values($states), array_values($states));
	return $statesArray;
}
```


__buildForm__ 메소드에서 빌더 add 해줄 때 if문을 통해 옵션의 값을 판정 할 수 있다.
'label' , 'required' ,'help' ...기타 등등은 심포니에서 기본적으로 제공하는 옵션 값이다.
기본적으로 제공되는 옵션은 __configureOptions()__ 에 디폴트 추가 하지 않아도 된다.
```php
if (true === $options['is_extended_address']) {
    $builder->add('addressLine3', TextType::class, [
	    'label' => 'State',
	    'required' => false,
        'help' => 'Extended address info',
        'placeholder' => "Defualt",
        'mapped' => true,
        'constraints' => [
	        new Assert\NotBlank() ,
	    ],
    ]);
}
```

__setAllowedTypes__ 통해 허용되는 타입을 정할수도 있다

허용되는 타입은 null, string, array 이다
```php
$resolver->setAllowedTypes('allowed_states', ['null', 'string', 'array']);
```

허용되는 타입은 null, array 이다
```php
$resolver->setAllowedTypes('allowed_states', ['null', 'array']);
```

허용되는 타입은 bool 이다
```php
$resolver->setAllowedTypes('is_extended_address', 'bool');
```





----
### 출처 :
- https://symfony.com/doc/current/form/create_custom_field_type.html


### 연결메모
-





