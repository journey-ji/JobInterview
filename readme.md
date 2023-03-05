# 해당 레포는 프론트엔드 개발자 면접에 관한 공부를 하기위해 개설된 레포입니다.


## 질문 리스트
1. ㄹㅁㄷㅈㄹ






### 1. This가 무엇인가요?
일반적으로 자신을 호출한 객체를 의미합니다.
this의 값이 결정되는 시기 : 실행될 때 ! 

아래의 예시를 참고하여 보겠습니다.
```js
const person = {
    name: 'Journey',
    age: 28,
    a(){
        // 여기에서 this는 person을 가리킵니다. 
        console.log(this);
        console.log(this.name);
        function b() {
            // 하지만 이와 같이 한단계 더 내부에 있는 함수의 경우 this는 따로 명시되지 않게 됩니다. 따라서 window를 가리키게 됩니다.
            console.log(this);
            console.log(this.name);
            function c() {
                // b 와 동일한 이유로 window를 가리키게 됩니다.
                console.log(this);
                console.log(this.name);
            }
            c()
        }
        b()
    }
}
person.a()

//출력시 아래와 같습니다.
{name: 'hojun', age: 25, a: ƒ}
hojun

Window {window: Window, self: Window, document: document, name: '', location: Location, …}
''

Window {window: Window, self: Window, document: document, name: '', location: Location, …}
''
```

하지만 narrow function에서는 ??


```js
const person = {
    name: 'Journey',
    age: 28,
    a(){
        // 여기에서 this는 person을 가리킵니다. 
        console.log(this);
        console.log(this.name);
        const b = () =>{
            // 화살표 함수에서는 this가 자동적으로 상위스코프를 참조하게 됩니다.
            // 따라서 person을 가리킵니다.
            console.log(this);
            console.log(this.name);
            const c = () =>{
                // b 와 동일합니다.
                console.log(this);
                console.log(this.name);
            }
            c()
        }
        b()
    }
}
person.a()
```



bind, call, apply ?
위 세가지 함수를 통해 this 가 가리키는것을 바꿔줄 수 있습니다.



### 2. CallStack 이 무엇인가요 ? 
해야할 일의 목록 혹은 순서라고 보면 됩니다.
우리는 처리해야 할 일(함수)은 스택형식으로 처리됩니다. FILO or LIFO 순서를 가집니다.
우선 가장 main 함수를 콜스택에 넣음과 동시에 다시 뺍니다. 일을 처리해야 하니까요.
그렇게 main 일을 처리하다가보면 안에서 또 다른 함수를 만나게 됩니다.
그러면 처리하던 main 함수를 일시중단하고 다시 넣죠.
그리고 Main 함수 안에 조우한 새로운 함수를 넣었다가 다시 뺍니다.(그 함수를 처리하기 위해서요)
해당 함수를 다 처리하면 다시 main을 꺼내 작업을 합니다.
이러한 과정을 통해 작업을 처리하도록 하는 것이 콜스택입니다.

크롬 브라우저의 개발자도구를 통해 디버깅을 하다보면 자주 확인하게되는 칸입니다.


### 3. Closure 가 무엇인가요 ?
클로져 : 중첩함수가 존재할 때, 내부의 중첩함수가 외부함수(상위 스코프)를 참조하면서 그보다 오래 살아있을 경우에 내부 중첩함수를 클로져라고 합니다.

