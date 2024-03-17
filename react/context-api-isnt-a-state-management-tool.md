# Context API는 "상태 관리" 도구인가?
[이전 글](https://github.com/emayom/TILs/blob/main/react/data-flow-in-react.md)에서는 리액트의 특징 중 하나인 단방향 데이터 흐름에 대해 언급했습니다.  
이번 글에서는 'Context API는 "상태 관리" 도구인가?'라는 원초적인 의문에 결론을 내리는 과정을 담아볼까 합니다.  

## 상태 관리(State Management)의 이해 
리액트를 사용하여 애플리케이션 개발을 하다보면 "상태 관리"는 피할 수 없는 중요한 부분입니다.  
컴포넌트의 계층 구조(tree)에 따라 위에서 아래로 흐르는 리액트의 **단방향 데이터 흐름**은 계층 구조가 깊어질수록 복잡한 상태를 관리하거나 여러 컴포넌트 간 상태를 공유하는 것이 더욱 어려워진다는 문제점을 안고있습니다. 

리액트에서는 상태 관리에 대한 명확한 가이드라인을 제시하고 있지 않기에 다양한 상태 관리 패턴을 기반의 라이브러리들(e.g. Redux, Recoil, Jotai, Zustand, Valtio, React Query, etc.) 이 등장하였으며, 현재는 상태 관리 _춘추전국시대_ 로 불릴 만큼 다양한 상태 관리 라이브러리가 현존하고 있습니다. 덕분에 라이브러리 각각의 접근 방식과 장단점을 파악하여, 애플리케이션 요구 사항에 적합한 상태 관리 라이브러리를 선택할 수 있는 역량까지 프론트엔드 개발자로서의 자질으로 자리 잡고 있는 듯합니다.

### 상태(State)란 
상태란 1) 시간이 지남에 따라 변하여 2) 렌더링 결과물(UI)에 영향을 주며, 3) **컴포넌트 내부적으로 관리되는 메모리**입니다.   
상태는 크게 **전역 상태(Global State)**, **지역 상태(Local State)** 로 분류할 수 있지만, 역할에 따라서는 UI 상태(UI State), 서버 상태(Server State), URL 상태(URL State), 폼 상태(Form State) 등의 다양한 유형으로 구분할 수 있습니다.  

<br/>

## Context API: 상태 관리 도구인가?  
> Context API는 [React v16.3.0](https://github.com/facebook/react/blob/main/CHANGELOG.md#1630-march-29-2018)부터 공식적으로 도입되었으며, 별도의 의존성 없이 리액트 애플리케이션 내부에서 사용할 수 있습니다.  

"상태 관리"라는 개념을 공부하다 보면 비교적 러닝 커브가 낮고, 추가적인 라이브러리 없이 사용할 수 있는 Context API를 useState, useReducer와 함께 사용하며  _"입문용 상태 관리 도구"_  정도로 설명하는 글들을 쉽게 찾아볼 수 있습니다. 그러나 머지않아 'Context API를 과연 상태 관리 도구로 설명하는 것이 옳은 것인가?'에 대한 의문이 생기기 시작할 것입니다. **사실상 상태의 "관리"는 useState, useReducer hook이 수행하고 있으니 말이죠.**  

그렇다면 Context API를 뭐라고 설명하는 것이 좋을까요?   
아무래도 아직까지는 <u>**Prop Drilling을 피하기 위한 의존성 주입 도구**</u> 정도가 적절하지 않을까 싶습니다.  
실제로 [리액트 공식 문서](https://react.dev/learn/passing-data-deeply-with-context)에서는 Context를 상태 끌어올리기(Lifting state up)로 발생가능한 Prop Drilling을 회피하며, **"props를 전달하기 위한 대안"** 정도로 설명하고 있습니다. Context는 아무것도 관리하지 않습니다. 전달받고, 전달할 뿐이죠. 

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