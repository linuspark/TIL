# 트리(Tree)

그래프(graph)의 일종으로 여러 노드가 한 노드를 가르킬 수 없는 구조. 간단하게는 회로가 없고, 서로 다른 두 노드를 잇는 길이 하나뿐인 그래프.

트리에서 탐색(Search)하는 것은 선형 구조인 배열이나 연결 리스트와 같은 구조에서 탐색하는 것 보다 훨씬 까다롭고 어렵다. 또한 최악의 수행시간과 평균적인 수행 시간이 매우 크게 바뀔 수 있기 때문에 알고리즘을 살필 때에는 항상 그 두 가지를 모두 살펴야 한다. 

![wikiTreeImg](https://upload.wikimedia.org/wikipedia/commons/thumb/5/5f/Tree_%28computer_science%29.svg/440px-Tree_%28computer_science%29.svg.png)

트리는 노드로 이루어진 자료구조 이다. 

- 최 상위 노드를 루트노드(Root Node, 뿌리노드)라고 한다.
- 한 노드가 다른 노드를 가르킬 때 가르키는 노드는 부모노드(Parent Node) 가리켜 지는 노드는 자식노드(Child Node) 라고 한다.
- 자식 노드가 없는 노드를 잎 노드(Leaf Node, 리프노드) 또는 단말노드(Terminal Node) 라고 하고 잎 노드가 아닌 노드를 내부노드(Internal Node) 또는 비단말노드라고 한다.

```csharp
class Node {
	public String Name;
	public Node[] children;
}
```

트리를 이해하기 위한 (재귀적) 설명

- 트리는 하나의 루트 노드를 갖는다.
- 루트 노드는 0개 이상의 자식 노드를 가지고 있다.
- 그 자식 노드 또한 0개 이상의 자식 노드를 가지고 있고 이는 반복적으로 정의된다.

# 트리의 종류

## 이진 트리 (Binary Tree)

각 노드가 최대 두 개의 자식 노드를 가지는 트리. 각각 왼쪽 자식, 오른쪽 자식 이라고 한다. 모든 트리가 이진트리는 아니다.

## 이진 탐색 트리(Binary Search Tree)

이진 탐색 트리는 모든 노드가 다음과 같은 특징을 가진 이진 트리를 말한다.

- '모든 왼쪽 자식들 ≤ N(현재 노드의 값) ≤ 모든 오른쪽 자식들'

이 때 "모든 왼쪽/오른쪽 자식들" 이라는 것은 바로 아래 자식 뿐만 아니라 내 밑에 있는 모든 자식 노드 들에 대하여 이 부등호가 성립해야 한다. (내 왼쪽 손자 노드가 나 보다 큰 값이면 안된다)

## 균형 트리

트리가 균형이 잡혀 있다 라는 말은 한 쪽으로 트리가 치우쳐져 있지 않는다. 라는 의미이며 조금 더 나아가서는 O(log N) 시간에 insert와 find를 할 수 있을 정도가 된다는 말과 같다.

대표적인 균형 트리는 레드-블랙 트리와 [AVL 트리](./AVLTree.md)가 있다.

## 완전 이진 트리(Complete Binary Tree)

트리의 모든 높이에서 노드가 꽉 차있는 이진 트리. 마지막 노드에서는 꽉 차 있지 않아도 되지만 노드가 왼쪽에서 오른쪽으로 채워져야 한다.

즉, 마지막 레벨을 제외하고 모든 레벨이 완전히 채워져 있으며 마지막 레벨의 노드들은 가능한 모두 왼쪽에 있다. 마지막 레벨을 h라고 할 때 마지막 레벨의 노드들은 1개부터 2^h-1개가 존재할 수 있다. 

## 전 이진 트리(Full Binary Tree)

모든 노드가 0개 또는 2개의 자식 노드를 가지고 있는 트리이다. 즉, 자식이 1개만 있는 노드가 없다.

## 포화 이진 트리(Perfect Binary Tree)

완전 이진 트리 이면서 전 이진 트리인 경우 포화 이진 트리라고 말 할 수 있다. 모든 잎 노드는 같은 레벨에 있으며 마지막 레벨의 노드가 2^(h-1)개 존재한다 (h 는 높이).

# 이진 트리 순회

여기서 이야기 하는 순회란 노드에 방문하여 해당 노드의 값을 읽는 순서를 이야기 한다. 이 때 방문이란 알고리즘에 따라서 특정 알고리즘을 처리하는 순서가 될 수 있다. 

![https://upload.wikimedia.org/wikipedia/commons/6/67/Sorted_binary_tree.svg](https://upload.wikimedia.org/wikipedia/commons/6/67/Sorted_binary_tree.svg)

## 중위 순회

중위 순회(in-order traversal)란 **왼쪽 가지 → 현재 노드 → 오른쪽 가지** 의 순서로 노드를 방문하는 방법을 말한다.

```csharp
void InOrderTraversal(Node node) {
	if (node == null) return;
	InOrderTraversal(node.left);
	visit(node);
	InOrderTraversal(node.right);
}
```

## 전위 순회

전위 순회(pre-order traversal)란 자식 노드에 방문하기 전에 현재 노드를 먼저 방문하는 방법을 이야기 한다.

```csharp
void PreOrderTraversal(Node node) {
	if (node == null) return;
	visit(node);
	InOrderTraversal(node.left);
	InOrderTraversal(node.right);
}
```

전위 순회에서는 항상 루트 노드를 먼저 방문한다.

## 후위 순회

후위 순회(post-order traversal)란 모든 자식 노드를 먼저 방문한 뒤에 마지막에 현재 노드를 방문하는 방법을 이야기한다.

```csharp
void PostOrderTraversal(Node node) {
	if (node == null) return;
	InOrderTraversal(node.left);
	InOrderTraversal(node.right);
	visit(node);
}
```

후위 순회에서는 항상 루트 노드를 마지막에 방문하게 된다.

# 그래프

![https://upload.wikimedia.org/wikipedia/commons/5/5b/6n-graf.svg](https://upload.wikimedia.org/wikipedia/commons/5/5b/6n-graf.svg)

노드와 노드를 연결하는 간선(edge)을 하나로 모아 놓은 것. 트리도 그래프의 일종이다. 

트리는 그래프라고 할 수 있지만 모든 그래프는 트리가 아니다. 즉, 사이클(cycle)이 없는 하나의 연결그래프가 트리라고 부를 수 있다.

- 모든 노드간에 경로가 존재하는 그래프를 '연결그래프' 라고 한다.
- 그래프에는 방향성이 있는 경우(방향그래프;directed graph)와 방향성이 없는 경우(무방향 그래프;undirected graph) 가 있다.
- 그래프에는 사이클(cycle)이 존재할 수도 있고 존재하지 않을 수 도(비순환 그래프) 있다.

## 인접 리스트

프로그래밍 관점에서 그래프를 표현하는 대표적인 방법.

모든 노드를 리스트에 저장하고 각 노드는 자신이 인접한 노드를 가리킨다. 코드로 보면 다음과 같다.

```csharp
public class Graph{
	public Node[] nodes;
}
public class Node{
	public string name;
	public Node[] children;
}
```

Node 가 표현하는 것은 Tree에서의 구현과 별 반 다를 바가 없다. 하지만 여기서 차이점은 Tree의 경우 Root Node를 알고 있으면 모든 Node에 접근 할 수 있었지만 Graph에서는 그렇지 않을 수 있기 때문에 Graph라는 클래스에서 모든 Node를 가지고 있어야 한다는 점이다.

무방향 그래프의 경우 간선(edge)는 두 번 저장된다. A ←→ B 의 경우 A Node의 Children에도 B가 저장되고 B Node의 Children에도 A가 저장된다.

위와 같이 노드에 관한 클래스를 따로 정의하지 않고 연결 리스트 등을 이용하여 표현할 수 있다.

위 그래프 이미지를 연결 리스트 등으로 표현하면 다음과 같이 표현할 수 있다.

- [1] → 2, 5
- [2] → 1, 3, 5
- [3] → 2, 4
- [4] → 3, 5, 6
- [5] → 1, 2, 4
- [6] → 4

## 인접행렬

N x N 행렬을 이용하여 그래프를 표현하는 방법. (N은 노드의 개수)

matrix[i][j] 에서 i 번째 노드에서 j 번째 노드로 간선이 있다면 true로 표기하는 방식이다. (boolean을 사용하던 int를 사용하던 상관은 없다.)

만약 무방향 그래프를 인접행렬로 표현한다면 행렬은 대칭행렬이 된다.

- 장점: N x N 의 매트릭스를 이용하기 때문에 구현이 쉽다. 노드 i와 j의 연결을 확인할 때 O(1) 만에 확인이 가능하다.
- 단점: 노드 i 에 연결된 노드를 찾기 위해 O(N)의 시간이 걸린다.

## 그래프 탐색

![https://upload.wikimedia.org/wikipedia/commons/thumb/8/89/4-tournament.svg/250px-4-tournament.svg.png](https://upload.wikimedia.org/wikipedia/commons/thumb/8/89/4-tournament.svg/250px-4-tournament.svg.png)

그래프를 탐색하는 일반적인 두 가지 방법으로는 깊이 우선 탐색(depth-first search)과 너비 우선 탐색(breadth-first search)가 있다. 

### 깊이 우선 탐색(Depth First Search)

깊이 우선 탐색(DFS)는 루트 노드에서 시작하여 다른 분기(branch)로 넘어가기 전에 해당 분기(branch)를 먼저 완벽하게 탐색하는 방법이다. 말 그래도 넓게 알기 보다 깊게 아는 것 먼저 한다는 뜻이다

위 예시로 나온 그래프를 깊이 우선 탐색을 한다고 생각하면 1번 노드를 시작 노드로 할 때 다음과 같은 순서로 Node를 탐색할 것이다.

Node 1 → Node 2 → Node 4 → Node 3

깊이 우선 탐색은 주로 그래프의 모든 노드를 탐색하고자 할 때 선호되는 사용법 이다. 너비 우선 탐색이 모든 노드를 탐색하지 못 하는 것은 아지지만 간단한 구현과 직관적인 방법이기 때문에 너비 우선 탐색 보다 선호된다. 

```csharp
void Search(Node root){
	if (root == null) return;
	visit(root);
	root.visited = true;
	foreach (var node in root.children){
		if (node.visited == false){
			Search(node);
		}
	}
}	
```

DFS 의 구현에서 가장 중요한 점은 어떤 노드를 방문했었는지에 대한 여부를 확인하는 것(node.visited=true) 이다. 노드의 방문 여부를 체크하지 않으면 무한 루프에 빠질 수 있기 때문이다. 

### 너비 우선 탐색(Breadth First Search)

너비 우선 탐색(BFS)는 루트 노드에서 시작하여 인접한 노드를 먼저 탐색하는 방법을 이야기 한다. 말 그대로 깊게 알기 전에 넓게 아는 것이 목적이다.

너비 우선 탐색은 주로 최단 경로, 혹은 임의의 경로를 찾고자 할 때 사용된다. 예를 들어 지구상의 모든 친구관계를 그래프로 표현한 뒤에 철수와 영희 사이에 존재하는 경로를 찾는 경우를 생각해 본다면 깊이 우선 탐색보다 너비 우선 탐색이 왜 더 선호되는지 알 수 있다. 만약 이 문제에서 깊이 우선 탐색을 사용한다면 지구상의 모든 친구관계를 탐색해야 할 수도 있다.

```csharp
void Search(Node root){
	Queue queue = new Queue();
	root.marked = true;
	queue.enqueue(root);
	
	while(!queue.IsEmpty()){
		Node r = queue.dequeue();
		visit(r);
		foreach(var node in r.children()){
			if (node.marked == false){
				node.marked = true;
				queue.enqueue(node);
			}
		}
	}
}
```

BFS는 재귀함수를 사용하지 않고 Queue를 이용하여 구현한다.

### 양방향 탐색(Bidirectional Search)

출발지와 도착지 사이의 최단 경로를 찾기 위해 사용되는 알고리즘이다. 기본적으로 출발지와 도착지를 중심으로 하여 너비 우선 탐색을 각각 수행하고 탐색 지점이 겹치는 경로를 찾는 방식이다.

양방향 탐색이 왜 더 빠른 탐색이라고 하는지 다음과 같은 예시를 보아서 알 수 있다.

모든 노드가 적어도 k개의 인접한 노드를 가지고 있다고 할 때 노드 s에서 노드 t까지의 최단 거리가 d 이다. 이 때 너비 우선 탐색을 사용할 경우 각 노드마다 k 번씩 탐색을 최단거리 d 만큼 수행해야 한다. 즉 O(K^d) 만큼의 시간이 걸린다. 양방향 탐색을 사용할 경우 각 노드마다 k 번씩 탐색을 d/2 만큼 수행할 것이다. 즉 O(K^(d/2)) 만큼의 시간이 걸린다.

---

참고. 게일 라크만 맥도웰. 코딩 인터뷰 완전분석 (이창현 옮김) 

참고. "트리구조", Wikipedia

참고. "그래프", Wikipedia
