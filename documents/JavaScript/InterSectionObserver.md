# InterSection Observer API
---

기본적으로 브라우저의 뷰포트와 설정한 요소의 교차점을 관찰하며, 요소가 뷰포트에 포함되는지 포함되지 않는지, 더 쉽게는 화면에 지금 보이는 요소인지 안보이는 요소인지를 구별하는 기능을 제공.

## InterSectionObserver

new InterSectionObserver() 를 통해 생성한 인스턴스로 관찰자(Observer)를 초기화하고 관찰할 대상 ( Element)를 지정.

생성자는 2개의 인수를 가짐 ( callback, options )

```jsx
const io = new InterSectionObserver(callback, options) 
io.observer(element) // 관찰할 대상 등록

const options = {
    root: null, // 관찰하는 대상의 부모요소를 지정
    rootMargin: "20px", // 관찰하는 뷰포트의 마진 지정
    threshold: 1.0, // 관찰요소와 얼만큼 겹쳤을때 콜백을 수행할지 지정
  };
```

### callback

---

관찰할 대상(Target)이 등록되거나, 가시성 (Visibility, 보이는지 보이지 않는지)에 변화가 생기면 관찰자는 콜백을 실행합니다.

### entries

---

entries는 IntersectionObserverEntry 인스턴스의 배열 입니다.

읽기 전용의 다음 속성들을 포함합니다.

- **`boundingClientRect`**: 관찰 대상의 사각형 정보([DOMRectReadOnly](https://developer.mozilla.org/en-US/docs/Web/API/DOMRectReadOnly))
- **`intersectionRect`**: 관찰 대상의 교차한 영역 정보([DOMRectReadOnly](https://developer.mozilla.org/en-US/docs/Web/API/DOMRectReadOnly))
- **`intersectionRatio`**: 관찰 대상의 교차한 영역 백분율(**`intersectionRect`** 영역에서 **`boundingClientRect`** 영역까지 비율, Number)
- **`isIntersecting`**: 관찰 대상의 교차 상태(Boolean)
- **`rootBounds`**: 지정한 루트 요소의 사각형 정보([DOMRectReadOnly](https://developer.mozilla.org/en-US/docs/Web/API/DOMRectReadOnly))
- **`target`**: 관찰 대상 요소([Element](https://developer.mozilla.org/en-US/docs/Web/API/Element))
- **`time`**: 변경이 발생한 시간 정보([DOMHighResTimeStamp](https://developer.mozilla.org/en-US/docs/Web/API/DOMHighResTimeStamp))

### options

---

```jsx
const options = { 
root: null, //기본 null (viewport), 관찰대상의 부모요소를 지정 
rootMargin: "20px", // 관찰하는 뷰포트의 마진 지정 
threshold: 1.0, // 관찰요소와 얼만큼 겹쳤을 때 콜백을 수행하도록 지정하는 요소 
};

출처: https://watermelonlike.tistory.com/153 [수박수의 블로그]
```

## Methods

---

observer() : 대상요소의 관찰 시작

unobserve() : 관찰 중지

disconnect(): 모든 요소 관찰 중지