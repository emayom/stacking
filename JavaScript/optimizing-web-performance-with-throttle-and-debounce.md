---
last_modified_at: '2025-01-20T16:20:31.999Z'
date: '2025-01-20T16:20:31.999Z'
---
# Throttle, Debounce로 웹 성능 최적화하기
[Throttle](#debounce---일정-시간-이후-한-번의-실행을-보장)과 [Debounce](#debounce---일정-시간-이후-한-번의-실행을-보장)는 이벤트 호출 빈도 제어를 통한 **성능 최적화**를 목적으로 사용되는 기법으로 주로 사용자와의 상호작용(스크롤, 드래그, 키보드 입력 등)에서 발생하는 연속적인 이벤트를 효율적으로 처리할 때 사용한다.

특히, 이벤트 핸들러 함수가 API 요청이나 고비용 연산을 포함하는 경우, 연속적인 이벤트로 인해 서버 부하나 불필요한 네트워크 호출 및 연산이 발생할 수 있다. Throttle과 Debounce를 사용하여 이러한 퍼포먼스 이슈를 방지하고 성능을 최적화할 수 있다.

Throttle과 Debounce는 비슷한 목적을 가지고 있지만, 두 가지 기법은 다르게 동작한다. 


## Throttle - 일정 시간 동안 한 번의 실행을 보장 
![image](https://github.com/emayom/emayom/assets/85545101/5bbf1425-7766-4de9-abc0-1c0932fbd2a8)

Throttle는 일정 시간(Waiting time) 동안 여러 개의 연속적인 이벤트 호출이 발생하더라도 최초 이벤트(Leading call)를 실행하고, 이후의 이벤트는 무시하는 방식으로 동작한다. 주의할 점은 일정 주기마다 이벤트가 실행되는 것이 아니라, 이벤트 발생 이후에만 실행된다.

Throttle를 사용하여 연속적인 이벤트를 처리할 경우 즉각적인 처리를 통해 사용자 경험을 향상시킬 수 있으며, 내부적으로는 반복되는 불필요한 호출을 방지하여 한 번의 실행만을 요청할 수 있다. 

<br/>

## Debounce - 일정 시간 이후 한 번의 실행을 보장
![image](https://github.com/emayom/emayom/assets/85545101/8d2385a7-0a8e-49ac-b9de-76b521051744)

Debounce는 여러 개의 연속적인 이벤트 호출을 하나의 "그룹"으로 간주하고, 일정 시간(Waiting time)이 경과할 때까지 함수의 실행을 **지연**시켰다가 마지막 이벤트를 실행(Trailing call)하는 방식으로 동작한다.  

일정 시간의 지연이 발생하지 않는 경우, 이전에 발생하는 이벤트의 실행은 무시되어 연속된 이벤트 호출을 단일 이벤트로 처리한다. 

Debounce를 사용하여 연속적인 이벤트를 처리할 경우 사용자에게 실시간으로 처리되는 것처럼 보이지만, 내부적으로는 반응성을 유지하면서도 불필요한 작업을 방지하여 한 번의 실행만을 요청할 수 있다. 

<br/>

## Throttle, Debounce의 사용 사례  
이전까지 Throttle과 Debounce, 두 가지 기법의 동작 방식에 대해 자세히 알아봤다.    

> **Throttle**은 일정 시간 동안 최초 한 번만 이벤트를 실행하고, 이후에 발생하는 이벤트는 무시한다.  
> **Debounce**는 일정 시간 동안 실행을 지연시킨 후 마지막 이벤트만을 실행한다.

직접 구현할 수도 있지만, Lodash와 같은 유용한 라이브러리를 사용하여 간단하게 적용할 수도 있다.

기법을 활용하는 것도 중요하지만, 각각의 기법을 목적에 맞게 사용하는 것도 중요하다.   
조금 더 구체적인 상황을 통해 사용 사례를 알아보자. 

### 무한 스크롤(Infinite Scroll)
사용자가 페이지를 스크롤 할 때마다 새로운 콘텐츠를 동적으로 로드하여 페이지를 연장시키는 기능을 구현한다고 가정해 보자.

Throttle, Debounce 어느 것을 사용하더라도 불필요한 렌더링 및 데이터 요청을 방지할 수 있지만,  
사용자의 스크롤이 멈출 때까지 기다렸다가 새로운 콘텐츠를 불러오는 것(Debounce)보다는  
사용자의 스크롤이 일정 위치까지 내려왔을 때 즉시(Throttle) 새로운 콘텐츠를 불러오는 것이 페이지가 부드럽게 스크롤 되는 느낌을 줄 수 있다.

사용자 경험까지 고려하고자 한다면, 페이지가 부드럽게 반응하면서도 불필요한 데이터 요청을 방지할 수 있도록 Throttle을 사용하여 새로운 콘텐츠를 불러오는 것이 더 좋은 선택일 수 있다.  

### 스크롤에 반응하는 헤더(Hide Menu on Scroll)
> 어떻게 명명하는 것이 자연스러울지 고민되어 '스크롤에 반응하는 헤더'라고 부르겠다. 

사용자의 스크롤이 수직 아래로 향할 때는 헤더를 숨기고, 수직 위로 향할 때는 헤더를 보여주는 기능을 구현한다고 가정해 보자.

Debounce를 사용하면 반복되는 불필요한 이벤트 실행은 방지할 수 있지만, 지연이 발생하여 사용자가 스크롤의 방향을 전환할 때 즉각적으로 빠르게 반응하지 못할 수 있다. 즉각적으로 빠르게 반응하여 사용자 경험을 향상시키면서도 반복되는 불필요한 실행을 방지하고 싶다면, Throttle을 사용하여 스크롤에 반응하는 것이 더 좋은 선택일 수 있다.  

### 화면창 리사이즈(Window Resize)
사용자가 화면 크기를 조정할 때마다 보여지는 다른 화면을 렌더링하는 기능을 구현한다고 가정해 보자.

Throttle을 사용하면 일정 시간 사용자가 화면 크기를 반복 조정하는 경우 매번 렌더링되게 되며 브라우저 성능에 부담을 줄 수 있다. 불필요한 렌더링을 방지하면서도 화면 크기의 조정에 따라 다르게 렌더링하고 싶다면, 화면의 조정이 종료되고 일정 시간 지연 후 렌더링을 처리할 수 있도록 Debounce를 사용하는 것이 더 좋은 선택일 수 있다.  

### 실시간 검색(Real-Time Search)
사용자가 검색창에 검색어를 타이핑할 때마다 결과를 실시간으로 보여주는 기능을 구현한다고 가정해 보자.

Throttle을 사용하면 일정 시간 사용자가 검색어를 갱신할 때마다 결과를 서버에 요청하게 될 뿐만 아니라 사용자가 검색어를 타이핑하는 동안에도 불필요한 검색 결과를 서버에 요청하게 될 수 있다. 이는 서버에 과도한 부담을 줄 수 있을 뿐만 아니라 사용자 경험을 향상시킬 수 있는 방향이 아닐지 모른다. 

따라서 사용자 경험을 향상시키면서도 불필요한 작업을 방지하기 위해서는 실시간으로 처리되는 것처럼 보이지만, 내부적으로는 일정 시간 지연 후에 검색 결과를 요청할 수 있도록 Debounce를 사용하는 것이 더 좋은 선택일 수 있다.

<br/>

대표적으로 언급되는 무한 스크롤(Infinite Scroll), 스크롤에 반응하는 헤더(Hide Menu on Scroll), 화면창 리사이즈(Window Resize), 실시간 검색(Real-Time Search)을 통해 Throttle과 Debounce의 사용 사례를 알아봤다. 

이외에도 마우스 이벤트 처리, 버튼 클릭 이벤트 처리, 페이지 스크롤 애니메이션 처리 등에서도 사용될 수 있다. 

<br/>

## 글을 작성하며   
최근 사전 과제를 진행하면서 위에서 언급한 '스크롤에 반응하는 헤더(Hide Menu on Scroll)'를 구현하게 되었고 Lodash의 Throttle을 사용하여 최적화했고, 이후 면접에서 Throttle과 Debounce 중 어떤 이유로 Throttle을 사용하였는지 설명해달라는 질문을 받게 되었다.    

Throttle과 Debounce의 개념은 알고 있었지만, 추상적으로 이해하고 기억한 덕분에  
Throttle과 Debounce를 비교하여 왜 Throttle을 사용하였는지에 대해 논리적인 근거로 설명하지 못했다.  
'다들 사용하니까.'가 아닌 '내가 왜' 사용했는지를 논리적 근거를 생각하며 코드를 작성해야겠다고 두번 생각하게 되었다. 

### References 
[Debouncing and Throttling Explained Through Examples](https://css-tricks.com/debouncing-throttling-explained-examples/)  
[Advanced JavaScript Functions to Improve Code Quality](https://www.paulsblog.dev/advanced-javascript-functions-to-improve-code-quality/)
