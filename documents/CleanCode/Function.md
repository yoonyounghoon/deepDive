## 함수 ( Function )

---

### 함수 인자는 2개 이하가 이상적입니다.

매개변수의 개수 제한 → 함수 테스팅을 쉽게 만들어 준다.

많은 인자들을 사용해야 한다면 → 객체를 이용

비구조화 구문을 사용하여면 함수가 어떤 속성을 사용하는지 즉시 알 수 있음

**안좋은 예:**

```jsx
function createMenu(title, body, buttonText, cancellable) {
  // ...
}
```

**좋은 예:**

```jsx
function createMenu({ title, body, buttonText, cancellable }) {
  // ...
}
createMenu({
  title: "Foo",
  body: "Bar",
  buttonText: "Baz",
  cancellable: true,
});
```

### 함수는 하나의 행동만 해야합니다.

소프트웨어 엔지니어링에서 가장 중요한 규칙.

함수가 1개 이상의 일을 한다면 → 작성하는 것, 테스트 하는것, 이해하는 것도 어려워짐

하나의 함수에 하나의 행동을 정의한다면 → 읽기 쉽고 유지보수하는 코드가 가능

**안좋은 예:**

```jsx
function emailClients(clients) {
  clients.fotEach((client) => {
    // DB에 고객기록 확인 후
    const clientRecord = database.lookup(client);
    if (clientRecord.isActive()) {
      // 있다면 이메일 보내기
      email(client);
    }
  });
}
```

**좋은 예:**

```jsx
function emailClients(clients) {
  clients.filter(isClientActive).forEach(email);
}

function isClientActive(client) {
  const clientRecord = database.lookup(client);
  return clientRecord.isActive();
}
```

### 함수명은 함수가 무엇을 하는지 알 수 있어야 합니다.

**안좋은 예:**

```jsx
function AddToDate(date, month) {
  // ...
}

const date = new Date();

// 뭘 추가하는 건지 이름만 보고 알아내기 힘듭니다.
AddToDate(date, 1);
```

**좋은 예:**

```jsx
function AddMonthToDate(date, month) {
  // ...
}

const date = new Date();
AddMonthToDate(date, 1);
```

### 중복된 코드를 작성하지 마세요

중복된 코드가 존재한다는 것 → 어떤 로직을 수정해야 할 일이 생겼을 때 수정 해야할 코드가 한 곳 이상이라는 것을 뜻함.

중복 코드를 제거한다는 것 → 함수/모듈/클래스를 사용하여 추상화를 만드는 것

**안좋은 예:**

```jsx
function showDeveloperList(developers) {
  developers.forEach((developers) => {
    const expectedSalary = developer.calculateExpectedSalary();
    const experience = developer.getExperience();
    const githubLink = developer.getGithubLink();
    const data = {
      expectedSalary,
      experience,
      githubLink,
    };

    render(data);
  });
}

function showManagerList(managers) {
  managers.forEach((manager) => {
    const expectedSalary = manager.calculateExpectedSalary();
    const experience = manager.getExperience();
    const portfolio = manager.getMBAProjects();
    const data = {
      expectedSalary,
      experience,
      portfolio,
    };

    render(data);
  });
}
```

**좋은 예:**

```jsx
function showEmployeeList(employees) {
  employees.forEach((employee) => {
    const expectedSalary = employee.calculateExpectedSalary();
    const experience = employee.getExperience();

    let portfolio = employee.getGithubLink();

    if (employee.type === "manager") {
      portfolio = employee.getMBAProjects();
    }

    const data = {
      expectedSalary,
      experience,
      portfolio,
    };

    render(data);
  });
}
```

### 사이드 이펙트를 피하세요

함수는 값을 받아서 어떤 일을 하거나 값을 리턴할 때 사이드 이펙트를 만들어냅니다.

사이드 이펙트는 파일에 쓰여질 수도, 전역 변수를 수정할 수도 있습니다.

**안좋은 예:**

```jsx
// 아래 함수에 의해 참조되는 전역 변수입니다.
// 이 전역 변수를 사용하는 또 하나의 함수가 있다고 생각해보세요
// 이제 이 변수는 배열이 될 것이고, 프로그램을 망가뜨리겠죠
let name = "Ryan McDermott";

function splitIntoFirstAndLastName() {
  return name.split(" ");
}

splitIntoFirstAndLastName();

console.log(name); // ['Ryan', 'McDermott'];
```

**좋은 예:**

```jsx
function splitIntoFirstAndLastName(name) {
  return name.split(" ");
}

const name = "Ryan McDermott";
const newName = splitIntoFirstAndLastName(name);

console.log(name); // 'Ryan McDermott';
console.log(newName); // ['Ryan', 'McDermott'];
```

### 명령형 프로그래밍보다 함수형 프로그래밍을 지향하세요

함수형 언어는 더 깔끔하고 테스트하기 쉽습니다. 가능하면 이 방식을 사용하도록 해보세

**안좋은 예:**

```jsx
const programmerOutput = [
  {
    name: "Uncle Bobby",
    linesOfCode: 500,
  },
  {
    name: "Suzie Q",
    linesOfCode: 1500,
  },
  {
    name: "Jimmy Gosling",
    linesOfCode: 150,
  },
  {
    name: "Gracie Hopper",
    linesOfCode: 1000,
  },
];

let totalOutput = 0;

for (let i = 0; i < programmerOutput.length; i++) {
  totalOutput += programmerOutput[i].linesOfCode;
}
```

**좋은 예:**

```jsx
const programmerOutput = [
  {
    name: "Uncle Bobby",
    linesOfCode: 500,
  },
  {
    name: "Suzie Q",
    linesOfCode: 1500,
  },
  {
    name: "Jimmy Gosling",
    linesOfCode: 150,
  },
  {
    name: "Gracie Hopper",
    linesOfCode: 1000,
  },
];

const totalOutput = programmerOutput
  .map((programmer) => programmer.linesOfCode)
  .reduce((acc, linesOfCode) => acc + linesOfCode, INITIAL_VALUE);
```

### 정리

- 함수는 두개 이하의 인자가 이상적
- 함수는 하나의 동작만 하도록 정의
- 함수명은 함수가 무엇을 하는지 알 수 있도록
- 중복된 코드를 제거 ( 추상화를 통해 )
- 함수형 프로그래밍 지향 ( 깔끔하고, 테스팅 하기 쉬움 )
