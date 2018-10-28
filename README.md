# 개요
유니티 ECS & Job System 공부 목적용 저장소입니다.

### ECS & C# Job System & Burst Compiler?

- **ECS(엔티티 컴포넌트 시스템) :** 새로운 C# 잡 시스템은 간편하면서도 안전한 방식으로 멀티코어를 활용합니다. C# 스크립트를 활용하여 사용자가 빠르게 잡 코드를 작성할 수 있으므로 간편하며, 경합 조건과 같은 멀티스레딩의 일부 위험을 방지하므로 더욱 안전합니다.

- **C# Joyb System(멀티 스레딩 활용 API) :** ECS는 실제 해결해야 하는 문제, 즉 게임을 구성하는 데이터와 동작을 집중적으로 다루는 코드 작성 방식입니다.
ECS를 사용하면 디자인 측면에서 더 나은 방식의 게임 프로그래밍이 가능할 뿐 아니라, Unity의 C# 잡 시스템과 버스트 컴파일러를 더욱 효과적으로 이용하여 최첨단 멀티코어 프로세서의 기능을 빠짐없이 활용할 수 있습니다.
Unity는 ECS를 통해 오브젝트 중심의 디자인에서 데이터 중심의 디자인으로 이동하고자 합니다. 이러한 변화를 통해 사용자 간에 코드를 이해하고 작성에 참여하거나 코드를 재사용하기가 더욱 수월해질 것입니다.
- **Burst Compiler(고도의 최적화 컴파일러) :** 새로운 LLVM 기반의 연산 인식 백엔드 컴파일러 기술을 통해 C# 작업을 처리하고 고도로 최적화된 코드를 작성할 수 있습니다.
또한 ECS 기반의 코드라면 코드 수정을 크게 하지 않고 쉽게 적용할 수 있습니다.

- **ECS & JobSystem & Burst Compolier 퍼포먼스**
  - 오브젝트를 만개 단위로 뿌려 FPS 30까지 얼마나 많은 오브젝트를 동시 실행할 수 있는지


| 작동 방식 | 오브젝트 개수 | 유튜브 영상 링크 |
| :---: | :---: | :---: |
| Classic | 18500개 | [링크](https://youtu.be/WZ6-LxwxWEI?t=2m51s) |
| Classic & Job System | 25000개 | [링크](https://www.youtube.com/watch?v=j2z5KRWZTDA) |
| ECS & Job System | 96000개 | [링크](https://youtu.be/D1KShj8ZV_I?t=12s) |
| ECS & Job System & Burst Compolier | 156000개 | [링크](https://youtu.be/D1KShj8ZV_I?t=1m57s) |


- 출처 링크 - 유니티 홈페이지에 소개된 설명
  - https://unity3d.com/kr/unity/features/job-system-ECS

### ECS 개발 세팅
- Unity 2018.01 버젼 이상 설치
- Unity - PlayerSetting - API Compatibility Level - .net 3.x -> .net 4.x로 변경
- Unity 2018버젼부터 생긴 Package Manager - ECS 설치
- Job System, Burst Compiler, IncrementalCompiler 설치
  - Job System, Burst Compolier의 경우 ECS & Job System에서 사용하기 때문에 설치하며,
  - IncrementalCompiler의 경우 ECS 코드에서 간혹 C# 7.0의 문법을 사용할 때 에러가 많은데, 이 Package가 해결해줍니다.

- Visual Studio 최신으로 설치
( VS 버젼이 오래되었을 경우 Unity 컴파일러와 VS 컴파일러가 따로 구동되어 VS에서 ECS 관련 스크립트 작성 불가 )

- 추천 개발 세팅 비디오
  - Brackeys / New way of CODING in Unity! ECS Tutorial
  - https://www.youtube.com/watch?v=_U9wRgQyy6s

### ECS 장단점

#### 장점

- 데이터 지향 개발을 사용하기 때문에, CPU 캐쉬메모리와 멀티 쓰레딩에 친화적. ( 성능 UP )
- 개발이 진행됨에 따라 생기는 예기치 못한 기능 추가 및 변경에 대해 보다 빠르게 대처할 수 있음.
- 코드의 상호 의존성이 없어 코드를 재사용하기 용이.
- 위와 마찬가지로 상호 의존성이 없어, 전체적으로 코드가 짧아져 코드 분석 및 유지보수가 용이.

![](https://pbs.twimg.com/media/DTOOMadX0AEdkVH.jpg)
사진 출처 유니티 테크니컬 에반젤리스트 Mike Geig 트윗 : https://twitter.com/mikegeig/status/951260836538003458

#### 단점

- 기존 객체 지향 개발 방식 **(OOP Object Oriented Develop)** 을 버리고 새로운 설계방식 **(DOP(Data Oriented Develop) - 데이터 지향 개발)** 을 사용해야 하기 때문에, 학습 및 개발 비용이 생김.
- 나온지 얼마 안된 기능으로, Research & Develop하기가 힘듦.
- Physics관련 기능을 ECS로 사용할 수 없음.

- 디버깅 관련
  - VS 디버그 - 중단점 기능을 지원하지 않음. ( 시도 시 VS 멈춤 & 유니티 응답 없음 )
  - Classic처럼 게임을 중단하여 렌더링 된 오브젝트를 클릭 시 오브젝트를 선택할 수 없다. ( Entity Debug - Entity를 선택해야 한다. )
  - Job System을 사용할 경우 멀티 스레딩 방식이기에 디버깅하기가 더 힘듦.

#### 결론

- **장단점은 결국 OOP와 DOP의 차이점이다.**
- 모든 스크립트를 ECS 기반으로 설계하는 것은 비효율적.
  - 대규모 오브젝트(성능을 요하는) 혹은 UI(재사용을 요하는)부분에만 ECS로 구현하는것이 좋음.
  - 절차위주나 그 외 **OCP(Open Close Principle, OOP - 개방 폐쇄의 원칙)** 을 적용하기 용이한 경우 - 구체적으로 게임 규칙의 경우 기존의 MonoBehaviour & Scriptable Object 방식으로 구현하는 것이 좋음.


---
## ECS

### 문법

#### ComponentData
- 컴포넌트 데이터는 변수만 들고있는 데이터 단위입니다.
- 권장 명명 규칙은 **~Component** 입니다.
  - Ex) MoveComponent, PositionComponent, RotationComponent 등
```csharp
// Pure ECS
[System.Serializable]
public struct ComponentData : IComponentData
{
    public float fValue;
    public int iValue;
}

// Hybrid  ECS
public class ComponentData : MonoBehaviour
{
  public float fValue;
  public int iValue;
}
```

#### Entity
- 컴포넌트 데이터를 가지고 있는 오브젝트입니다.
  - 다수의 컴포넌트 데이터를 가질 수 있습니다.
- [Hybrid 기준] Unity에서 GameObject에 기본적으로 제공되는 GameObjectEntity를 GameObject에 Attach하여야 ECS가 정상 동작합니다.

#### System
- ComponentData를 다루는 Manager격의 오브젝트입니다.
- 권장 명명 규칙은 **~System** 입니다.
  - Ex) MoveSystem, PositionSystem, RotationSystem 등

#### Filter & Data
- System 내부 Struct를 말하며, 말 그대로 선언한 타입으로 Entity를 걸러냅니다.
- GetEntities를 통해 Entity를 얻는 경우 Filter, [Inject]를 통해 상시 얻는 경우 Data라 명명하기도 합니다.
  - Infallible Code - ECS Tutorial 비디오 내 코드 중
- 권장 명명 규칙은 **Filter, 혹은 Data** 입니다.

#### Bootstrap
- ECS만으로는 Public 변수를 Inspector에 노출하여 사용자의 요구사항에 맞춰 설정할 수 없습니다.
- 그래서 이 역할을 하는 Monobehaviour 기반의 단순히 변수만을 들고있다가 ECS에 설정하는 스크립트를 Bootstrap이라 합니다.
  - 권장 명명 규칙은 **~Bootstrap** 입니다.
  - Ex) TimeScaleBootstrap

#### Convention Over Configuration
- Filter 역할을 하는 Struct에 Array와 readonly int형 Length를 선언하면,
Unity가 리플렉션을 통해 그에 맞는 길이를 변수에 넣습니다. int형 lengt 같이 유사하게 선언할 경우 작동하지 않습니다.
- 또한 선언한 ComponentArray 타입별로 논리연산 And 조건을 체크하여 Inject Attribute를 선언할 경우 자동으로 할당합니다.
  - 동적으로 Create, Destroy Entity를 할 경우에도 갱신됩니다.
```csharp
private struct Filter
{
  public int Length; // 이 필드는 자동으로 할당됩니다. - 옛날 버젼
  public readonly int Length; // 이 필드는 자동으로 할당됩니다. - 최신 버젼
  public ComponentArray<SomthingComponent> SomthingComponents
}
```

- Component Array를 2가지 이상 선언한 경우, 2가지가 모두 들어있는 것만 필터링됩니다.
```csharp
// A 혹은 B만 있는 경우 Filter에 포함이 안됩니다.
private struct Filter
{
    public readonly int Length; // A와 B 두개 다 들어있는 엔티티의 개수가 할당
    public ComponentArray<SomthingComponent_A> SomthingComponents_A;
    public ComponentArray<SomthingComponent_B> SomthingComponents_B;
}
```



### ECS 예시

#### Hybrid ECS
```csharp
using System.Collections;
using System.Collections.Generic;
using Unity.Entities;
using UnityEngine;

public class Rotater : MonoBehaviour
{
    public float fSpeed;
}

class RotaterSystem : ComponentSystem
{
    struct Components
    {
        public Rotater rotater;
        public Transform transform;
    }

    protected override void OnUpdate()
    {
        float fDeltaTime = Time.deltaTime;
        foreach (var e in GetEntities<Components>())
        {
            e.transform.Rotate(0f, e.rotater.fSpeed * fDeltaTime, 0f);
        }
    }
}
```

### Class & Interface

#### EntityArray
- Filter에 추가할 경우, 조건을 만족시킨 Entity를 Array에 할당합니다.
```csharp
private struct Filter
{
    public readonly int Length; // A가 있는 엔티티 개수만 할당
    public EntityArray Entities; // A가 있는 엔티티 Instsance를 할당
    public SubtractiveComponent<SomthingComponent_A> SomthingComponent;
}
```

#### SubtractiveComponent<ComponentData>
- Filter에 추가할 경우, 이 ComponentData가 있는 엔티티를 할당하지 않습니다.
```csharp
private struct Filter
{
    public readonly int Length; // A가 있으면서 B는 없는 엔티티의 개수만 할당
    public ComponentArray<SomthingComponent_A> SomthingComponent_A;
    public SubtractiveComponent<SomthingComponent_B> SomthingComponent_B;
}
```


---
## Job System

#### JobComponentSystem

#### IJobParallelFor
```csharp
public void Excute(int index);
```
- 반복문을 사용할 때 사용하는 Job입니다.


#### EntityCommandBuffer.Concurrent
- Job이 동작하는 중에 ( 멀티 스레드 환경에서 ) Add, Delete, Modify을 Thread-Safe하게 사용할 수 있는 버퍼입니다.

#### BarrierSystem
- 다른 스레드에서 메인 스레드로 요청하는 메시지 큐를 생성하는 시스템입니다.
  - Create / Destroy Entity, Add / Set / Remove Component Data 등을 요청합니다.


---
## 도움이 되는 링크

### Github

비디오를 시청 후 번호 순서대로 보시는 것을 추천합니다.

#### 1. Unity Tehcnologies / EntitiyComponentSystemSamples
- 유니티에서 제작한 ECS Sample 예제이며, 항상 최신버젼으로 업데이트됩니다.
  - https://github.com/Unity-Technologies/EntityComponentSystemSamples


#### 2. stella3d / job - system - cookbook
- 유니티에서 소개하는 C# Job System Sample 예제입니다.
  - https://github.com/stella3d/job-system-cookbook

#### 3. KptEmreU / Roll - A - Ball - ECS - style
- 어떤 개발자가 제작한 Pure ECS Style Roll a Ball 예제입니다.
  - https://github.com/KptEmreU/Roll-A-Ball-ECS-style

---
### Youtube Video

번호 순서대로 보시는 것을 추천합니다.

#### 1. Unity / Overview - Intro To The Entity Component System And C# Job System 1/5
- 유니티에서 ECS & Job System에 대해 개요부터 Classic ~ ECS & Job System 퍼포먼스 체크까지 설명합니다.
- 7~11여분 길이의 비디오가 총 5편으로, 코드보단 왜 ECS를 사용해야 하는지에 대해 초점이 맞춰져 있습니다.
  - https://www.youtube.com/watch?v=WLfhUKp2gag&list=PLX2vGYjWbI0S4yHZwjDI1boIrYStpBCdN

#### 2. Brackeys / New way of CODING in Unity! ECS Tutorial
- 유니티 및 개발 전문 방송 Brackeys에서 설명하는 ECS 튜토리얼입니다.
- 10분정도 길이이며, Hybrid ECS만 간단하게 설명합니다.
  - https://www.youtube.com/watch?v=_U9wRgQyy6s

#### 3. Infallible Code / Unity ECS Tutorial • Introduction
- 유니티 및 개발 전문 방송 Infallible Code에서 설명하는 ECS 튜토리얼 입니다.
- 10여분 정도 길이의 비디오가 총 7편으로, Hybrid ~ Pure ECS, Job System까지 슈팅게임 제작 기준으로 설명합니다.
  - https://www.youtube.com/watch?v=yzhsgaFVpZY

---
### 그 외 링크

#### [Unity ECS] All of the Unity’s ECS + Job system gotchas (so far)
- 유니티 ECS를 작업하면서 생기는 노하우 혹은 주의사항을 모아놓은 글입니다.
  - 내용이 상당히 세부적이며 많습니다.
- https://gametorrahod.com/all-of-the-unitys-ecs-job-system-gotchas-so-far-6ca80d82d19f

#### Burst User Guide
- 유니티 공식 Burst 컴파일러 메뉴얼 중 유저 가이드입니다.
- 위 문서에 Burst Compiler에 대해 따로 기입하지 않는 이유는 이 링크만 보셔도 무방하기 때문입니다.
- https://docs.unity3d.com/Packages/com.unity.burst@0.2/manual/index.html
