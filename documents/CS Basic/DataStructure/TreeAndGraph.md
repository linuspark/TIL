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

대표적인 균형 트리는 레드-블랙 트리와 AVL 트리가 있다.

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
