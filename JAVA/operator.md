[돌아가기](README.md)
# 연산자(operator)

연산을 수행하는 기호

→ `+` `-` `*` `/` `%` ...

# 피 연산자(operand)

연산자의 작업 대상

→ 변수, 상수, 리터럴, 수식 ...

## 연산자 종류

- 산술 연산자

    `+` `-` `*` `/` `%` `<<` `>>`

- 비교 연산자

    `>` `<` `>=` `<=` `==` `!=`

- 논리 연산자

    `&&` `||` `!` `&` `|` `^` `~`

- 대입 연산자

    `=`

- 기타

    `(type)` `? :` `instanceof`

## 증감 연산자

- `++`

    피 연산자에 저장된 값을 1 증가시킴

- `--`

    피 연산자에 저장된 값을 1 감소시킴

### prefix (전위)

피 연산자의 앞에 붙는다; 피 연산자 값이 참조되기 전에 증감 연산을 수행

### postfix (후위)

피 연산자의 뒤에 붙는다; 피 연산자 값이 참조된 후에 증감 연산을 수행

# 문자열의 비교

### ==

`==` 연산자는 피 연산자의 값이 같은지 비교한다.

→ 비교 하는 피 연산자의 타입이 다르다면 캐스팅 후에 비교를 진행

e.g.,

'0' == 0 ⇒ 48 == 0 ⇒ `false`

'A' == 0 ⇒ 65 == 0 ⇒ `true`

### String.equals(String)

두 문자열의 값을 비교하기 위해서 사용 되는 메소드

e.g.,

```jsx
String a = "cheese";
String b = new String("cheese");

boolean x = (a == b); // false
boolean y = a.equals(b); // true
```

String 객체에 리터럴로 대입된 문자열과 `new` 키워드로 새로 생성된 String 객체는 `==` 로 비교 불가능
