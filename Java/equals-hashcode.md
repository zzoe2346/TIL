# Java의 equals(), hashCode(), Objects Class(Set 오버라이딩시 equals(),hashcode()를 둘다 해야야되는 이유)

```java
@Override public int hashCode() { 

	return Objects.hash(a,b,c); // name 필드의 해시코드를 반환한다. 

}
```
 - Objects.hash() 는 hash코드 생성해줌. native활용
- hashMap, hashSet 등의 hash를 이용하는 자료구조는 hashcode() 일치여부->equal() 일치여부 순서로 같은 객체인지 확인한다. 

## Reference
- https://docs.oracle.com/javase/8/docs/api/java/util/Objects.html
- https://youtu.be/Go-Yf09xxzQ?si=3jkHE1i_U1c0JerC
- https://inpa.tistory.com/entry/JAVA-%E2%98%95-equals-hashCode-%EB%A9%94%EC%84%9C%EB%93%9C-%EA%B0%9C%EB%85%90-%ED%99%9C%EC%9A%A9-%ED%8C%8C%ED%97%A4%EC%B9%98%EA%B8%B0