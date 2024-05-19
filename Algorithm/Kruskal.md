Kruskal

# 소개
- 그리디를 활용
- 네트워크의 모든 정점을 최소 비용으로 연결하는 최적 해답 도출
- Kruskal Algorithm을 활용하여 MST 획득
# 동작 과정
1. 그래프의 간선들을 가중치의 오름차순으로 정렬
2. 정렬된 간선 리스트에서 순서대로 사이클을 형성 하지 않도록 간선을 선택
	- 가장 낮은 가중치를 선택하면 됨
	- 사이클을 형성하는 간선을 제외하면 됨
3. 선택된 간선을 현재의 MST 집합에 추가
# 구체적인 동작 과정
- **간선 선택을 기반**으로 하는 알고리즘
- 이전 단계에서 선택한 신장 트리와 상관없이 무조건 최소 간선만을 선택(greedy니깐)
![[Pasted image 20240503131029.png]]
주의점
- 다음 간선을 MST집합에 추가할 때 사이클 생성되는지 체크!
	- 추가될 선택된 간선의 양 끝 정점이 이미 MST집합에 속해 있으면 사이클이 형성됨
- 사이클 여부 확인 하는 방법
	- 선택된 간선의 양 끝 정점이 같은 집합에 속해 있는지를 검사
	- union - find Algorithm 활용
# Java Code
```java
import java.util.*;

class Edge implements Comparable<Edge> {
    int src, dest, weight;

    public Edge(int src, int dest, int weight) {
        this.src = src;
        this.dest = dest;
        this.weight = weight;
    }

    @Override
    public int compareTo(Edge other) {
        return this.weight - other.weight;
    }
}

class Graph {
    int V, E;
    Edge[] edges;

    public Graph(int V, int E) {
        this.V = V;
        this.E = E;
        edges = new Edge[E];
    }
}

class Kruskal {
    int V, E;
    Graph graph;

    public Kruskal(int V, int E) {
        this.V = V;
        this.E = E;
        graph = new Graph(V, E);
    }

    int find(int[] parent, int i) {
        if (parent[i] == -1)
            return i;
        return find(parent, parent[i]);
    }

    void union(int[] parent, int x, int y) {
        int xset = find(parent, x);
        int yset = find(parent, y);
        parent[xset] = yset;
    }

    void kruskalMST() {
        Edge result[] = new Edge[V]; // Array to store the resultant MST
        int e = 0; // An index variable, used for result[]
        int i = 0; // An index variable, used for sorted edges
        Arrays.sort(graph.edges);

        int parent[] = new int[V];

        Arrays.fill(parent, -1);

        while (e < V - 1 && i < graph.E) {
            Edge next_edge = graph.edges[i++];

            int x = find(parent, next_edge.src);
            int y = find(parent, next_edge.dest);

            if (x != y) {
                result[e++] = next_edge;
                union(parent, x, y);
            }
        }

        System.out.println("Following are the edges in the constructed MST");
        for (i = 0; i < e; ++i)
            System.out.println(result[i].src + " -- " + result[i].dest + " == " + result[i].weight);
    }

    public static void main(String[] args) {
        int V = 4; // Number of vertices in graph
        int E = 5; // Number of edges in graph
        Kruskal kruskal = new Kruskal(V, E);

        // add edge 0-1
        kruskal.graph.edges[0] = new Edge(0, 1, 10);

        // add edge 0-2
        kruskal.graph.edges[1] = new Edge(0, 2, 6);

        // add edge 0-3
        kruskal.graph.edges[2] = new Edge(0, 3, 5);

        // add edge 1-3
        kruskal.graph.edges[3] = new Edge(1, 3, 15);

        // add edge 2-3
        kruskal.graph.edges[4] = new Edge(2, 3, 4);

        kruskal.kruskalMST();
    }
}

```
# 참고
- [블로그](https://gmlwjd9405.github.io/2018/08/29/algorithm-kruskal-mst.html)
- 코드는 chatGPT