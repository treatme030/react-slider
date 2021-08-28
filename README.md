## ⬅➡ react-slider

1. 데이터와 데이터 인덱스 변경에 따른 이전, 다음 슬라이드
```javascript

const [people, setPeople] = useState(data)
const [index, setIndex] = useState(0)

//index, people 상태값 변경될때마다 
useEffect(() => {
  const lastIndex = people.length - 1;
  if(index < 0){
    setIndex(lastIndex)
  }
  if(index > lastIndex){
    setIndex(0)
  }
},[index, people])

//슬라이드 되는 부분
<div className="section-center">
  {
    people.map((person, personIndex) => {
      const { id, image, name, title, quote } = person

      let position = 'nextSlide';
      if(personIndex === index){
        position = 'activeSlide';
      }
      if(personIndex === index - 1 ||
        (index === 0 && personIndex === people.length - 1)){
          position = 'lastSlide';
        }

      return(
        <article className={position} key={id}>
          <img src={image} alt={name} className="person-img" />
          <h4>{name}</h4>
          <p className="title">{title}</p>
          <p className="text">{quote}</p>
          <FaQuoteRight className="icon" />
        </article>
      );
    })
  }
  <button className="prev" onClick={() => setIndex(index - 1)}>
    <FiChevronLeft/>
  </button>
  <button className="next" onClick={() => setIndex(index + 1)}>
    <FiChevronRight/>
  </button>
</div>
```

2. 자동 슬라이드
```javascript
useEffect(() => {
    let slider = setInterval(() => {
      setIndex(index + 1)
    }, 4000);
    //자동슬라이드 중 이동버튼을 여러번 클릭해도 전에 작업이 남아 계속되지 않도록
    return () => clearInterval(slider);
 },[index])
```

<참고>
Coding Addict
