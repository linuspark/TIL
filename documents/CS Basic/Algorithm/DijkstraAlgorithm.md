# Dijkstra Algorithm

데이크스트라 알고리즘, 혹은 다익스트라 알고리즘은 "음의 가중치가 없는 그래프의 한 정점에서 다른 한 정점까지의 최단거리를 구하는 알고리즘" 이다. (최단경로 알고리즘)

이 알고리즘의 변형으로는 한 정점에서 부터 모든 정점까지의 최단 경로를 구하는 "최단경로 트리" 를 만드는 것이 있다.

a와 b 사이의 최단 경로를 찾는 데이크스트라의 알고리즘이다. 가장 낮은 값을 가진 방문하지 않은 꼭짓점을 선택하고, 방문하지 않은 각 인접 노드와의 거리를 계산하고, 작을 경우 인접 거리를 업데이트한다. 이 그림에서는 꼭짓점에 도착하면 빨간색으로 표시했다.

![https://upload.wikimedia.org/wikipedia/commons/5/57/Dijkstra_Animation.gif](https://upload.wikimedia.org/wikipedia/commons/5/57/Dijkstra_Animation.gif)

# 알고리즘

1. 모든 정점(꼭짓점)을 "미방문" 상태로 표시한다.
2. 시작점 A를 제외한 모든 정점의 값을 "무한대" 로 설정한다.
3. "현재 정점" 에 인접한 미방문 정점 까지의 거리를 계산하여 미방문 정점의 값을 업데이트 한다.
    1. 미방문 정점의 현재 값과 계산된 거리값 중 더 작은 값으로 업데이트 한다.
4. "현재 정점" 에서 인접한 모든 미방문 정점의 값을 모두 업데이트 하였다면 현재 정점을 "방문한 정점" 으로 표시하고 미방문 정점 리스트에서 제거한다.
5. "미방문 정점" 중 가장 거리 값이 작은 정점을 선택하여 "현재 정점" 으로 만들고 3번 부터 다시 수행한다.
6. 목적지가 "방문한 상태" 로 표시되면 알고리즘을 종료한다.

# 예시

![https://upload.wikimedia.org/wikipedia/commons/2/23/Dijkstras_progress_animation.gif](https://upload.wikimedia.org/wikipedia/commons/2/23/Dijkstras_progress_animation.gif)

로봇 모션 계획 문제에서 데이크스트라 알고리즘이 시작점(좌측 하단, 빨간색)에서 도착점(우측 상단, 초록색)까지의 경로를 찾는 도해

![https://upload.wikimedia.org/wikipedia/commons/thumb/e/e4/DijkstraDemo.gif/440px-DijkstraDemo.gif](https://upload.wikimedia.org/wikipedia/commons/thumb/e/e4/DijkstraDemo.gif/440px-DijkstraDemo.gif)

유클리드 거리에 기반한 데이크스트라 알고리즘의 시연이다. 빨간색 선은 최단 경로이다

---

참고. "다익스트라 알고리즘", wikipedia

참고. "다익스트라 알고리즘", namu wiki
