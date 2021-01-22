[돌아가기](./README.md)

# Interface 변화

### 이전

- public abstract method

### Java 8

- public abstract method
- static method
- default method

```jsx
public interface Animal {
		void run();
		static void cry() {
				System.out.println("YEE");
		}
}
```

```jsx
Animal.cry(); // YEE
```

→ static method와 default method가 추가되었기 때문에, 

더 이상 추상 클래스에서 default method를 만들 필요가 없어짐

# Method referencing

### static & instance method

`ContainingClass`::`methodName` 형태를 통해 기존 lambda의 메서드 참조를 더욱 짧게 함

```jsx
Product[] result = Arrays.stream(products)
												.filter(product->Product.isValid(product))
												.toArray(size->new Product[size]);
```

```jsx
Product[] result = Arrays.stream(products)
												.filter(Product::isValid)
												.toArray(size->new Product[size]);
```

### 생성자

`ClassName`::`new` 형태를 통해 생성자를 나타냄

```jsx
Product[] result = Arrays.stream(products)
												.filter(Product::isValid)
												.toArray(Product::new);
```

# Optional

Java 8에 등장한, NullPointerException 극복을 위한 것

기존의 불필요한 null 검사 로직을 줄여줄 수 있다

```jsx
List<Integer> intList = getIntList();
List<Integer> intListOpt = intList != null? intList: new ArrayList<>();
```

```jsx
List<Integer> intListOpt = getIntList().orElseGet(() -> new ArrayList<>());
```

```jsx
Product product = getProduct();
if (product != null) {
		String isbn = product.getIsbn();
		if (isbn != null)
				return isbn;
}
return "not found";
```

```jsx
Optional<Product> product = Optional.ofNullable(getProduct());
String result = product.map(Product::getIsbn).orElse("not found");
```
