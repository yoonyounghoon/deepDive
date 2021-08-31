### 이벤트(event)

- 특정 버튼을 클릭했을 때, DOM이 로드되었을 때 등의 어떠한 사건을 의미합니다.
- 브라우저는 이벤트를 감지할 수 있으며 이를 통해 사용자와 웹페이지가 상호 작용이 가능합니다.
- 이벤트 핸들러를 통해 이벤트 발생 시 원하는 함수에 연결하여 실행시킬 수 있습니다.

### event listener(event handler)

- 어떠한 이벤트가 발생했을 때 이를 처리하는 함수를 뜻 합니다.
- vanila JS에서는 addEventListener()를 통해 이벤트를 감지 할 수 있습니다.

### 이벤트 버블링

![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/0eb47baa-f116-49fb-87f9-9bd377dd81a8/Untitled.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/0eb47baa-f116-49fb-87f9-9bd377dd81a8/Untitled.png)

- 이벤트 버블링은 특정 화면 요소에서 이벤트가 발생했을 때 **해당 이벤트가 더 상위의 화면요소들 즉 부모 요소들로 전달되어 가는 특성**을 의미합니다.

프로젝트에서 Card 요소에 onClick 이벤트로 해당 링크로 연결하도록 구현했고, 하위 요소(자식 요소) hover시에 삭제버튼과 공유버튼을 만들어서 onClick 시 복사와 삭제가 되도록 구현했습니다.

삭제와 공유버튼을 클릭하면, 부모요소에도 onClick 이벤트가 걸려있으므로 클릭 시 이벤트 버블링에 의해 삭제와 링크 연결 두 가지 기능이 동작하게 됩니다.

즉 각 부모 자식 관계를 가진 태그들이 event를 가지고 있다면, 자식 요소에서 이벤트가 발생한 경우 부모 요소로 이벤트가 전파 되는 현상을 이벤트 버블링 이라고 합니다.

### stopPropagation()

이를 해결하기 위해서 e.stopPropagation()를 사용했습니다.

해당 자식 요소에서만 이벤트를 발생시키고 부모 요소로까지 버블링 되는 것을 막아주는 역할을 합니다.

### 이벤트 캡처

![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/9675071b-58fe-4b23-934d-16b02a62fd58/Untitled.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/9675071b-58fe-4b23-934d-16b02a62fd58/Untitled.png)

- 이벤트 캡처는 이벤트 버블링과 반대 방향으로 진행되는 이벤트 전파 방식입니다.
- addEventListener() 부분에 옵션으로 capture: true 를 주어 설정할 수 있습니다.

### 이벤트 위임

- 하위 요소에 각각 이벤트를 붙이지 않고 상위 요소에서 하위 요소의 이벤트들을 제어하는 방식입니다.

```jsx
var inputs = document.querySelectorAll("input");
inputs.forEach(function (input) {
  input.addEventListener("click", function (event) {
    alert("clicked");
  });
});
```

다음과 같이 자식 요소들에게 이벤트 리스너를 달아준 모습입니다.

하지만 이 상태에서 다음과 같이 새로운 list 요소를 만들어 주면, 또 이벤트 리스너를 각각 달아줘야 하는 문제가 있습니다.

```jsx
var itemList = document.querySelector(".itemList");

var li = document.createElement("li");
var input = document.createElement("input");
var label = document.createElement("label");

input.setAttribute("type", "checkbox");
input.setAttribute("id", "item3");
li.appendChild(input);
itemList.appendChild(li);
```

이를 해결하기 위해

```jsx
var itemList = document.querySelector(".itemList");
itemList.addEventListener("click", function (event) {
  alert("clicked");
});
```

list의 상위 요소(부모 요소)에 이벤트 리스너를 한번만 등록해 주면 하위 요소(자식 요소)를 클릭했을때 **이벤트 버블링**이 일어나 상위 요소(부모 요소)로 까지 이벤트가 전달됩니다.

#### 요약

**이벤트 버블링** : 하위요소에서 상위요소로 이벤트가 전파
**이벤트 캡처링** : 상위요소에서 하위요소로 이벤트가 전파
