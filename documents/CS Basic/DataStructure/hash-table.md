# 해시테이블(Hash Table)

해시테이블 (Hash Table), 해시 맵(Hash map) 등 으로 불리는 자료구조는 효율적인 탐색을 위한 자료구조로, 키(Key)를 값(Value)에 대응시키는 방법으로 연관배열(associative array) 구조를 통해 구현된다. 연관배열 구조란 키 하나와 값 하나가 연결되어 있어 키를 통해 연결된 값을 얻을 수 있는 구조이다. (사전:Dictionary, 맵:Map 등)

연관배열 구조는 다음과 같은 명령을 지원하며, 해시테이블도 동일하다.

- Insertion: 키와 값이 주어졌을 때, 연관 배열에 그 두 값을 저장하는 명령
- Search: 키가 주어졌을 때, 연관되는 값을 얻는 명령
- Replace: 키와 새로운 값이 주어졌을 때, 원래 키에 연관된 값을 새로운 값으로 교체하는 명령
- Deletion: 키가 주어졌을 때, 그 키에 연관된 값을 제거하는 명령

![https://upload.wikimedia.org/wikipedia/commons/thumb/7/7d/Hash_table_3_1_1_0_1_0_0_SP.svg/630px-Hash_table_3_1_1_0_1_0_0_SP.svg.png](https://upload.wikimedia.org/wikipedia/commons/thumb/7/7d/Hash_table_3_1_1_0_1_0_0_SP.svg/630px-Hash_table_3_1_1_0_1_0_0_SP.svg.png)

해시테이블을 이해하기 위해서는 키(Key), 값(Value), 해시함수(Hash Function), 저장소(Buckets, Slot)의 개념을 이해해야 한다.

- Key: 고유한 값으로 해쉬함수(Hash Function)의 입력이 된다. 다양한 길이가 되며 무한한 값이다.
- Value: 최종적으로 저장소(buckets)에 저장될 값이다. 키와 매칭되어 접근할 수 있다
- Hash Function: 키(key)를 해시(hash)로 바꾸어주는 함수.
- Hash: 해쉬함수(Hash) 를 통해 계산되어 나온 값

```csharp
hash = hashFunction(key);
index = hash % arraySize;
```

# 동작 과정

1. 해쉬함수(hash function)을 이용하여 키(key)의 해시(hash)값을 계산한다.

    key의 개수는 무한한데 반해 hash는 유한하기 때문에 서로 다른 key가 같은 hash를 만들 수 있다.

2. hash % arraySize 와 같은 방법을 이용하여 인덱스를 구한다. 

    서로 다른 hash가 같은 인덱스를 만들어 낼 수 있다.

3. 저장소의 구해진 인덱스에 값을 저장한다.

    같은 인덱스에 값을 저장해야 하는 경우가 있다. 이를 해시 충돌이라고 한다.

해시테이블에 저장하는 과정의 시간 복잡도는 O(1) 이다. 해시함수를 통해 만들어 낸 인덱스에 그냥 데이터를 저장하기만 하면 되기 때문이다. 해시함수의 복잡도는 계산하지 않는다.

# 해시 충돌(Hash Collisiont)

기본적으로 해시테이블은 무한한 값을 유한한 공간에 매핑하는 것 이다. [비둘기집 원리](https://ko.wikipedia.org/wiki/비둘기집_원리)에 따라 해쉬 충돌에 대비하여야 한다.

해시함수에 의해 같은 해시값이 나오는 경우, 저장공간(array size)의 부족으로 같은 인덱스를 만들어 내는 경우, 등에서 충돌이 생길 수 있다.

해시충돌을 해결하기 위한 방법으로는 다음과 같은 두 가지 방법이 주로 사용된다.

## 체이닝(Separated Chaining)

![https://upload.wikimedia.org/wikipedia/commons/thumb/d/d0/Hash_table_5_0_1_1_1_1_1_LL.svg/900px-Hash_table_5_0_1_1_1_1_1_LL.svg.png](https://upload.wikimedia.org/wikipedia/commons/thumb/d/d0/Hash_table_5_0_1_1_1_1_1_LL.svg/900px-Hash_table_5_0_1_1_1_1_1_LL.svg.png)

충돌이 발생 했을 때 새로운 값을 기존의 값에 연결리스트로 연결해 저장하는 방식.

위 예시에서 John과 Sandra의 해시 값이 충돌하였다. 저장소는 그냥 배열 등으로 구현되어 있는 것이 아니라 각 위치에 연결리스트로 구현되어 있어 해당 값이 이미 있는 경우 연결리스트로 계속해서 추가한다. 

## 개방주소법 (Open Addressing)

![https://upload.wikimedia.org/wikipedia/commons/thumb/b/bf/Hash_table_5_0_1_1_1_1_0_SP.svg/760px-Hash_table_5_0_1_1_1_1_0_SP.svg.png](https://upload.wikimedia.org/wikipedia/commons/thumb/b/bf/Hash_table_5_0_1_1_1_1_0_SP.svg/760px-Hash_table_5_0_1_1_1_1_0_SP.svg.png)

충돌이 발생 하였을 때 주어진 해시 값 다음 위치에 값을 저장한다. 즉 비어있는 공간에 값을 저장하는 것이다. 

# 문제

## 회문순열

주어진 문자열열이 회문(Palindrome)의 순열인지 아닌지 확인하는 함수를 작성하라. 회문이란 앞으로 읽으나 뒤로 읽으나 같은 단어 혹은 구절을 의미하며, 순열이란 문자열을 재배치하는 것을 뜻한다. 회문이 꼭 사전에 등장하는 단어로 제한 될 필요는 없다.

- 입력: Tact Coa
- 출력: True (taco cat / atcocta 등)

---

참고. 게일 라크만 맥도웰. 코딩 인터뷰 완전분석 (이창현 옮김) 

참고. "연관배열", Wikipedia

참고. "Hash Table", Wikipedia
