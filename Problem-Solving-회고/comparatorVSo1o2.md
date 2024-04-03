return o2 - o1;의 치명적 약점
> https://www.acmicpc.net/problem/7662
## 회고
2개의 우선순위큐와 1개의 맵을 활용했다. 시작방향은 맞았지만, 중간에서 틀림. 맵을 활용해서 카운팅한다는 개념이 새로웠다.
주어지는 값이 INTEGER_MAX, INTEGER_MIN 까지 주어진다. 이때
```java
PriorityQueue<Integer> maxQ = new PriorityQueue<>((o1,o2)->{
	return o2-o1;
});
```
이런 코드를 사용해서 내림차순큐를 구현했는데 만약에 o2 = INTEGER_MAX이고 o1이 INTEGER_MIN이면 오버플로가 발생해서 의도하지 않은 결과가 나오는것!!! 안전하게
```java
PriorityQueue<Integer> maxQ = new PriorityQueue<>(Comparator.reverseOrder());
```
이렇게 작성하거나
```java
PriorityQueue<Integer> maxQ = new PriorityQueue<>((o1,o2)->{
	if(o1>o2){
	}else{
	}
});
```
이렇게 꼭 if문으로 대소를 비교하자!!!