## 변수 ( Variables )

---

### 의미있고 발음하기 쉬운 변수 이름을 사용하세요

**안좋은 예:**

```jsx
const yyyymmdstr = moment().format("YYYY/MM/DD");
```

**좋은 예:**

```jsx
const currentDate = moment().format("YYYY/MM/DD");
```

### 동일한 유형의 변수에 동일한 어휘를 사용하세요

**안좋은 예:**

```jsx
getUserInfo();
getClientData();
getCustomerRecord();
```

**좋은 예:**

```jsx
getUser();
```

### 검색가능한 이름을 사용하세요

우리는 코드를 작성하는 것보다 읽는 경우가 더 많습니다. 그렇기 때문에 코드를 읽기 쉽고 검색 가능하게 작성해야 합니다. 그렇지 않으면 여러분의 코드를 이해하려고 하는 사람들에게 큰 어려움을 줍니다.

buddy.js, ESLint와 같은 도구들이 이름이 정해져있지 않은 상수들을 발견하고 고칠 수 있게 도와줍니다.

**안좋은 예:**

```jsx
// 대체 864000000 무엇을 의미하는 걸까요?
setTimeout(blastOff, 864000000);
```

**좋은 예:**

```jsx
// 대문자로 `const` 전역 변수를 선언하세요
const MILLISECONDS_IN_A_DAY = 86400000;
setTimeout(blastOff, MILLISECONDS_IN_A_DAY);
```

### 의도를 나타내는 변수들을 사용하세요

**안좋은 예:**

```jsx
const address = "One Infinite Loop, Cupertino 95014";
const cityZipCodeRegex = /^[^,\\]+[,\\\s]+(.+?)\s*(\d{5})?$/;
saveCityZipCode(
  address.match(cityZipCodeRegex)[1],
  address.match(cityZipCodeRegex)[2]
);
```

**좋은 예:**

```jsx
const address = "One Infinite Loop, Cupertino 95014";
const cityZipCodeRegex = /^[^,\\]+[,\\\s]+(.+?)\s*(\d{5})?$/;
const [, city, zipCode] = address.match(cityZipCodeRegex) || [];
saveCityZipCode(city, zipCode);
```

### 자신만 알아볼 수 있는 작명을 피하세요

명시적인 것이 암시적인 것보다 좋습니다.

**안좋은 예:**

```jsx
const locations = ["서울", "인천", "수원"];
locations.forEach((l) => {
  doStuff();
  doSomeOtherStuff();
  // ...
  // ...
  // ...
  // 잠깐, 'l'은 또 뭘까요?
  dispatch(l);
});
```

**좋은 예:**

```jsx
const locations = ["서울", "인천", "수원"];
locations.forEach((location) => {
  doStuff();
  doSomeOtherStuff();
  // ...
  // ...
  // ...
  dispatch(location);
});
```

### 문맥상 필요없는 것들을 쓰지 마세요

**안좋은 예:**

```jsx
const Car = {
  carMake: "BMW",
  carModel: "M3",
  carColor: "파란색",
};

function paintCar(car) {
  car.carColor = "빨간색";
}
```

**좋은 예:**

```jsx
const Car = {
  make: "BMW",
  model: "M3",
  color: "파란색",
};

function paintCar(car) {
  car.color = "빨간색";
}
```

### 기본 매개변수가 short circuiting (단축평가) 트릭이나 조건문 보다 깔끔합니다.

기본 매개변수는 매개변수가 undefined 일때만 적용됩니다.

'', "", false, null, 0, NaN 같은 falsy한 값들은 기본 매개변수가 적용되지 않습니다.

**안좋은 예:**

```jsx
function createMicrobrewery(name) {
  const breweryName = name || "Hipster Brew Co.";
  // ...
}
```

**좋은 예:**

```jsx
function createMicrobrewery(name = "Hipster Brew Co.") {
  const breweryName = name;
  // ...
}
```

### 정리

- 의미있는 이름, 의도를 나타내는 이름을 명시적으로 작성
- 동일한 유형의 변수에 동일한 어휘로 작성
- 검색가능한 이름 사용
- 기본 매개변수 사용이 깔끔할 경우가 있다.
