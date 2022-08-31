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




----
### 출처 :
-


### 연결메모
-








