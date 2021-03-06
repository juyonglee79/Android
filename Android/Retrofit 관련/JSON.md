# JSON

## 1. JSON이란?

- JavaScript Object Notation라는 의미의 축약어로 데이터를 저장하거나 전송할 때 많이 사용되는 **경량의 DATA 교환 형식**

- Javascript에서 객체를 만들 때 사용하는 표현식을 의미한다.

- JSON 표현식은 사람과 기계 모두 이해하기 쉬우며 용량이 작아서, 최근에는 JSON이 XML을 대체해서 데이터 전송 등에 많이 사용한다.

- JSON은 데이터 포맷일 뿐이며 어떠한 통신 방법도, 프로그래밍 문법도 아닌 단순히 데이터를 표시하는 표현 방법일 뿐이다.

  

## 2. JSON 구조

JSON은 자바스크립트의 객체 표기법으로부터 파생된 부분 집합이다.

따라서 JSON 데이터는 다음과 같은 자바스크립트 객체 표기법에 따른 구조로 구성된다.

- JSON 데이터는 이름과 값의 쌍으로 이루어집니다.

- JSON 데이터는 쉼표(,)로 나열됩니다.

- 객체(object)는 중괄호({})로 둘러쌓아 표현합니다.

- 배열(array)은 대괄호([])로 둘러쌓아 표현합니다.

  

### 2.1  JSON 데이터

JSON 데이터는 이름과 값의 쌍으로 구성된다.

이러한 JSON 데이터는 데이터 이름, 콜론(:), 값의 순서로 구성된다.

##### 문법

```json
"데이터이름": 값
```

 

다음 예제는 데이터의 이름이 "name"이고, 값은 "식빵"이라는 문자열을 갖는 JSON 데이터의 예제입니다.

##### 예제

```json
"name": "식빵"
```

데이터의 이름도 문자열이므로, 항상 큰따옴표("")와 함께 입력해야 합니다.



데이터의 값으로는 다음과 같은 타입이 올 수 있다.

1.  숫자(number)
2. 문자열(string)
3. 불리언(boolean)
4. 객체(object)
5. 배열(array)
6. NULL

### 2.1  JSON 객체

JSON 객체는 중괄호({})로 둘러쌓아 표현한다.

또한, JSON 객체는 쉼표(,)를 사용하여 여러 프로퍼티를 포함할 수 있다.



##### 예제

```json
{
    "name": "식빵",
    "family": "웰시코기",
    "age": 1,
    "weight": 2.14
}
```



JSON 객체를 그림으로 표현하면 아래와 같다.

![1591679493759](C:\Users\user\AppData\Roaming\Typora\typora-user-images\1591679493759.png)



### 2.1  JSON 배열

JSON 배열은 대괄호([])로 둘러쌓아 표현한다.

또한, JSON 배열은 쉼표(,)를 사용하여 여러 JSON 데이터를 포함할 수 있다.

 



##### 예제

```json
"dog": [
    {"name": "식빵", "family": "웰시코기", "age": 1, "weight": 2.14},
    {"name": "콩콩", "family": "포메라니안", "age": 3, "weight": 2.5},
    {"name": "젤리", "family": "푸들", "age": 7, "weight": 3.1}
]
```

 배열의 이름이 "dog"이고, 3개의 JSON 객체를 요소로 가지는 JSON 배열이다.



JSON 배열을 그림으로 나타내면 아래와 같다.

![1591679625464](C:\Users\user\AppData\Roaming\Typora\typora-user-images\1591679625464.png)



## 3. 기타

### 3.1  객체 안의 객체

JSON에서 데이터 이름과 대응되는 값으로 숫자, 문자열, 불리언뿐만 아니라 또 다른 객체가 올 수도 있다.

만약 데이터의 값이 객체라면 객체 안에 객체가 포함되는 계층 구조가 형성된다.

 

##### 예제

```json
{
    "dog": {
        "name": "식빵",
        "family": "웰시코기",
        "age": 1,
        "weight": 2.14,
        "owner": {
            "ownerName": "홍길동",
            "phone": "01012345678"
        }
    }
}
```

 위의 예제에서 가장 상위 계층의 데이터 이름은 "dog"이며, 데이터값으로 다섯 개의 또 다른 데이터를 가지고 있다.

그중에서 다섯 번째 데이터인 "owner" 객체는 "ownerName"과 "phone"이라는 또 다른 데이터를 가지고 있다.



### 3.2  배열과 객체의 차이점

JSON에서 배열과 객체는 여러 데이터를 묶어놓은 집합이라는 점에서 서로 비슷한 타입이다.

하지만 객체는 프로퍼티의 집합이며, 배열은 데이터값의 집합이라는 차이가 있다.

 

##### 예제

```json
{
    "dog": [
        "웰시코기",
        "포메라니안",
        "푸들",
        {
            "ownerName": "홍길동",
            "phone": "01012345678"
        }
    ]
}
```

위의 예제에서 "dog"라는 이름의 JSON 배열은 문자열뿐만 아니라 객체도 요소로 가지고 있다.

 

대부분의 프로그래밍 언어에서 배열은 여러 타입의 데이터를 동시에 가질 수 없다.

하지만 자바스크립트 기반의 JSON 배열은 **여러 타입의 배열 요소를 가질 수 있다**.