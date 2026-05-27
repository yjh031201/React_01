# 202230220 양종호
# 2026-05-27
1. React가 state를 강조하는 이유   
   >React의 거의 모든 기능은 state 중심으로 연결   
2. State Hook의 동작 원리   
   >useState와 같은 "use"로 시작하는 모든 함수를 Hook이라고 함   
   >Hook은 렌더링 중에만 사용 가능한 특별한 함수   
   >useState()는 문법적으로는 함수 호출이지만   
   >React관점에서 보면 Hook사용은 "함수를 실행해서 값을 받아온다"보다는 "이 컴포넌트는 state가 필요하다"하고 선언하는 것으로 좋다.   
   >useState를 사용할 때 변수 이름이 결정되면 setter함수의 이름은 변수이름 앞에 set을 붙여서 지정하는 것이 관례적인 규칙이다.   
   >예) ```const [index, setIndex] = useState(0)```   
3. Hook 사용의 주의점   
   >일반 모듈과 같이 import해서 사용한다.   
4. 여러개의 state 사용
   >하나의 컴포넌트에서 사용 가능한 state변수의 개수에는 제한이 없으며, 원하는 타입의 state변수를 가질 수 있다.   
   >예)
   >```jsx
   >const [index, setIndex] = useState(0)
   >const [more, setMore] = useState(false)
   >function handlerSee() {
   >   setMore(!more);
   >}
   ><button className={`${styles.navBtn} ${styles.see}`} onClick={handlerSee}>
   >   {more ? 'Hide' : 'Show'} Description
   ></button>
   >{more && <p>{slide.description}</p>}
   >```
5. state가 있는 컴포넌트를 중첩한다면?   
   >state는 각 컴포넌트에서 독립적으로 동작함   
   >props와 달리 state는 선언한 컴포넌트 외에는 완전히 비공개   
   >두개의 캐러셀 state를 동기화 하고 싶다면, 자식 컴포넌트에서 state를 제거하고, 가장 가까운 공통 부모 컴포넌트에 state를 추가하면 된다.   
6. 렌더링 과정의 3단계
   >React는 컴포넌트가 화면에 표시되기 전에 렌더링 과정을 거치게 됩니다.   
   >Reacr의 렌더링 프로세스는 렌더링 트리거-> 컴포넌트 렌더링 -> Dom에 커밋 등 3단계로 진행됨   
   >1단계 : 렌더링 트리거   
   >>컴포넌트에 렌더링이 일어나는 이유는 2가지
   >>#### 1.컴포넌트의 초기 렌더링인 경우   
   >>>대상 DOM노드와 함께 createRoot를 호출한 다음 해당 컴포넌트로 render 메서드를 호출하면 이 작업이 완료됩니다.   
   >>>vite로 프로젝트를 생성한 경우 index.jsp의 역할을 main.jsx에서 함   
   >>>id가 root인 엘리먼트 즉 DOM노드를 createRoot()함수로 호출한 다음, render 메서드를 통해 App컴포넌트를 호출하고있다   
   >>>이 작업을 초기 렌더링 작업이라고 함   
   >>>```jsx
   >>>import { StrictMode } from 'react'
   >>>import { createRoot } from 'react-dom/client'
   >>>import './index.css'
   >>>import App from './App.jsx'
   >>>createRoot(document.getElementById('root')).render(
   >>><StrictMode>
   >>><App />
   >>></StrictMode>,
   >>>)
   >>>```
   >>#### 2.컴포넌트의 state가 업데이트된 경우
   >>>컴포넌트가 초기 렌더링 된 후에는 set함수를 통해 state를 업데이트해서, 추가적인 렌더링을 촉발시킬 수 있다.
   >>>컴포넌트의 state를 업데이트하면 자동으로 렌더링 큐가 추가되고, 순서대로 렌더링합니다.
   >>>#### StrictMode컴포넌트
   >>>>StriceMode 컴포넌트는 개발 모드에서 애플리케이션의 잠재적인 버그롸 부작용을 조기에 발견할 수 있도록 돕는 검사 도구   
   >>>>이중 렌더링 검사 / Effect 및 Ref 클린업 테스트 / 지원 중단된 API 경고 등   
   >>>#### 렌더링 큐(Queue)   
   >>>>큐는 선입선출 자료구조   
   >>>>렌더링 요청을 순서대로 보관했다가 가장 먼저 요청한 것부터 차례대로 처리 자료구조를 사용함   
# 2026-05-20
### 이미지를 배열로 저장
```jsx
export const imgData = [
  {
    name : "slide1",
    artist : "artist1",
    description : "description1",
    url:"https://placehold.co/600x400?text=Slide1",
    alt: "slide1"
  },
  {
    name : "slide2",
    artist : "artist2",
    description : "description2",
    url:"https://placehold.co/600x400?text=Slide2",
    alt: "slide2"
  },
  {
    name : "slide3",
    artist : "artist3",
    description : "description3",
    url:"https://placehold.co/600x400?text=Slide3",
    alt: "slide3"
  },
  {
    name : "slide4",
    artist : "artist4",
    description : "description4",
    url:"https://placehold.co/600x400?text=Slide4",
    alt: "slide4"
  },
  {
    name : "slide5",
    artist : "artist5",
    description : "description5",
    url: slide.slider1,
    alt: "slide5"
  },
  {
    name : "slide6",
    artist : "artist6",
    description : "description6",
    url: slide.slider2,
    alt: "slide6"
  }
];
```
### 저장한 이미지를 가져와서 사용
```jsx
export default function Carousel() {
  const [index, setIndex] = useState(0);
  function handlerClick() {
    if (index === imgData.length - 1) {
      setIndex(0);
    } else {
      setIndex(index + 1);
    }
  }
  function handlerPrevious() {
    if (index === 0) {
      setIndex(imgData.length - 1);
    } else {
      setIndex(index - 1);
    }
  }

  let slide = imgData[index];
  return (
    <>
      <div className={styles.imgWrapper}>
        <div className={styles.btnGroup}>
          <button className={`${styles.navBtn} ${styles.next}`} onClick={handlerClick}>Next</button>
          <button className={`${styles.navBtn} ${styles.prev}`} onClick={handlerPrevious}>Previous</button>
        </div>
        <h2>
          <i>{slide.name}</i>
          by {slide.artist}
        </h2>
        <h3>
          ({index + 1} of {imgData.length})
        </h3>
        <img src={slide.url} alt={slide.alt} />
      </div>
      <p>{slide.description}</p>
    </>
  )
}
```
# 2026-05-13   
1. 비디오 함수 및 이벤트 함수에 대해,   
   > 저번 실습에서는 Hook을 사용할 수 없어 DOM에 직접 접근했지만 React에서는 DOM에 직접 접근하는 것을 권장하지 않음   
   > React에서 DOM을 제어할 때는 useRef를 사용하여 엘리먼트를 ref객체로 관리하는 것이 좋음(관례적으로 앞에 use가 붙은 것은 Hook임)   
   > 모듈 이름은 camelCace, 컴포넌트는 PascalCase사용
2. 이벤트 전파의 중지
   > 이벤트 헨들러는 이벤트 오브젝트를 유일한 매개변수로 사용
   > 관례적으로 이벤트 오브젝트를 의미하는 "event"를 "e"로 줄여서 호출
   > ## e.stopPropagation() 예시
   > ```jsx
   > import style from '../assets/Bubble.module.css' 
   >function Button({onClick, children}){
   >  return(
   >    <button className={style.button} onClick={e=>{e.stopPropagation(); onClick()}}>
   >      {children}
   >    </button>
   >  )
   >}
   >
   >export default function Bubble(){
   >  
   >  return (
   >    <>
   >      <h1 className={style.Bubble}>Bubble</h1>
   >      <nav className={style.navBar} onClick={()=>alert("네비게이션바 클릭!")}>
   >        <Button onClick={() => alert("버튼 1 클릭")}>
   >           버튼1      {/*<---children */}
   >        </Button>
   >        <Button onClick={() => alert("버튼 2 클릭")}>
   >          버튼2
   >        </Button>
   >      </nav>
   >    </>
   >  )
   >}
   >```
3. e.stopPropagation()와 e.preventDefult()   
   >이벤트 전파를 중지하는 데는 둘다 유용하지만, 전혀 다른 기능을 가지고 있음   
   >e.stopPropagation()은 이벤트 핸들러가 상위 태그에서 실행되지 않도록 멈추는 기능을 합니다.   
   >반면 e.preventDefult()는 브라우저 기본 동작을 갖고 있는 일부 이벤트가 해당 기본 동작을 실행하지 않도록 방지하는 기능을 합니다.
   >## e.preventDefult() 예시
   >```jsx
   >export default function Signup2(){
   >return(
   > <form onSubmit={(e)=> {
   >   e.preventDefault();
   >   alert("Submitting");
   > }}>
   >   <input/>
   >   <button>Send2</button>
   > </form>
   >)
   >}
   >```
4. State의 개념과 useState   
   >State: 컴포넌트의 기억장소   
   >>컴포넌트는 상호작용의 결과로 화면의 내용을 변경해야 하는 경우가 있는데   
   >>예를 들어 폼에 무언가 입력하면 입력 필드가 업데이트 되어야 하고   
   >>이미지 캐러셀에서 다음 버튼을 클릭할 때 표시되는 이미지가 변경되어야 함   
   >>State는 현재 값들을 저장하는 곳   
# 2026-05-06
## 이벤트 핸들러 적용   
1. 비디오 실행
```jsx
import Button from "./Button";
import { handleClick, handlePlay, handleStop } from "./Handle";

export default function Toolbar() {
  return (
    <>
      <nav>
        <Button message="videoplay" handler={handlePlay}>
          play
        </Button>
        
        <Button message="videoplay" handler={handleStop}>
          stop
        </Button>
      </nav>
      <section>
        <video id="videoplay" width="320" height="240" controls>
          <source src="https://www.w3schools.com/html/mov_bbb.mp4" type="video/mp4" />
          Your browser does not support the video tag.
        </video>
      </section>
      <section>
        <div className="toolbar">
          <Button message="버튼1클릭" handler={handleClick}>
            버튼1
          </Button>
          <Button message="버튼2클릭" handler={handleClick}>
            버튼2
          </Button>
        </div>
      </section>
    </>
  );
}
```
```jsx
export function handleClick(message) {
    alert(message);
  }
export function handlePlay({ message }) {
  const videoSource = document.getElementById(message);
  if (videoSource) videoSource.play();
}

export function handleStop({ message }) {
  const videoSource = document.getElementById(message);
  if (videoSource) videoSource.pause();
}
```
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

## 이벤트 핸들러
>사용자가 클릭과 같은 특정 입력을 이벤트라고 하고, 이벤트가 발생했을때 로직을 설정하는게 이벤트 핸들러이다.   
>button과 같은 내장 컴포넌트는 onClick과 같은 내장 브라우저 이벤트만 지원함   
>이벤트 핸들러 함수는 호출하는 것이 아니라 전달하는 것이다
>>함수의 이름만 prop의 형태로 전당   
>함수를 호출하므로 함수의 이름에 소괄호 사용   
>```jsx
>
>export default function ButtonCom() {
>  function clickHandler() {
>    alert("버튼 클릭");
>  }
>
>  return (
>    <>
>      <h1 className={style.title}>ButtonCom</h1>
>      <nav className={style.nav}>
>        <button className={style.btn} onClick={clickHandler}>
>          Button1
>        </button>
>        <button className={style.btn} onClick={clickHandler}>
>          Button2
>        </button>
>      </nav>
>    </>
>  );
>}
>```
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

