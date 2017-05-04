# FlowComponent

**FlowComponent를 사용하면 여러 화면 사이를 전환하고 탐색 할 수 있습니다.** <br>
새로운 레이어로 전환하는 `showNext`와 이전 레이어를 거쳐 순환하는 `showPrevious`라는 두 가지 기본 기능을 기반으로합니다. <br>
또한 모달과 같은 [오버레이](https://framer.com/docs/#flow.showOverlayCenter) 및 탭 막대와 같은 [고정 요소](https://framer.com/docs/#flow.header)를 디자인하는 데 사용할 수 있습니다. FlowComponent는 `Transition` 이벤트를 발생시킵니다. 그들에 대해 더 자세히 알아보십시오.

### Properties
`layer` — 대상 레이어 인 레이어 객체
> A layer object, the targeted layer.

`options` — 커브, 시간 등과 같은 모든 애니메이션 옵션을 가진 객체입니다. (선택 사항)
> An object with all the animation options like curve, time and more. (Optional)

```CS
# Create layer 
layerA = new Layer
    size: Screen.size
 
# Create FlowComponent 
flow = new FlowComponent
 
# Show the layer 
flow.showNext(layerA, animate: true)
```

## flow.showNext(layer, options)

새 레이어로 전환합니다. 기본적으로, FlowComponent에 추가 된 **첫 번째 레이어를 제외하고는 레이어에 애니메이션을 적용합니다**. 레이어의 너비 또는 높이가 부모의 너비 또는 높이를 초과하면 스크롤 할 수있게됩니다. 또한 수직 또는 수평 스크롤 가능 여부를 자동으로 감지합니다.

### Arguments
`layer` — 레이어 객체<br>
`options.animate` — boolean으로 레이어가 애니메이션으로 표시되는지 여부를 설정합니다. (선택 사항)<br>
`options.scroll` — boolean으로 레이어가 스크롤 가능한지 여부를 설정합니다. (선택 사항)<br>

```CS
# Create layer 
layerA = new Layer
    size: Screen.size
 
# Create FlowComponent 
flow = new FlowComponent
 
# Show the layer 
flow.showNext(layerA)
```

애니메이트를 `false`로 설정하면 전환없이 레이어간에 전환 할 수 있습니다.
> 자연스러운 애니메이션이 아닌 즉각적인 화면전환이 일어난다.

```CS
# Create layers 
layerA = new Layer
    size: Screen.size
    backgroundColor: "#00AAFF"
 
layerB = new Layer
    size: Screen.size
    backgroundColor: "#FFCC33"
 
# Create FlowComponent and show layer 
flow = new FlowComponent
flow.showNext(layerA)
 
# Instantly show layerB on click 
layerA.onClick ->
    flow.showNext(layerB, animate: false)
```

### flow.showPrevious(options)

이전 레이어로 전환합니다. 기본적으로 레이어에 애니메이션이 적용됩니다.

####Arguments
`options.animate` —  boolean으로 레이어가 애니메이션으로 표시되는지 여부를 설정합니다. (선택 사항)<br>
`options.scroll` —  boolean으로 레이어가 스크롤 가능한지 여부를 설정합니다. (선택 사항)<br>

```CS
# Create layer 
layerA = new Layer
layerB = new Layer
 
# Create FlowComponent 
flow = new FlowComponent
flow.showNext(layerA)
 
# Switch to layerA on click 
layerA.onClick ->
    flow.showNext(layerB)
 
# Return to the previous on click 
layerB.onClick ->
    flow.showPrevious()
```