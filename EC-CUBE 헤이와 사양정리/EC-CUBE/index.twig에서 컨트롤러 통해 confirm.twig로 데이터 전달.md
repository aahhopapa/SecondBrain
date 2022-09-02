### 날짜 :  2022-08-31 13:56

### 인덱스 :

### 태그 : #controller 

----

### 메모 :

index.twig
```twig
<div class="ec-off1Grid">
	<form method="post" action="{{ url('anything') }}" novalidate class="h-adr">
		<div class="ec-halfInput{{ has_errors(form.any_input) ? ' error' }}">
			{{ form_widget(form.any_input) }}
			{{ form_errors(form.any_input) }}
		</div>
		<div class="ec-group{{ has_errors(form.any_select) ? ' error' }}">
			{{ form_widget(form.any_select) }}
			{{ form_errors(form.any_select) }}
		</div>
		
		<div class="ec-off4Grid__cell">
			<button class="ec-blockBtn--action" type="submit" name="mode" value="confirm">{{ '同意する'|trans }}</button>
		</div>
	</form>
</div>
```

버튼 클릭 하여 Request를 Post로 보낼 때

기본적으로 form 태그의 __action="{{ url('anything') }}"__ 의 anything 이 
Request의 parameters에 추가 된다.

button태그의 __name="mode"__ 는 키,  __value="confirm"__  이 벨류가 되는 어레이 가 되어 
Request의 parameters에 추가 된다.

![[index.twig에서 컨트롤러 통해 confirm.twig로 데이터 전달.png]]

controller.php
```php
/**
 * 画面.
 * @Route("/anything", name="anything", methods={"GET", "POST"})
 * @Route("/anything", name="anything_confirm", methods={"GET", "POST"})
 * @Template("Anything/index.twig")
 */
public function testMethod(Request $request){

	switch ($request->get('mode')) {
		case 'confirm':
	
	    return $this->render('Anything/confirm.twig', [
	            'form' => $form->createView(),
	        ]
	    );
	
		case 'complete':
	
		return  [
	        'form' => $form->createView(),
	    ];
	}
}
```

index.twig에서 confirm.twig로 넘기기 위해서
또 하나 설정을 꼭 해야 하는것이 있다
바로 토큰 값이다.

index.twig
```twig
<div class="ec-off1Grid">
	<form method="post" action="{{ url('anything') }}" novalidate class="h-adr">
	{{ form_widget(form._token) }}
</div>
```


twig에 토큰 값을 추가 하지 않으면 
>{{ form_widget(form._token) }}

컨트롤러에서 isValid() 가 false가 되며 디버깅을 보면 에러를 담고 있다.

![[index.twig에서 컨트롤러 통해 confirm.twig로 데이터 전달2.png]]

controller.php
```php
// Request가 post로 전달되었는지 확인
$var1 = $form->isSubmitted();
if($var1) {
	// post로 전달되었을 경우만 isValid 메소드를 호출할수있다. 
	// 폼의 검증이 마쳐졌는지 확인
	$var2 = $form->isValid();
}

// post로 전달되었고 검증도 마쳤다면 confirm.twig로 이동
if ($var1 && $var2) {
	switch ($request->get('mode')) {
		case 'confirm':
	        return $this->render('Anything/confirm.twig', [
	                'form' => $form->createView(),
	        ]);
	
	    case 'complete':
	        return  [
	            'form' => $form->createView(),
	        ];
    }
} else {
	// 아닌경우 index.twig로 남는다.
	return  [
		'form' => $form->createView(),
	];
}
```

----
### 출처 :
-


### 연결메모
-








