# Flux 패턴

## MVC 패턴과 한계

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/d4149520-d6be-4d44-bd0c-53bf7cba0e7a/Untitled.png)

MVC 패턴은 데이터를 다루는 로직 ( Controller ), 데이터 ( Model ), 사용자 인터페이스 ( View )로  나누어 애플리케이션을 구현하는 하나의 개발 모델이다.

Controller는 Model의 데이터를 조회하거나 업데이트 하는 역할을 하며, Model의 변화는 View에 반영된다. 그리고 사용자가 뷰를 통해 데이터를 입력하면, 모델에 영향을 주면서,  데이터를 관리하게 됩니다.

### 로직과 데이터, 뷰를 나누어 관리하기 때문에 효율적이다. 하지만?

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/c76520fb-3909-4833-8d38-6f28e4ad3d48/Untitled.png)

FaceBook 웹앱 에서의  MVC 구조는 앱이 커지면서 굉장히 복잡해졌다고 합니다. View가 다양한 상호 작용을 위해 여러 개의 Model을 동시에 업데이트 하는 상황이 발생했고,  이렇게 많은 의존성을 가지면서 예측 불가능한 상황이 많이 나오게 되었습니다.

## Flux 패턴

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/e9ab9ad5-a0dc-4377-86b7-32bdb3029b71/Untitled.png)

Facebook팀은 단방향 데이터 흐름을 가지는 Flux 패턴을 만들어 해결하였습니다.

### Action

사용자와의 상호작용, 어떤 액션이 발생하면  액션생성 함수를 만들어, Dispatcher에 해당 액션 메시지를 보내줍니다. 타입과 데이터(payload)를 가지고 있습니다.

```jsx
{
  type: 'ADD_TODO',
  payload: 1,
}
```

### Dispatcher

디스패처는 액션 메시지를 감지하는 순간 그것을 각 스토어에 전달합니다. 

### Store

Store는 데이터와 데이터를 가공하는 로직을 가지고 있습니다. 액션이 넘어오면 등록된 콜백을 통해, 액션타입에 맞는 로직을 실행하고 데이터를 업데이트 합니다. Store는 변경된 데이터를 View에게 알려줍니다.

### View

컨트롤러 뷰는 스토어에서 변경된 데이터를 가져와 모든 자식 뷰에게 데이터를 분배합니다. 데이터를 넘겨받은 뷰는 화면을 새로 렌더링합니다.

## 정리

Facebook은 이 Flux 패턴을 고안하고 View의 역할로 React를 이용했다. 이 조합은 더 예측 가능하고 확장성이 높은 앱을 만들 수 있게 해주었다고 한다