---
layout: single
title: "[Python] 자료구조 알고리즘 코드 정리"
categories: Algorithm
tag: [python, algorithm]
toc: true
author_profile: false
sidebar:
    nav: "docs" 
---

잘못된 부분이 있다면 댓글부탁드립니다:D

## 이분 탐색(Binary Search)

```python
def search_binary(x, left, right): #x = 찾을 숫자
    while (right > left):
        mid = (left + right) // 2
        if x == arr[mid]:
            return mid
        elif x > arr[mid]:
            left = mid + 1
        else:
            right = mid - 1
    return -1
```

```python
#라이브러리 사용
from bisect import bisect_left
result = bisect_left(arr, x) #x = 찾을 숫자
```

---

## 그래프 탐색 (DFS/BFS)

```python
# 인접 리스트
graph = [[1, 2, 3], [2, 4], [0], [4], [3]] #graph[i]: i에서 갈 수 있는 정점
# 인접 행렬
graph = [[0, 1, 1, 1, 0], #graph[i][j]: 정점 i에서 정점 j로 이동 가능 여부
         [0, 0, 1, 0, 1]
         [1, 0, 0, 0, 0],
         [0, 0, 0, 1, 0]]
```



### 깊이우선탐색(DFS)

```python
#인접 리스트
visited = [0] * 정점 개수
def DFS(v):
    visited[v] = 1
    for n in graph[v]:
        if not visited[n]: DFS(n)
```

```python
#인접 행렬
visited = [0] * 정점 개수
def DFS(v):
    visited[v] = 1
    for n in range(len(graph)):
        if graph[v][n] and not visited[n]: DFS(n)
```

```python
#좌표에서 상하좌우 이동
N = 배열 세로길이
M = 배열 가로길이
ni = [-1, 1, 0, 0] #위, 아래, 왼쪽, 오른쪽
nj = [0, 0, -1, 1]
visited = [[0]*M for _ in range(N)]
def DFS(i, j):
    visited[i][j] = 1
    for n in range(4):
        if 0<=i+ni[n]<N and 0<=j+nj[n]<M and visited[i+ni[n]][j+nj[n]]:
            DFS(i+ni[n], j+nj[n])
```



### 너비우선탐색(BFS)

```python
#인접 리스트
from collections import deque
visited = [0] * 정점 개수
def BFS(v):
    queue = deque()
    queue.append(v)
    visited[v] = 1
    while queue:
        for n in graph[v]:
            if not visited[n]:
                visited[n] = 1
                queue.append(n)
```

```python
#인접 행렬
from collections import deque
visited = [0] * 정점 개수
def BFS(v):
    queue = deque()
    quque.append(v)
    visited[v] = 1
    while queue:
        v = queue.popleft()
        for n in range(len(graph)):
            if graph[i][n] and not visited[n]:
                visited[n] = 1
                queue.append(n)
```

```python
#좌표에서 상하좌우 이동
from collections import deque
N = 배열 세로길이
M = 배열 가로길이
ni = [-1, 1, 0, 0] #위, 아래, 왼쪽, 오른쪽
nj = [0, 0, -1, 1]
visited = [[0]*M for _ in range(N)]
def BFS(i, j):
    queue = deque((i, j))
    visited[i][j] = 1
    while queue:
        i, j = queue.popleft()
        for n in range(4):
            if 0<=i+ni[n]<N and 0<=j+nj[n]<M and visited[i+ni[n]][j+nj[n]]:
                queue.append((i+ni[n], j+nj[n]))
                visited[i+ni[n]][j+nj[n]] = 1
```

---

## 최단 경로

### 다익스트라(Dijkstra)

```python
import sys
import heapq
INF = sys.maxsize

def Dijkstra(start):    
    distance = [INF] * (V+1)
	distance[start] = 0
    heap = []
	heapq.heappush(heap, (start, 0))

    while heap:
        v, w = heapq.heappop(queue)

        if distance[v] < w: continue

        for nv , nw in graph[v]: #nv: 다음 정점, nw: 거리
            if w+nw < distance[nv]:
                distance[nv] = w+nw
                heapq.heappush(queue, (W+nw, nv))
    return distance
```



### 플로이드 와샬(Floyd Warshall)

```python
V = 정점의 개수
for k in range(V): #거쳐가는 정점
    for i in range(V): #출발
        for j in range(V): #도착
            distance[i][j] = min(distance[i][j], distance[i][k] + distance[k][j])
```

---

## 유니온 파인드(Union Find)

```python
def find_root(target):
    if target != parent[target]:
        parent[target] = find_root(parent[target])
    return parent[target]
    
def union(a, b):
    a = find_root(a)
    b = find_root(b)
    
    if a > b: parent[a] = b
    else: parent[b] = a
```

---

## 최소 신장 트리(MST)

```python
#크루스칼 알고리즘, 유니온 파인드 사용
import heapq
#graph[i] = [(다음정점, 비용), (다음정점, 비용), ...]
heap = []
for v in range(N):
    for nv, nw in graph[v]:
        heapq.heappush((nw, v, nv))
    
weight = 0
while heap and count != V-1:
    w, a, b = heapq.heappop(heap)
    if union(a, b): weight += w
```

---

## 위상 정렬

```python
import heapq

indegree = [0] * N
for v in range(N): #진입차수 확인
    for n in graph[v]:
        indegree[n] += 1

heap = []
for i in range(N): #진입차수가 0인 정점 찾기
    if indegree[i] == 0:
        heapq.heappush(heap, i)
        
result = []
while heap:
    v = heapq.heappop(heap)
    result.append(v)
    for i in graph[v]:
        indegree[i] -= 1
        if indegree[i] == 0:
            heapq.heappush(heap, i)
```

