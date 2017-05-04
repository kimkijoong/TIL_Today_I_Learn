
# PageComponent

PageComponent는 ScrollComponent를 기반으로 하지만 연속 된 내용 대신 페이지 매김을 표시하도록 설계되었습니다. 다양한 크기의 컨텐츠 레이어를 지원하며 위치 및 스크롤 속도에 따라 레이어에 스냅 할 수 있습니다

```
# Create a new PageComponent and only allow horizontal scrolling. 
# 새로운 PageComponent를 만들고 수평 스크롤링만 되는 것을 만들자
page = new PageComponent
    width: Screen.width
    height: Screen.height
    scrollVertical: false
 
 
# Define the first page 
# 첫번째 페이지를 정의하자
pageOne = new Layer
    width: page.width
    height: page.height
    parent: page.content
    backgroundColor: "#28affa"
```

이제 두 번째 페이지를 추가합시다. [addPage 메소드](https://framer.com/docs/#page.addPage)에 대해 자세히 읽어보십시오.

```CS
# Define second page 
pageTwo = new Layer
    width: page.width
    height: page.height
    backgroundColor: "#90D7FF"
 
# Add the second page to the right 
page.addPage(pageTwo, "right")
```
컨텐츠를 추가하는 또 다른 방법은 [for-loop](https://framer.com/getstarted/programming/#loops-and-arrays)를 사용하는 것입니다.

```CS
# 새로운 PageComponent를 만들고 수평 스크롤링만 되는 것을 만들자
page = new PageComponent
    width: Screen.width
    height: Screen.height
    scrollVertical: false
    backgroundColor: "#fff"
 
# Create 5 new layers and add them to the page.content 
# 5개의 레이어들을 만들고 각 page.content를 추가하자
for number in [0...5]
    pageContent = new Layer
        width: page.width
        height: page.height
        x: page.width * number
        backgroundColor: Utils.randomColor(0.5)
        parent: page.content
 
    # Visualize the current page number 
    # 현재 페이지 넘버를 시각화하자
    pageContent.html = pageContent.html = number + 1
 
    # Center the current page number
    # 현재 페이지 넘버를 가운데 정렬하자 
    pageContent.style =
        "font-size" : "100px",
        "font-weight" : "100",
        "text-align" : "center",
        "line-height" : "#{page.height}px"
```

## page.addPage(direction)
PageComponent의 page.content 레이어에 새 페이지를 추가합니다.<br>
두 인수가 필요합니다 : layer (page)와 direction ( `"right"`또는 `"bottom"`)
> `right`를 하면 첫번째 레이어의 오른쪽에 생성, 첫번째 레이어의 width값 만큼의 x값을 가진다. <br>
> `bottom`을 하면 첫번째 레이어의 하단에 생성, 첫번째 레이어의 height값 만큼의 y값을 가진다.

```CS
page = new PageComponent
    width: Screen.width
    height: Screen.height
 
# The first page, placed directly within the page.content 
# 첫 페이지는 page.content 안에 직접 배치됩니다.
pageOne = new Layer
    width: page.width
    height: page.height
    parent: page.content
    backgroundColor: "#28affa"
 
# Second page 
pageTwo = new Layer
    width: page.width
    height: page.height
    backgroundColor: "#90D7FF"
 
# Third page 
pageThree = new Layer
    width: page.width
    height: page.height
    backgroundColor: "#CAECFF"
 
 
# Add the second and third page to the right 
page.addPage(pageTwo, "right")
page.addPage(pageThree, "right")
```

왼쪽에 페이지를 추가하려는 경우 처음에는 오른쪽에 추가하고 [snapToPage()](https://framer.com/docs/#page.snapToPage)를 사용하여 다른 페이지로 즉시 전환 할 수 있습니다.
>  이런식으로 하면 두번째 추가한 페이지가 화면에 바로 전환되어 두번째 페이지가 보이고, 첫번째 페이지가 왼쪽으로 밀려서 보이지 않는다.

```CS
page = new PageComponent
    width: Screen.width
    height: Screen.height
 
pageOne = new Layer
    width: page.width
    height: page.height
    parent: page.content
    backgroundColor: "#28affa"
 
pageTwo = new Layer
    width: page.width
    height: page.height
    backgroundColor: "#90D7FF"
 
# Add a page to the right 
page.addPage(pageTwo, "right")
 
# Start at the second page by default 
page.snapToPage(pageTwo, false)
```

## page.snapToPage(page, animate, animationOptions)
**특정 페이지에 스냅된다.** 세 개의 인수를 가질 수 있다 :  page.content layer, animate (true 또는 false), [animation options](https://framer.com/docs/#animation.animation). 기본적으로, animate은 true로 설정되고 animationCurve는 spring curve를 사용한다.

```CS
page = new PageComponent
    width: Screen.width
    height: Screen.height
 
pageOne = new Layer
    width: page.width
    height: page.height
    parent: page.content
    backgroundColor: "#28affa"
 
pageTwo = new Layer
    width: page.width
    height: page.height
    backgroundColor: "#90D7FF"
 
page.addPage(pageTwo, "right")
 
# Automatically scroll to pageTwo 
page.snapToPage(pageTwo)
```
> 여기서는 page.content layer를 pageTwo인자를 넣어서 두번째 페이지가 스냅핑 되게 했다. <br>
>  나머지는 디폴트 값을 사용하여(생략된), 스프링 커브값을 가진 애니메이션은 작동한다.

위 예제에서 사용자 정의 animationOptions를 정의하여 스크롤 애니메이션을 사용자 정의 할 수 있습니다.

```CS
# Define a slower easing curve 
# 느린 이징 커브를 정의하기
page.snapToPage(
    pageTwo
    true
    animationOptions = time: 2
)
```