# states(상태)

**states는 하나의 레이어에 여러 개의 속성을 저장해 놓고 이것을 애니메이션으로 ‘연결’하는 방법이다.**

- Framer는 애니메이션을 만드는 방식이 animate와 states가 있다.
- animate는 레이어에 애니메이션을 ‘추가’하는 방식이다.* 

> 모바일 앱 프로토타이핑 120.p
<br>

```정의
레이어 상태는 레이어 속성의 다양한 조합을 관리하고 구성 할 수 있습니다.
애니메이션을 대상으로 사용할 수 있습니다.

상태 전환(Switch)를 사용하면 즉시 다른 상태로 이동할 수 있으며
상태 사이클(Cycle)로 상태에서 상태로 순차적으로 이동할 수 있습니다.

x 및 y와 같은 상태에 레이어 속성을 추가 할 수 있습니다. 
html과 같은 애니메이션 가능하지 않은 레이어 속성은 상태 
애니메이션의 끝 부분에 설정됩니다.

상태에는 애니메이션 옵션 속성이있을 수 있습니다. 
레이어가 정의 된 상태로 애니메이션이 적용될 때마다 사용됩니다.

세 가지 사전 정의 된 상태는 이미 용도가 지정되어 있으므로 재정의 할 수 없습니다. 

당신은 name 속성을 사용하여 현재 및 이전에 대한 상태 이름을 가져올 수 있습니다
```

`default` — The initially active state : 초기 상태.<br>
`current` — The currently active state : 현재 활성 상태 <br>
`previous` — The previously active state. : 이전에 액티브 한 상태

#### Example: Create and delete a state - 상태를 만들고 지우기

``` CS
# Create a state (상태 만들기)
layerA.states.stateA =
    x: 100
 
# Delete a state (상태 지우기)
delete layerA.states.stateA
```
> 지울때는 delete를 먼저 선언해주고 지운다.

#### Example: A state with animation options - 상태에 애니메이션 옵션 주기
```CS
# Create a state with animationOptions  
( 애니메이션 옵션이 있는 상태 만들기)

layerA.states.stateA =
    x: 100
    animationOptions:
        curve: Spring(damping: 0.5)
        time: 0.5
```

#### Example: Animate to a state - 상태에 애니메이션 주기
```CS
# Create a state (상태 만들기)
layerA.states.stateA =
    x: 100
 
# Animate to the state (상태에 애니메이션 하기)
layerA.animate("stateA")
```

#### Example: Cycle through states - 사이클을 통한 상태
```CS
# Set multiple states at once (한번에 여러 상태를 설정하기)

layerA.states =
    stateA:
        x: 100
    stateB:
        x: 200
 
 
# On a click, go back and forth between states. 
(클릭을 할때 마다 상태가 왔다갔다 한다)

layerA.onTap ->
    layerA.stateCycle("stateA", "stateB")
```
## layer.states.current [object]
현재 활성 상태의 객체를 반환합니다.
> Returns an object of the currently active state.

### Properties
`name` — 상태 객체의 이름을 반환하는 읽기 전용 속성입니다.
> A read-only property that returns the name of the state object.

``` CS
layerA = new Layer
 
layerA.states.stateA =
    x: 500
    opacity: 0.5
 
layerA.stateSwitch("stateA")
 
print layerA.states.current
# Output: <Object State> 
 
print layerA.states.current.name
# Output: stateA 
```

> 여기에서 layereA.stateSwitch("stateA")를 하면 layerA의 상태가 **stateA의 상태로 바로 바꾸라는 코드**<br>
> layerA.states.current는 layerA의 **현재 상태를 알려달려는 코드** 그리고 print는 그걸 검사창에 글로 보여줌<br>
> print layerA.states.current.name는 레이어A의 현재 상태의 이름을 알려주라는 뜻 여기서는 **stateA**

## layer.states.previous [object]

이전에 액티브 한 상태의 객체를 돌려줍니다.
> Returns an object of the previously active state.

### Properties
`name` —  상태 객체의 이름을 반환하는 읽기 전용 속성입니다.
> A read-only property that returns the name of the state object.

```CS
layerA = new Layer
 
layerA.states.stateA =
    x: 500
    opacity: 0.5
 
layerA.stateSwitch("stateA")
 
print layerA.states.previous
# Output: <Object State> 
```

## layer.stateSwitch(name)

애니메이션이 되지 않은채 상태가 즉각적으로 바뀐다.
> layer.states.switchInstant()는 더이상 사용되지 않는다.

### Arguments
`name `— 문자열, 상태의 이름
> A string, the name of the state.

```CS
layerA = new Layer
 
layerA.states.stateA =
    x: 100
 
layerA.stateSwitch("stateA")
```


## layer.stateCycle(states, options)
모든 레이어 상태를 순환합니다. 일단 우리가 사이클의 끝까지 도달하면 우리는 처음부터 다시 시작합니다. <br>
순서가 추가되지 않은 경우 주문 상태에 대한 배열을 제공 할 수 있습니다.

애니메이션 옵션 매개 변수를 추가하여 한 사이클의 애니메이션을 변경할 수도 있습니다.
> layer.states.next() 는 더이상 사용되지 않습니다.

### Arguments
`states` — 상태의 이름의 배열 (옵션사항)
> An array of state names. (Optional) 

`options` — 커브, 시간 등과 같은 모든 애니메이션 옵션을 가진 객체입니다. (옵션사항)
> An object with all the animation options like curve, time and more. (Optional)

```CS
layerA = new Layer
 
layerA.states =
    stateA:
        x: 100
    stateB:
        x: 200
 
# Every time we call this we cycle to the next state 
(우리가 이 사이클을 부를 때마다 다음 상태가 됩니다.)

layerA.stateCycle(["stateA", "stateB"])
```
