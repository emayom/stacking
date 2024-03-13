# Context API는 "상태 관리" 도구인가?
[이전 글](https://github.com/emayom/TILs/blob/main/react/data-flow-in-react.md)에서는 리액트의 특징 중 하나인 단방향 데이터 흐름에 대해 언급했습니다.  
이번 글에서는 'Context API는 "상태 관리" 도구인가?'라는 원초적인 의문에 결론을 내리는 과정을 담아볼까 합니다.  

## 상태 관리(State Management)의 이해 
리액트를 사용하여 애플리케이션 개발을 하다보면 "상태 관리"는 피할 수 없는 중요한 카테고리입니다.  
상태는 크게 1) **전역 상태(Global State)** 2) **지역 상태(Local State · UI State)** 로 구분하며 이외에도 3) 서버 상태(Server state) 4) URL 상태(URL state) 등으로 분류할 수 있습니다. 

컴포넌트의 계층 구조(tree)에 따라 위에서 아래로 흐르는 리액트의 **단방향 데이터 흐름**은 복잡한 전역적인 상태를 관리하거나 컴포넌트 간 상태를 공유하고 변경하는 것에 어려움을

리액트는 상태 관리에 명확한 가이드라인을 제시하고 있지 않고 있기에, 다양한 상태 관리 라이브러리들을 통하여 전역 상태를 관리하고 있습니다. 

<br/>

## Context API: 상태 관리 도구인가?  
> Context API는 [React v16.3.0](https://github.com/facebook/react/blob/main/CHANGELOG.md#1630-march-29-2018)부터 공식적으로 도입되었으며, 별도의 의존성 없이 리액트 애플리케이션 내부에서 사용할 수 있습니다.  

"상태 관리"라는 개념을 공부하다보면, 비교적 러닝커브가 낮은 Context API를 useState, useReducer와 함께 사용하며 _"입문용 상태 관리 도구"_ 로 설명하는 글들을 쉽게 찾아볼 수 있습니다.  
 
그렇게 Context API를 상태 관리 도구로 인식하며 시작했지만, 머지않아 Context API를 과연 상태 관리 도구로 설명하는 것이 옳은 것인가?에 대한 의문이 생겼습니다. **사실상 상태를 "관리"해주는 건 useState, useReducer인데 말이죠.**  

그렇다면 Context API를 어떻게 정의할 수 있을까?

[리액트 공식 문서](https://react.dev/learn/passing-data-deeply-with-context)에서는 Context API를 **"props를 전달하기 위한 대안"** 정도로 설명하고 

결론적으로 **의존성 주입**을 위해 

<br/>

## 합성(Composition): Prop Drilling를 피하기 위한 다른 대안
Prop Drilling를 피하기 위한 다른 대안으로는 [컴포넌트 합성](https://legacy.reactjs.org/docs/context.html#before-you-use-context)이 있다. 

<br/>

> #### References
> - [Why React Context is Not a "State Management" Tool (and Why It Doesn't Replace Redux)](https://blog.isquaredsoftware.com/2021/01/context-redux-differences/#:~:text=Therefore%2C%20Context%20is%20not%20a,based%20on%20React%20component%20state.)  
> 