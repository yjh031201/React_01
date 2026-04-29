# 202230220 양종호
# 2026-04-29   
## 스타일 적용하기
1. css (import)   
2. 인라인 css   
3. CSS-in-JS   
4. CSS 프레임워크   
> 

### CSS-in-JS
>(장점)컴포넌트 내에 바인딩되기 때누에 관리와 유지보수 유리   
>(장점)props기반으로 동적 스타일링 적용에 편리   
>(장점)고유한 클래스명 자동 생성   
>(장점)provider컴포넌트를 통해 전역 테마 설정을 쉽게 적요 가능   
>(단점)런타임이 오래 걸릴 수 있음   
### CSS 프레임워크
> tailwindcss   
> bootstrap   
> materialize   
> bulma 등등   
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

