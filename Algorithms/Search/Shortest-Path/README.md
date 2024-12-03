---
title: "최단 경로(Shortest Path)"
category: "Algorithms"
tags: ["Algorithms", "Search", "Shortest Path"]
date: 2024-12-04
last_modified_at: 2024-12-04
---

# 최단 경로(Shortest Path)
> 너비 우선 탐색(BFS) 알고리즘은 특정 상황에서 최단 경로를 보장할 수 있는 탐색 알고리즘이다. 

최단 경로 탐색 알고리즘은 **그래프에서 두 노드 간의 가장 짧은 경로를 찾는 알고리즘**을 의미한다. 

그래프의 최단 경로를 찾는 문제는 **가중치가 없는 그래프(Unweighted Graph)** 에서 가장 적은 간선을 통해 도달하는 경로를 찾는 문제와, **가중 그래프(Weighted Graph)** 에서 간선의 가중치 합이 최소가 되는 경로를 찾는 문제로 나눌 수 있다. 여기서 가중치(Weight)의 경우 거리, 비용, 시간 등으로 표현될 수 있으며, 경우에 따라 음수로 주어지기도 한다.

#### 최단 경로 문제의 종류 
- 단일 출발지 최단 경로 (Single-Source Shortest Path, SSSP)
- 단일 도착지 최단 경로 (Single-Destination Shortest Path, SDSP)
- 모든 쌍 최단 경로 (All-Pairs Shortest Path, APSP)

#### 최단 경로 알고리즘의 종류

- 다익스트라(Dijkstra) 
- 벨먼-포드(Bellman–Ford)
- 플로이드-워셜(Floyd–Warshall)
- 에이스타(A*)	
- SPFA(Shortest Path Faster Algorithm)

## 다익스트라(Dijkstra) 
> **음수 사이클**이 존재한다면 사용할 수 없다.

다익스트라 알고리즘은 음수 사이클이 존재하지 않는 가중치 그래프에서 **하나의 정점에서 모든 다른 정점으로 가는, 즉, 단일 출발지 최단 경로(Single Source Shortest Path, SSSP)** 문제를 해결하는 대표적인 알고리즘이다.

다익스트라 알고리즘은 시작 정점에서부터 인접한 정점들 중 가장 작은 가중치를 가진 정점을 선택하고, 그 정점의 인접 정점들의 경로를 갱신하며 최단 경로를 탐색한다. 이 과정에서 중복 계산을 피하고, 점차적으로 최단 경로를 갱신하는 방식은 다이나믹 프로그래밍의 최적 부분 구조와 중복된 부분 문제 특성을 포함한다. 또한, 각 단계에서 가장 가중치가 작은 선택(최적의 해)을 우선적으로 하는 방식으로 진행되는 점에서 그리디 알고리즘으로 분류되기도 한다.

### 간단한 다익스트라 알고리즘 구현 - 배열

```js
const input = [
    [0, 2, 5, 1, Infinity, Infinity], 
    [2, 0, 3, 2, Infinity, Infinity], 
    [5, 3, 0, 3, 1, 5], 
    [1, 2, 3, 0, 1, Infinity], 
    [Infinity, Infinity, 1, 1, 0, 2], 
    [Infinity, Infinity, 5, Infinity, 2, 0]
];

// O(V²)
function dijkstra(graph, source){   
    const n = graph.length; 
    const distance = new Array(n).fill(Infinity);
    const visited = new Array(n).fill(false);
        
    function getSmallIdx(){
        let min = Infinity;
        let idx = 0;

        distance.forEach((v, i) => {
            if(v < min && !visited[i]){
                min = v;
                idx = i;
            }
        });
        return idx;
    }

    distance.forEach((_, i) => distance[i] = graph[source][i]);
    
    // 출발지 초기화
    distance[source] = 0;    
    visited[source] = true;
    
    for(let i = 0; i < n - 2; i++){
        const current = getSmallIdx();
        
        visited[current] = true;
        
        for(let j = 0; j < n; j++){
            if (visited[j]) continue;

            const cost = distance[current] + input[current][j];

            if (cost < distance[j]) distance[j] = cost;
        }
    }
    
    return distance;
}

dijkstra(input, 0);
```

#### 의사코드(pseudo code)

### 개선된 다익스트라 알고리즘 구현 - 우선순위 큐(Priority Queue)

```js
// O((V + E) log V) → E = 간선의 수
function dijkstra(graph, source){   
}
```

#### 의사코드(pseudo code)

## 벨먼-포드(Bellman–Ford)
> 그래프에서 음수 가중치를 가진 간선이 있을 때 최단거리를 구하는 알고리즘 (음수 사이클이 있으면 동작하지 않습니다.)

## 플로이드 워셜(Floyd Warshall)

플로이드-워셜 알고리즘은 한 번 실행하여 모든 노드 간 최단 경로

## 에이스타(A*)	

## SPFA(Shortest Path Faster Algorithm)