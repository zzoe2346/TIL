# Union-Find
>https://www.acmicpc.net/problem/1717

>https://www.acmicpc.net/problem/1976

## 회고
이 알고리즘을 몰라서 계속 시간초과와 메모리초과에 시달리다가 이 알고리즘으로 이 문제들로 부터 해방되었다.
## Code
```java
static int getParent(int[] parents,int x){  
    if(parents[x]==x) return x;  
    else{  
	//이 부분이 잘 이해가 안되었었다. 
	//그냥 아래 2줄을 return getParent(parents,parents[x]);로 하면 시간초과가 발생한다.
	//getParent()메서드가 한번 훝은 부분을 또 훝는것이기 때문
	//어차피 루트노드만 같은지 판단하는게 핵심이기 때문에 parents[x] = getParent(parents,parents[x]) 이 코드로 갱신 시키는게 시간복잡도 측면에서 매우 유리하고 당연한것!!!
        parents[x] = getParent(parents,parents[x]);  
        return parents[x];  
    }  
}
static void union(int[] parents,int a, int b){  
    a = getParent(parents, a);  
    b = getParent(parents, b);  
    if(a == b) return;  
    if(a<b){  
        parents[b] = a;  
    }else {  
        parents[a] = b;  
    }  
  
}  
static boolean find(int[] parents,int a, int b){  
    a = getParent(parents, a);  
    b = getParent(parents, b);  
    if(a == b) return true;  
    else return false;  
}
```

## Reference
- https://ip99202.github.io/posts/%EC%9C%A0%EB%8B%88%EC%98%A8-%ED%8C%8C%EC%9D%B8%EB%93%9C(Union-Find)/