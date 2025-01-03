# 주제: [[GoJS]]
# GoJS Tutorials
- 대화형(interactive) 다이어그램을 구현하기 위한 JavaScript의 라이브러리

## GoJS 라이브러리 연결
- 라이브러리를 컴퓨터에 다운로드한 경우
```html
<script src="go-debug.js"></script>
```
- CDN에서 제공하는 GoJS 라이브러리에 바로 연결
```HTML
<script src="https://cdn.jsdelivr.net/npm/gojs/release/go-debug.js"></script>
```

## GoJS 다이어그램의 위치
- 각각의 GoJS 다이어그램은 HTML 페이지에서 크기를 지정하는 HTML `<div>`요소에 포함되어 있다.
```HTML
<div id="myDiagramDiv" style="width:400px; height:150px; background-color: #DAE4E4;"></div>
```
- JavaScript 코드에서 다이어그램을 만들 때 `<div>`의 ID를 전달한다.
```JS
const myDiagram = new go.Diagram("myDiagramDiv");
```
- 위의 HTML과 JS 코드로 빈 다이어그램이 생성된다.
- `go`는 GoJS의 모든 유형이 있는 namespace다. GoJS 클래스(Diagram, Node, Panel, Shape, TextBlock)를 사용하는 모든 코드 앞에는 `go.`접두사가 붙는다.

# Diagrams and Models
- 다이어그램의 노드와 링크는 데이터를 시각화한 것이며 그 데이터는 모델을 통해 관리된다.
- GoJS는 model-view 구조이다
	- model: 모델은 노드와 링크를 설명하는 데이터(JavaScript 객체 배열)를 보관
	- view: 다이어그램은 실제 노드 및 링크 객체를 사용하여 이 데이터를 시각화하는 뷰 역할
	- 모델의 데이터 객체에서 앱에 필요한 속성을 추가할 수 있지만 Diagram 및 GraphObject 클래스의 프로토타입에 속성을 추가하거나 수정할 수 없다.
	- ⇒ 모델을 로드하고, 편집하고, 저장하는 것이다.
```JS
// You can specify options in the Diagram's second argument
// These options not only include Diagram properties, but sub-properties, too.
const myDiagram =
	  new go.Diagram("myDiagramDiv",
		  {// enable Ctrl-Z to undo and Ctrl-Y to redo
			  "undoManager.isEnabled": true
		  }
	  );

myDiagram.model = new go.Model(
	[ // for each object in this Array, the Diagram creates a node to represent it
		{ text: "Alpha" },
		{ text: "Beta" },
		{ text: "Gamma" },
	]
);
```
![[SmartSelect_20241112_085808_Whale.jpg]]
- 다이어그램은 모델에 있는 세개의 노드를 표시한다.
- 상호 작용이 가능한 기능
	- 화면 이동: 다이어그램의 배경을 클릭하고 드래그하여 화면을 이동할 수 있다.
	- 노드 선택 및 이동: 노드를 선택하기 위해 클릭하거나, 드래그하여 노드를 움직일 수 있다.
	- 선택 상자: 선택 상자를 만들려면 배경을 길게 클릭한 다음 드래그를 시작한다.
	- 복사본: Ctrl-C 및 Ctrl-V를 사용하거나 Ctrl-드래그, 드롭을 사용해 선택한 것들의 복사본을 만들 수 있다.
	- 삭제: Delete 키를 눌러 선택한 노드를 삭제한다.
	- 컨텍스트 메뉴: 터치 장치에서는 길게눌러 컨텍스트 메뉴를 불러온다.
	- 실행 취소: 실행 취소 관리자가 활성화되었으므로, Ctrl-Z 및 Ctrl-Y로 이동, 복사 및 삭제를 실행 취소하고 다시 실행한다.

# Styling Nodes(노드 스타일 지정)
- 노드는 GraphObjects로 구성된 템플릿을 생성하고 해당 오브젝트에 프로퍼티를 설정하여 스타일을 지정한다.
	- building block classes: 노드를 만들기 위한 몇 가지 클래스
		- **Shape**: 사선 정의되거나 사용자 정의된 지오메트리(custom geometry)를 색상과 함께 표시
		- **TextBlock**: 다양한 글꼴로 (편집 가능한) 텍스트를 표시
		- **Picture**: SVG 파일을 포함한 이미지를 표시
		- **Panel**: 패널의 유형에 따라 다양한 방식으로 배치하고 크기를 조정할 수 있는 기타 object들의 조합(collection)을 담는 컨테이너(like tables, vertical stacks, and stretching containers)
		- GraphObject 추상 클래스에서 파생되었으므로 GraphObject 또는 객체 또는 요소라고 지칭한다.
		- GraphObject는 HTML DOM요소가 아니므로 이러한 객체를 만들거나 수정할 때 오버헤드가 훨씬 적다.
## 데이터 바인딩(data binding)
- 데이터 바인딩을 통해 모델의 데이터 속성과 노드가 연결된다.
- 데이터 바인딩을 사용하면 GraphObject의 속성을 **모델의 데이터에서 가져온 값으로 자동 설정하여 GraphObject의 모양과 동작을 변경할 수 있다.**
## 기본 노드 템플릿
-  하나의 텍스트 블록을 포함하는 노드
- 텍스트 블록의 텍스트 프로퍼티와 모델 데이터의 키 프로퍼티 사이에 **데이터 바인딩**이 있다.
```JS
myDiagram.nodeTemplate = 
	new go.Node()
		.add(
			new go.TextBlock()
				.bind("text") // TextBlock.text is bound to Node.data.text
		)
```
## 일반적인 노드 템플릿의 골격
```JS
myDiagram.nodeTemplate = 
	new go.Node("Vertical", // first argument of a Node (or any Panel) can be a Panel type
		/* set Node properties here */
		{ // the Node.location point will be at the center of each node
			locationSpot: go.Spot.Center
		}
	)
	/* then add Bindings here */
	// example Node binding sets Node.location to the value of Node.data.loc
	.bind("location", "loc", go.Point.parse)

	/* add GraphObjects contained within the Node */
	//  this shape will be vertically above the TextBlock
	.add(
		new go.Shape("RoundedRectangle", // string argument can name a predefined figure
			{ /* set Shape properties here */ }
		)
		// example Shape binding sets Shape.figure to the value of Node.data.fig
		.bind("figure", "fig"),
		new go.TextBlock("default text", // string argument can be initial text string
			{ /* set TextBlock properties here */ }
		)
		// example TextBlock binding sets TextBlock.text to the value of Node.data.text
		.bink("text")
	);
```
주석을 제거한 경우
```JS
// The same Node template as above
myDiagram.nodeTemplate = 
	new go.Node("Vertical", { locationSpot: go.Spot.Center })
	.bind("location", "loc", go.Point.parse)
	.add(
		new go.Shape("RoundedRectangle")
		.bind("figure", "fig"),
		new go.TextBlock("default text")
		.bind("text")
	)
```
- Panel 내 GraphObject는 임의로 깊게 중첩할 수 있다.(=계속해서 추가할 수 있다.)

## 실제 볼 수 있는 예제(이름 옆에 이미지)
- "가로(Horizontal)" 패널 유형의 노드로 요소가 가로로 나란히 배치된다.
- 사용되는 요소(element)
	- 이미지 소스 데이터가 바인딩된 초상화를 위한 그림
	- 이름을 위한 텍스트 블록(텍스트 데이터가 바인딩됨)
```js
const myDiagram = 
	new go.Diagram("myDiagramDiv",
		{ // enable Ctrl-Z to undo and Ctrl-Y to redo
			"undoManager.isEnabled": true
		}
	);

// define a simple Node template
myDiagram.nodeTemplate = 
	new go.Node("Horizontal",
		// the entire node will have a light-blue background
		{ background: "#rrCCFF"}
	)
	.add(
		new go.Picture(
			//Pictures should normally have an explicit width and height.
			// This picture has a red background, only visible when there is no source set
			// or when the image is partially transparent.
			{ margin: 10, width: 50, height: 50, background: "red" }
		)
		// Picture.source is data bound to the "source" attribute of the nodel data
		.bind("source")
	),
	new go.TextBlock("Default Text", // the initial value for TextBlock.text
		// some room around the text, a larger font, and a white stroke:
		{ margin: 12, stroke: "white", font: "bold 16px sans-serif" }
	)
	.bind("text", "name")
);

myDiagram.model = new go.Model(
	[ // note that each node data object holds whatever properties it needs;
	  // for this app we add the "name" and "source" properties
	  // because in our template above, we have defined bindings to expect them
		{ name: "Don Meow", source: "cat1.png" },
		{ name: "Copricat", source: "cat2.png" },
		{ name: "Demeter", source: "cat3.png" },
		{ /* Empty node data, to show a node with no values from bindings */ } // 비어있는 노드 데이터도 잘 작동할 수 있다.
	]
);
```

# Model의 종류
- 사용자 정의 노트 템플릿을 통해 다이어그램이 예뻐질 수는 있지만 조직도 등을 보여주기엔 한계가 있다.
- GraphLinksModel, TreeModel
	- 링크를 지원하는 GoJS의 다른 2 모델
	- GraphLinksModel에 있는 `model.nodeDataArray`와 `model.linkDataArray`에는 "to" 및 "from" 노드 키를 지정하여 링크를 설명하는 JavaScript 객체 배열이 들어있다.
```js
myDiagram.model = new go.GraphLinksModel(
	[ // the nodeDataArray
		{ key: "A" },
		{ key: "B" },
		{ key: "C" },
	],
	[ // the linkDataArray
		{ from: "A", to: "B" },
		{ from: "B", to: "C" },
	]
);
```




















