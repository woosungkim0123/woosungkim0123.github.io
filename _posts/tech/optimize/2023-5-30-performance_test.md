---
title: 성능 테스트 개념
author: woosungKim
date: 2023-5-30 20:00:00 +0800
categories: [성능, 테스트]
tags: [성능 테스트]
---

**1. 성능 테스트 개념**  
[2. 성능 테스트 - nGrinder](/posts/ngrinder)

<br>
<br>

### 성능 테스트란?

서비스 및 서비스 시스템의 성능을 확인하기 위해 실사용 환경과 비슷한 조건에서 테스트하는 과정이고 결과적으로 서비스의 응답 시간, 처리량, 확장성 등의 성능 지표를 측정하고 분석하는 것입니다.

<br>

**부하테스트(Load Test)**

시스템이 예상되는 사용량에서도 원활하게 동작하는지 확인하기 위한 테스트

이벤트나 특정 시간대와 같은 특정 상황에서의 최대 트래픽 처리 능력과 그 한계치를 파악하기 위한 테스트입니다.

<br>

**스트레스 테스트(Stress Test)**

서비스나 시스템이 예상 최대 부하나 그 이상의 부하를 장기간 받았을 때 어떻게 반응하는지 확인하는 테스트

시스템의 한계치를 탐색하고, 지속적인 과부하 상황에서의 예외 동작이나 오류를 파악하기 위한 테스트입니다.

<br>

### 질문을 통해 알아보는 성능 테스트

**"메모리 2GB에 2코어 프로세서를 사용하는 서버가 400TPS를 처리할 것으로 예상했는데 성능테스트를 해보니 실제로 해당 수치가 달성되지 않았다." 이 말에서 하드웨어에 이정도 성능이 나올거라고 예상하는 부분은 어떻게 예측하는가?**

서비스가 해당 성능에 도달하기 위해서 어떤 하드웨어를 사용해야하는 지는 예측할 필요가 없다.

비용에 따라 하드웨어를 선택하고 서버를 구축, 개발이 끝난 후 성능 테스트를 진행하게 되는데 이때 나온 성능을 바탕으로 비지니스 여부를 판단하게 된다.

성능이 부족한 상황에서 비즈니스가 가능하다고 판단되면 클라우드 환경에서 트래픽이 증가하는 것을 보고 확장하는 의사결정을 내리면 되는 것이고 아니라면 스케일 업이나 스케일 아웃을 통해 성능을 향상 시키면 된다.

즉, 이러한 비즈니스 사실을 성능 테스트를 통해 알 수 있고 예측은 할 수 없다.

성능테스트란 우리 비즈니스의 목표에 맞는 성능을 만들 수 있는 인프라를 찾아가는 과정이라고 볼 수 있다.

<br>

**4core->8core, 메모리 16g->32g면 성능이 두배 증가하나요?**

리소스가 증가하는 것에 비례해서 성능이 증가하지 않는다.

왜냐하면 우리가 만든 어플리케이션 런타임 환경이 리소스 환경에 최적화 되어 있지 않아서이다.

배틀그라운드라는 게임이 초기에는 매우 높은 그래픽카드를 요구했었지만 최적화를 통해 낮은 그래픽카드를 가진 유저들도 즐길 수 있게 변화된 것을 예시로 들 수 있겠다.

성능 테스트는 시스템이 어떤 상황에서 한계에 도달하는지, 성능이 기대치에 미치지 못하는 구체적인 이유는 무엇인지를 파악하고, 해결 방안을 모색하는 데 필수적인 과정이다


<br>

**로그인 API를 만들었는데 1500TPS가 나왔는데 이 수치는 의미가 있나?**

사용자가 로그인만 요청하는 경우는 없기 때문에 해당 수치는 크게 가치가 없다.

현실에서는 누군가는 로그인을 하고 있고 누군가는 조회를 하고 있는 복합적인 API 호출 상황이 발생한다. 이런 실제 트래픽 상황과 유사한 환경에서의 성능 테스트가 의미가 있다.

API 하나만의 성능 테스트는 그 API의 성능을 알아보기 위한 초기 단계로는 유용할 수 있으나 서비스 전체의 성능을 예측하거나 최적화하기 위해서는 더 복잡한 테스트 시나리오와 실제 서비스 사용 패턴을 반영한 테스트가 필요하다.

그러나 해당 API를 개선하려는 목적이면 성능 테스트를 통해 현재의 성능 지표를 파악하고, 개선 작업 후에는 다시 성능 테스트를 통해 개선효과를 확인할 수 있다.

<br>

### 사용자 경험을 결정하는 성능 테스트의 역할

성능 테스트는 단순히 숫자를 측정하는 것을 넘어서, 사용자 경험과 직결된 중요한 의사결정 도구이다. 

이른바 '4초룰'은 웹 사이트나 어플리케이션이 사용자의 관심을 유지하려면 최초 콘텐츠를 4초 이내에 불러와야 한다는 기준을 제시하는 것으로 사용자의 인내심이 제한적이고 그들의 경험이 기술적 성능에 얼마나 의존하고 있는지를 강조하는 부분이라고 할 수 있다.

결론적으로, 성능 테스트는 서비스가 사용자에게 우수한 경험을 제공할 수 있도록 보장하는 노력의 일환이자 시장에서의 경쟁력을 유지하고, 사용자의 만족을 극대화하는 동시에, 기술적인 한계를 극복하고 비즈니스 목표를 달성할 수 있는 방법이다.


