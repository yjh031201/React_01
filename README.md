# 202230220 양종호
### 2026-04-08

true, false 확인에는 변수명 앞에 is를 붙여서 만들어주면 좋음
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
PackingList 컴포넌트에서 이름과 이미 싼 물건의 여부를 확인해서 보내면   
Item컴포턴트에서 받아서 조건부 렌더링을 통해 html코드를 내보냄
```jsx
export default function Item({ name, isPacked }) {
  return (
    <>
      {isPacked ? <del><li>{name} ✅</li></del> : <li>{name} ❌</li>}
    </>
  )
}
```
삼항 연산자로 수정   
-> return문 안에 넣고 중괄호로 감싼다
