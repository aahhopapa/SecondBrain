### 날짜 :  2022-11-17 18:19

### 인덱스 :

### 태그 :

<span style="color: red">강조</span>

----

### 메모 :

cmd를 열어 pem키가 있는 폴더로 이동한다
> cd C:\ProgramData

하나씩 실행하면된다
aahhopapa.com.pem 는 적용할 pem 파일 명과 일치 시킨다

> icacls.exe aahhopapa.com.pem /reset
> icacls.exe aahhopapa.com.pem /grant:r %username%:(R)
> icacls.exe aahhopapa.com.pem /inheritance:r



----
### 출처 :
- https://dabid.tistory.com/entry/%EC%9C%88%EB%8F%84%EC%9A%B010%EC%97%90%EC%84%9C-SSH-%EC%A0%91%EC%86%8D-%EC%8B%9C-pem-%ED%8C%8C%EC%9D%BC-%EA%B6%8C%ED%95%9C%EB%B3%80%EA%B2%BD



### 연결메모
-








