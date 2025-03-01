---
title: 이제 Framer-Motion에서 Framer를 뗀
category: Library
tags:
  - Web
  - Motion
  - Framer Motion
last_modified_at: '2025-03-01T11:05:28.823Z'
date: '2025-03-01T11:05:28.823Z'
---

# 이제 Framer-Motion에서 Framer를 뗀

최근 API 도큐먼트를 확인하기 위해 찾은 [Motion](https://motion.dev/)의 웹 페이지는 불과 몇달 전 본 것과는 사뭇 달라진 분위기였다.   
그새 빠르게도 변했네. 하며 둘러보다보니 슬로건이 이상하다.  

> _"A modern animation library for JavaScript and React"_

분명, React 의존성을 가진 React 전용 라이브러리였던 것 같은데?  
어느새 한편에는 Vanilla JavaScript에서의 애니메이션을 위한 문서가 자리하고 있다.   

아무리 찾아봐도 Framer Motion에서 _"Framer"_ 가 보이지 않는다.  
혹시 내가 보고 있는게 너무 닮은 다른 무언가인가(?)하는 생각에 잠시 혼란이 찾아왔다. 

### Popmotion, Motion의 시작 

우리가 알고 있는 Framer Motion 프로젝트는 이미 10년 전부터 이어져 오고 있다.    

Motion의 시작은 2015년 7월, npm에 배포된 [Popmotion](https://github.com/Popmotion/popmotion)으로, CSS와 Native Browser JavaScript API가 제한적이었던 2014년, CSS만으로 구현할 수 있는 UI가 만족스럽지 않았던 현 Motion의 제작자
[@mattgperry](https://github.com/mattgperry)가 _"one where anything was possible"_ 을 목표로 첫 번째 라이브러리 Popmotion을 제작하게 되었다. 지금처럼 React가 많은 프로젝트에서 채택되기 전부터 시작한 Popmotion 프로젝트는 초기 Vanilla JavaScript 기반의 간단하고, 저수준의 경량 애니메이션 라이브러리로 제작되었다. 

> 이때 `animate` 함수는 5kb가 채 안되는 작은 번들 사이즈를 가졌었다. 

### Framer에 인수되다

2018년, Framer는 Framer X를 런칭하며, React와의 통합을 통해 사용자가 동적이고, 데이터 기반의 프로토타입(data-driven prototypes)을 만들 수 있도록 하는 등, Framer는 더 이상 디자이너만을 위한 프로토타이핑 툴이 아닌, React 기반의 프로토타입 도구로서 디자인과 개발간의 경계를 허물며, 제품에 상당한 변화를 가져오게 된다.

> 자세한 Framer의 히스토리가 궁금하다면, ['The Evolution of Framer and why I switched.'](https://www.framerverse.com/blog/the-evolution-of-framer-a-timeline-of-innovation-in-web-design-and-prototyping)을 읽어보기를 추천한다. 

또한, Framer는 모든 기기에서 유연하고 매끄러운 애니메이션을 구현할 수 있는 React API의 개발을 목표로 하였고, 이 과정에서 Popmotion 프로젝트를 인수하며, Popmotion의 제작자 Matt Perry는 Framer에 합류하여 Framer Motion의 개발에 참여하게 된다.

그렇게 2019년 1월, Framer Motion이 npm에 공개되며, 현재까지 다운로드 수가 590만 건을 돌파하는 강력한 애니메이션 라이브러리로 자리매김하게 되었다. 

> Popmotion은 2022년 8월, v11.0.5를 마지막으로 더 이상의 업데이트는 이루어지지 않고 있다. 

![Image](https://github.com/user-attachments/assets/6ace90b1-5cdf-40d5-a80d-b8fa764538e7)


Framer Motion의 누적 다운로드 수는 계속해서 증가하고 있으며, 라이브러리의 지속적인 성장이 예상된다.  
Framer Motion은 어떻게 이렇게 많은 선택을 받으며 성장할 수 있었을까?   

직접 사용해보거나 다른 글들을 참고하면서 장단점은 어렵지 않게 확인할 수 있을 것 같아, 개인적으로 Framer Motion을 직접 사용하면서 느꼈던 DX 측면의 장점 하나를 언급하고자 한다. 

#### 두 마리 토끼 잡기: `Declarative` & `Imperative`

우리가 구현하는 애니메이션은 대부분 간단하지만, 때로는 요구사항에 따라 애니메이션의 흐름을 외부 상태나 이벤트와 연결하여 동적으로 제어하거나, 컴포넌트 간의 오케스트레이션이 필요한 경우도 존재한다. 

Framer Motion에서는 애니메이션을 컨트롤하기 위한 방식으로, `motion` 컴포넌트와 `useAnimate` 훅, 두 가지의 선택지를 제공하여 애니메이션의 복잡도나 요구 사항에 맞춰 유연하게 선택할 수 있다. 

- `motion` 컴포넌트: 선언적 방식(declarative way)

  ```jsx
  <motion.div
    initial={{
      rotate: 0,
    }}      
    animate={{
      rotate: 180,
    }}      
    transition={{
      type: 'tween',
      ease: 'easeInOut',
      repeat: Infinity,
      repeatType: 'reverse',
      repeatDelay: 1,
      duration: 2,
    }}  
  />
  ```

  기본적으로 Framer Motion은 애니메이션 기능이 추가된 형태로 추상화된 [`motion` 컴포넌트](https://motion.dev/docs/react-motion-component)를 제공하여 애니메이션을 보다 간편하게 제어할 수 있도록 설계되었다. 컴포넌트에 `initial`, `animate`, `transition` 등의 props를 전달하여 상태에 따른 애니메이션의 변화를 선언하기만하면, 애니메이션(CSS transitions)을 내부적으로 처리한다.

  컴포넌트의 여러 상태(`focus`, `hover`, `tap` 등)에 따라 실행될 애니메이션을 다르게 적용하고 싶다면, `variants` 속성을 사용하여 사전에 정의된(predefined) 애니메이션 객체 형태로도 선언할 수 있다.

  > `Variant`는 동적으로 인자(argument)를 받아 애니메이션 객체를 리턴하는 함수 형태로도 정의할 수 있다. 

  뿐만 아니라, 부모-자식 간의 관계에서는 부모 컴포넌트의 애니메이션 상태(`variants` 키)는 자식 컴포넌트로 전파(propagate)되어 애니메이션 흐름을 동기화할 수 있으며, 부모 컴포넌트는 `transition` 속성에 포함된 `delayChildren`과 `staggerChildren`을 통해 자식 컴포넌트들의 애니메이션을 오케스트레이션할 수 있다.

- `useAnimate` 훅: 명령형 방식(imperative way)

  ```js
  import { useAnimate, useInView } from "motion/react"

  function Component() {
    const [scope, animate] = useAnimate();
    const isInView = useInView(scope);
    
    useEffect(() => {
      const enterAnimation = async () => {
        await animate(scope.current, { opacity: 1 })
        await animate("li", { opacity: 1, x: 0 })
      }

      if (isInView) {
        enterAnimation();
      }
    }, [isInView])
    
    return (
      <ul ref={scope}>
        <li />
        // ...
      </ul>
    )
  }
  ```

  `motion` 컴포넌트만으로도 충분히 복잡한 애니메이션을 선언적으로 처리할 수 있지만, 
  실시간 애니메이션이나 사용자의 상호작용에 따른 애니메이션 혹은 연속된 여러 애니메이션 사이의 타이밍을 세밀하게 제어하기는 부족할 수 있다. 
  
  중앙 집중적이고, 세밀한 컨트롤이 필요하다면 `motion` 컴포넌트 대신 [`useAnimate` 훅](https://motion.dev/docs/react-use-animate)을 활용할 수 있다.  

  `useAnimate` 훅은 명령형 방식으로 애니메이션을 제어하며, Framer Motion에서 제공하는 여러 훅들과 결합하여 사용할 수 있다. 예를 들어, `useMotionValue`, `useTransform`과 같은 훅들을 결합하여 애니메이션의 동적인 값을 실시간으로 추적하고 변환하여 적용하거나, 여러 컴포넌트 간의 애니메이션을 유기적이고, 효율적으로 처리할 수 있다. 

  > `motion.div`과 같은 `motion` 컴포넌트는 내부적으로 `motionValue를` 생성해 애니메이션 값의 상태와 속도를 추적한다. 

### Motion이라는 이름으로

Framer Motion은 2024년 11월, 또 한 번 새로운 전환점을 맞이했다.  

제작자 Matt Perry는 블로그에 ['Framer Motion is now independent, introducing Motion'](https://motion.dev/blog/framer-motion-is-now-independent-introducing-motion)라는 제목의 글을 포스팅하며 Framer Motion이 Framer로부터 독립하여 '**Motion**'이라는 이름으로 나아갈 것을 발표했다. Framer를 든든한 첫 스폰서로 등에 업고 말이다. 앞으로 몇 주, 몇 달 안에 더 많은 기능이 새로운 기본 API에 추가될 것을 예고한 만큼 Motion의 업데이트가 개인적으로 기대가 된다.

단순히 _"Framer"_ 가 풀 네임에서 사라진 것에서 시작한 이야기이지만, 지금의 Motion이 있기까지의 배경들을 여러 글들을 통해 접하다보니 10년 사이 브라우저가 발전한 속도도, Framer의 발전과 변화 과정도 개인적으로 참 놀랍다. 사실, 10년동안 애니메이션 라이브러리를 운영하며, 개발하고 있는 Matt Perry님이 제일 놀랍다. (positive) 

차치하고, 개인적으로 지금의 프로덕트 UI에서 애니메이션은 단순한 모션을 넘어, 꽤나 중요한 부분이라고 생각한다. 애니메이션을 적절히 활용하는 것은 트렌드가 아니라, 인터페이스의 시각적 매력을 높이고, 시스템과 상호작용을 매끄럽고 풍부하게 만들어 사용자 경험을 향상시키는 필수적인 요소로 자리잡고 있다.  

