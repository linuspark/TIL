# Red-Black Tree

AVL 트리와 마찬가지로 자가 균형 이진 트리이다. 자료구조로써 복잡한 편에 속하지만 실 사용에 효율적이고 최악의 상황에서도 우수한 실행시간을 보이기 때문에 잘 사용된다.

레드-블랙 트리는 이진 탐색 트리(BST)를 기반으로 하며 아주 엄격하게 균형을 잡지는 않지만 탐색(Search), 삽입(Insert), 삭제(Delete) 등의 연산을 충분히 O(log N)의 시간에 수행할 수 있음을 보장한다.  

거의 번갈아 가면서 빨간색과 검은색 노드를 가지고 있어 레드-블랙 트리 라고 이름붙여졌으며 어떤 노드 부터 단말 노드(리프노드) 까지의 경로에 있는 모든 검은색 노드의 개수가 같다. 이렇게 되면 **꽤 균형잡힌** 트리가 된다.

![https://upload.wikimedia.org/wikipedia/commons/thumb/6/66/Red-black_tree_example.svg/800px-Red-black_tree_example.svg.png](https://upload.wikimedia.org/wikipedia/commons/thumb/6/66/Red-black_tree_example.svg/800px-Red-black_tree_example.svg.png)

# 특성(속성)

1. 노드는 **레드(Red)** 혹은 **블랙(Black)** 중의 한 가지 색을 가진다.
2. 루트노드는 블랙이다.
3. 모든 단말노드(NIL)는 블랙이다.(일반적인 단말노드와 다르다)
4. 레드 노드의 자식은 모두 블랙이다.(레드 노드의 자식으로 레드 노드가 있을 수 없다. / 블랙 노드는 블랙노드를 자식으로 가질 수 있다.)
5. 특정 노드부터 그에 속한 하위 리프 노드에 도달하는 모든 경로에는 같은 개수의 블랙 노드가 있다.

## 균형

위 레드-블랙 트리의 특성 때문에 레드-블랙 트리는 거의 균형이 잡혔다고(Roughly Balenced) 볼 수 있다. 루트 노드에서 가장 가까운 리프노드까지의 경로(A)와 가장 먼 리프노드 까지의 경로(B)가 항상 두 배 보다 적게 차이가 나기 때문이다. (2A > B)

4번째 속성에 따라 레드 노드는 한 경로에서 인접해서 있을 수 없다. 즉, 어떤 경로에서든 레드 노드는 경로상 노드의 절반 보다 적게 있어야 한다. 

5번째 속성에 따라 어떤 경로에서든 블랙 노드의 개수는 항상 같아야 한다. 

이 때 두 가지 특성에 따라 가장 가까운 리프 노드 까지의 거리(A)와 가장 먼 리프 노드 까지의 경로(B)를 생각해 본다면 가장 가까운 리프 노드 까지의 거리에는 블랙노드만 있는 경우가 되고 가장 먼 리프노드 까지의 거리는 최대한 많은 레드노드가 있는 경우, 즉 레드노드와 블랙 노드의 개수가 같은 경우이다.

리프노드 까지의 블랙 노드 개수를 b 라고 할 때,

1. (A) 의 경우 경로의 길이는 b 가 된다.
2. (B) 의 경우 경로의 길이는 2b 가 된다.

즉, 최악의 경우에도 경로의 차이가 2배 보다 많지 않게 된다. 이런 성질의 의미는 최악의 경우에도 검색, 삽입의 연산이 O(log N) 에 가능하다는 의미가 된다.

# 삽입연산

일반적인 이진 탐색 트리(BST)의 삽입으로 시작한다. 단말노드에 삽입(NIL 노트와 교체)

새로운 노드는 항상 레드 노드이다. (새로운 노드가 삽입되면 그 자식노드로 단말노드 NIL 이 생긴다)

이 후 레드-블랙 트리의 속성을 위반하지 않도록 고쳐나간다.

레드-블랙 트리의 속성을 위반하는 경우는 2가지가 있다.

1. 레드 노드의 연속성 위반.

    레드 노드의 자식으로 레드노드가 존재하는 경우

2. 블랙 노드의 개수 위반

    단말 노드 까지의 경로에 블랙 노드의 개수가 다른 경우

새로 추가된 노드는 레드 노드 이기 때문에 경로상 블랙 노드의 개수에는 변함이 없다.

레드 노드가 연속되어 있는 연속성 위반일 경우 새로 추가된 노드(N)의 부모노드(P)는 레드 노드가 된다. 또한 레드 노드의 조부모 노드(G)는 블랙 노드가 된다.(기존에 레드-블랙 트리의 속성을 만족하므로)

여기서 가능성을 나누어본다.

- 삼촌 노드(U)의 색이 레드/블랙
- 삼촌 노드(U)이 왼쪽/오른쪽 자식인 경우
- 새로운 노드(N)이 왼쪽/오른쪽 자식인 경우

1. 삼촌 노드가 레드 노드일 경우

    ![https://upload.wikimedia.org/wikipedia/commons/c/c8/Red-black_tree_insert_case_3.png](https://upload.wikimedia.org/wikipedia/commons/c/c8/Red-black_tree_insert_case_3.png)

    부모노드(P), 삼촌노드(U), 조부모노드(G)의 색을 반전시킨다. 

    만약 조부모 노드의 부모노드가 레드노드일 경우 이 과정을 재귀적으로 수행한다.

2. 삼촌 노드가 블랙 노드일 경우

    여기선 다시 4가지를 고려해야 한다.

    - 삼촌 노드(U)가 왼쪽 / 오른쪽 자식인 경우,
    - 새로운 노드(N)가 왼쪽 / 오른쪽 자식인 경우

    삼촌 노드가 왼쪽/오른쪽인 경우는 서로 대칭되므로 삼촌 노드가 오른쪽 자식인 경우만 생각해 본다.

    a. 새로운 노드(N)가 왼쪽 자식인 경우

    트리를 왼쪽으로 회전시킨다.

    ![https://upload.wikimedia.org/wikipedia/commons/6/66/Red-black_tree_insert_case_5.png](https://upload.wikimedia.org/wikipedia/commons/6/66/Red-black_tree_insert_case_5.png)

    회전을 함으로써 레드 블랙 트리의 속성을 만족시킬 수 있다.

    b. 새로운 노드(N)가 오른쪽 자식일 경우

    부모노드(P)와 새로운 노드(N)을 오른쪽 회전 시킨다.

    ![https://upload.wikimedia.org/wikipedia/commons/5/56/Red-black_tree_insert_case_4.png](https://upload.wikimedia.org/wikipedia/commons/5/56/Red-black_tree_insert_case_4.png)

    이 후, "a. 새로운 노드(N)가 왼쪽 자식인 경우" 을 반복한다.

# 장점

자료의 삽입, 삭제, 검색에 최악의 상황에서도 일정한 실행시간을 보장함(Worst-case Guarantees). 

AVL 트리보다 회전의 수가 적음(AVL 트리가 더욱 엄격한 균형트리)

---

참고. 게일 라크만 맥도웰. 코딩 인터뷰 완전분석 (이창현 옮김) 

참고. "레드블랙트리", Wikipedia