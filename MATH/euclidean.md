[돌아가기](./README.md)

# 유클리드 호제

최대 공약수 구하는 방법

1. 어떤 두 수 a, b (단, a > b)
2. a % b = r (r > 0)
3. a = b, b = r
4. r=0이 될 때까지 2, 3번 반복
5. r=0이 되는 b가 최대 공약수

e.g., a=150, b=120

⇒ 150 % 120 = 30 (r = 30)

⇒ 120 % 30 = 0 (r = 0)

그러므로, 최대 공약수는 (b=30)

**Java**

```java
int gcm(int a, int b) {
	if (a%b==0) return b;
	return gcm(b, a%b);
}
```

# 확장된 유클리드 호제

`ax + by = gcd(a, b)` 에 대해, `gcd(a, b)`와 `x`, `y`를 동시에 구하는 것

