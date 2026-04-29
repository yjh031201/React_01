# 202230220 양종호
# 2026-04-29   
## 스타일 적용하기
1. css (import)   
2. 인라인 css   
3. CSS-in-JS   
4. CSS 프레임워크   
5. CSS Module
### CSS(import)   
>css파일과 jsx파일을 따로 만들어 import해주는 방식

### 인라인 css
>따로 설정파일을 만들지 않고 jsx파일 내부에서 style을 부여해주는 방식   
### CSS-in-JS
>(장점)컴포넌트 내에 바인딩되기 때누에 관리와 유지보수 유리   
>(장점)props기반으로 동적 스타일링 적용에 편리   
>(장점)고유한 클래스명 자동 생성   
>(장점)provider컴포넌트를 통해 전역 테마 설정을 쉽게 적요 가능   
>(단점)런타임이 오래 걸릴 수 있음   
### CSS 프레임워크
> tailwindCSS   
> bootstrap   
> materialize   
> bulma 등등
### CSS Module
>css module은 클래스명을 _[클래스이름]-[해쉬값]의 형태로 자동 변환하여,   
>고유한 이름의 로컬 스코프를 제공하는 기술
>스타일의 충돌 방지가능, 유지보수에 유리
>### 사용법
>>파일 이름의 규칙: 파일이름은 [컴포넌트 이름].module.css의 형태로 확장자는 반드시 .module.css 사용   
>>일반 css의 작성법을 따름
>>태그선택자는 고유한 이름을 할당받지 않음   
>>camelCase를 주로 사용   
>### 클래스에 적용
>>import하여 스타일을 사용   
>>jsx에서는 class키워드 대신 className을 사용   
>>class 이름은 객체를 사용할 때처럼 [변수명].[클래스명]의 형태로 작성   
>>class이름 전체를 중괄호로 감싸야함   
>>
# 2026-04-15
json

> key : value

== --> 타입은 달라도 모양이 같으면 true   
=== --> 타입까지 같아야 true

화살표 함수는 묵시적으로 => 바로 뒤 식을 반환하기 때문에 return문이 필요하지않다.

그러나 ```<li>...</li>``` 와 같은 한 줄이 아닌 중괄호를 사용해야 하는 경우는 반환이 안되게 때문에 return문이 필요하다

내부 변수 이름은 관용적으로 heroes -> hero, filterHeroes -> filterHero 처럼 복수를 단수로 사용한다.   
key prop(key={hero.id})를 부여해줘야 key prop오류가 안남 
```jsx
import { heroes } from '../components/Heroes';

export default function MovieHeroes() {
  const filterHeroes = heroes.filter(hero => hero.power === 5);
  const listHeroes = filterHeroes.map(hero =>
    <li key={hero.id}>
      <p>
        {hero.name}의 배역은 {hero.casting}입니다.
      </p>
      <p>
        {hero.casting}의 파워는 {hero.power}입니다.
      </p>
    </li>);
  return (
    <section>
      <h1>영화 속 영웅들</h1>
      <ul>
        {listHeroes}
      </ul>
    </section>
  );
}
```
# 2026-04-08

true, false 확인에는 변수명 앞에 is를 붙여서 만들어주면 좋음   
   
PackingList 컴포넌트에서 이름과 이미 싼 물건의 여부를 확인해서 보내면   
Item컴포턴트에서 받아서 조건부 렌더링을 통해 html코드를 내보냄
```jsx
export default function PackingList() {
  return (
    <section>
      <h2>여행 준비 목록</h2>
      <ul>
        <Item name="여분 옷" isPacked={true} />
        <Item name="책" isPacked={false} />
        <Item name="노트북" isPacked={true} />
      </ul>
    </section>
  )
}
```
```jsx
export default function Item({ name, isPacked }) {
  if (isPacked) {
      return <li>{name} ✅</li>
      
    } else {
      return <li>{name} ❌</li>
    }
}
```
삼항 연산자로 수정   
-> return문 안에 넣고 중괄호로 감싼다   
```<del>``` <-- <del>취소선
```jsx
export default function Item({ name, isPacked }) {
  return (
    <li>
      {isPacked ? (
        <del>{name+ "✅"}</del>
      ) : (
        name
      )}
    </li>
  )
}
```

