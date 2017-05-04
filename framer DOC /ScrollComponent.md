#ScrollComonent
ScrollComponent는 내용을 스크롤하는 데 사용됩니다. 운동량과 스프링 물리학을 구현하고, 맞춤화(customization)를 허용하며, 다양한 이벤트를 내 보냅니다.
<br><br>
ScrollComponent는 두 개의 레이어로 구성됩니다. ScrollComponent 자체는 내용(content)을 가리는 레이어입니다. 그것은 draggable 활성화 및 제약 조건이 구성되어있는 콘텐츠 레이어가 있습니다. 이는 컨텐츠 레이어의 하위 레이어의 총 크기를 기반으로 컨텐츠 레이어의 크기를 자동으로 관리합니다.

```CS
# Create a new ScrollComponent 
scroll = new ScrollComponent
    width: 100
    height: 100
 
# Include a Layer 
layerA = new Layer
    parent: scroll.content
```
ScrollComponent.wrap ()을 사용하여, ScrollComponent 내에 기존 레이어를 감쌀 수 할 수도 있습니다. ScrollComponent는 내용과 슈퍼 레이어 사이에 자신을 삽입합니다. 이 기능은 Sketch 또는 Photoshop에서 디자인을 가져 와서 레이어를 스크롤 가능하게 만들 때 유용합니다. 학습 섹션에서 줄 바꿈에 대해 [자세히](https://framer.com/docs/#scroll.wrap) 배울 수 있습니다. 

```CS
layerA = new Layer
    width: 300
    height: 300
 
scroll = ScrollComponent.wrap(layerA)
```

## scroll.content [layer]
내용(content)을 추가 할 레이어입니다. 내용(content)을 추가하려면 새 레이어를 만들고 해당 `부모(parent)`를 `scroll.content` 레이어로 설정합니다. 컨텐츠가 ScrollComponent에 적합하지 않은 경우, 클립됩니다.

```CS
scroll = new ScrollComponent
    width: 100
    height: 100
 
layerA = new Layer
    parent: scroll.content
    image: "images/bg.png"
    width: 100
    height: 200
```

## scroll.contentInset [object]
내용 삽입(Inset for the content). 이렇게 하면 콘텐츠가 제약 조건과 실제 콘텐츠 레이어 사이에 여분의 패딩을 제공합니다.

```CS
scroll = new ScrollComponent
    width: 100
    height: 100
 
layerA = new Layer
    parent: scroll.content
    image: "images/bg.png"
    width: 100
    height: 200
 
scroll.contentInset =
    top: 20
    right: 0
    bottom: 20
    left: 0
```

