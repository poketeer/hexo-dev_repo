---
title: React DnD - React에서 Drag & Drop을 사용하자.
categories: react
tags:
- react-dnd
- react
---
## 시작하기에 앞서
이 글은 [React DnD 공식 사이트](http://react-dnd.github.io/react-dnd/docs-overview.html)를 참고하여 작성하였으며, 읽으며 정리용으로 쓴 글로 번역문으로 보일 수도 있습니다.

## React-dnd란?
React-dnd는 React의 특징중 하나인 Higher-Order Components를 사용하는 Drag & Drop을 위한 라이브러리 중 하나이다. backend로는 [HTML5의 drag and drop API](https://developer.mozilla.org/en-US/docs/Web/API/HTML_Drag_and_Drop_API)를 사용하고 있다. 이 때문에 모바일에서의 drag & drop은 지원할 수 없는 단점이 있지만, 추후에 개선될거라고 한다.
React-dnd는 내부에서 Redux를 사용하는데, DOM 이벤트를 React DnD가 처리할 수 있는 내부의 Redux 액션으로 변환한다. React DnD가 처리할 수 있는 데이터로는 Item와 Type가 있다. 앞으로는 React DnD에서 사용하는 구성요소들을 알아보겠다.

## Items와 Types 
React DnD에서는 화면에서 어떤 것이든 드래그 할 때, 컴포넌트나 DOM node가 드래그 되고 있다고 하지 않는다. 대신, 특정 Type의 Item이 드래그 된다고 한다.
Item이란, 어떤 것이 드래그 되고 있는지를 알려주는 단순한 JavaScript Object이다. 예를 들어, 체스게임에서 게임 말을 집었을 때, Item은 { fromCell: 'C5', piece: 'queen' }처럼 될 것이다. 이처럼 드래그된 데이터를 단순한 Object로 묘사하는 것은 컴포넌트가 서로 모르게 해준다.
Type은 당신의 App에서 Item을 유일하게 구분하는데 사용되는 문자열(또는 [symbol](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Global_Objects/Symbol))이다. 체스게임에서라면, '게임 말' Type을 정의할 수 있을 것이다. Type은 어떤 drage source와 drop target이 서로 호환되는지를 명세하게 해준다.

## Monitor
Drag & Drop은 본질적으로 상태기반이다. 상태는 드래그 되고 있는지 아닌지 등이 될 수 있다.
React DnD는 상태를 Monitor라 불리는 내부 상태 저장소를 통해 당신의 컴포넌트에 전해진다. **Monitor는 당신이 Drag & Drop의 상태 변화에 따라, 당신의 컴포넌트의 prop을 업데이트해준다.** Drag & Drop 상태를 추적하는 각 컴포넌트를 위해, 당신은 Monitor로부터 관련된 정보를 받는 collect 함수를 정의해줘야 한다.

체스에서 '게임 말'이 드래그될 때, 체스 셀을 강조하고 싶다고 해보자. `Cell` 컴포넌트를 위한 collect 함수는 다음과 같은 것이다.

```javascript
function collect(monitor) {
  return {
    highlighted: monitor.canDrop(),
    hovered: monitor.isOver()
  };
}
```
이것은 React DnD에게 `highlighted`와 `hovered`의 최신값을 모든 `Cell` 인스턴스에 prop으로 전달해 주도록 지시하는 코드이다. 

## Connector
만약 백엔드가 DOM 이벤트를 다루지만, 컴포넌트가 DOM을 묘사하기 위해 React를 사용한다면, 백엔드는 어떤 DOM node에 대기하고 있는지를 어떻게 알 수 있을까. 이를 해결하기 위해, Connector가 필요하다. **Connector는 당신의 `render` 함수에서 미리 정의된 역할(drag source, drag preview, drop target)중 하나를 DOM node에 할당하도록 해준다.**

사실, Connector는 collect 함수에서 monitor와 함께 매개변수로 사용된다. Connector를 사용해서 어떻게 drop target을 명시하는지 보자.
```javascript
function collect(connect, monitor) {
  return {
    highlighted: monitor.canDrop(),
    hovered: monitor.isOver(),
    connectDropTarget: connect.dropTarget()
  };
}
```

컴포넌트의 `render` 함수에서, 우리는 monitor로부터 얻어진 데이터와 connector로부터 얻어진 함수 모두에 접근할 수 있다.

```javascript
render() {
  const { highlighted, hovered, connectDropTarget } = this.props;

  return connectDropTarget(
    <div className={classSet({
      'Cell': true,
      'Cell--highlighted': highlighted,
      'Cell--hovered': hovered
    })}>
      {this.props.children}
    </div>
  );
}
```

`connectDropTarget` 호출은 React DnD에게 우리 컴포넌트의 root DOM node가 유효한 drop target이고, 이것의 hover와 drop 이벤트가 백엔드에 의해서 다뤄져야만 한다는 것을 알려준다. 


## Higher-Order Components와 ES7 decorators에 대해
Higher-Order Components를 처음 듣는다면, [React 공식문서의 아티클](https://facebook.github.io/react/docs/higher-order-components.html)과 [Mixins Are Dead. Long Live Composition](https://medium.com/@dan_abramov/mixins-are-dead-long-live-higher-order-components-94a0d2f9e750)를 읽어보기를 권한다.

**higher-order 컴포넌트는 단지 React 컴포넌트 클래스를 가지고, 다른 React 컴포넌트 클래스를 반환하는 함수이다.** 라이브러리에 의해 제공된 Wrapping 컴포넌트는 `render` 함수 안 당신의 컴포넌트를 렌더링하고 prop을 당신의 컴포넌트에 전달한다. 또한, 몇몇 유용한 기능도 추가해준다.

React DnD에서, [DragSource](http://react-dnd.github.io/react-dnd/docs-drag-source.html)와 [DragTarget](http://react-dnd.github.io/react-dnd/docs-drop-target.html)은 사실 higher-order 컴포넌트이다. 

이제 당신의 컴포넌트를 [DragSource](http://react-dnd.github.io/react-dnd/docs-drag-source.html)로 감싸는지 알아보자.
```javascript
import { DragSource } from 'react-dnd';

class YourComponent {
  /* ... */
}

export default DragSource(/* ... */)(YourComponent);
```

맨 마지막 줄에서 추가로 감싸는 과정이 번거롭다고 생각할 수도 있다.
이를 해결하기 위해 ES7에 추가된 [decorator syntax](https://github.com/wycats/javascript-decorators)를 사용할 수 있다. 물론 아직 ES7을 지원하는 브라우저는 많지 않으므로 Babel를 사용해야 한며, 이미 ES6를 위해 Babel을 사용하고 있었다면 .babelrc 파일에 `{ "stage": 1 }`을 추가해주면 된다.

## 한데 모아서 보자
마지막으로 지금까지 설명한 요소들을 사용하는 예제를 보도록 하자. 다음 예제는 Card 컴포넌트를 drag source로 감싸는 예제이다.

```javascript
import React from 'react';
import { DragSource } from 'react-dnd';

// Drag sources and drop targets only interact
// if they have the same string type.
// You want to keep types in a separate file with
// the rest of your app's constants.
const Types = {
  CARD: 'card'
};

/**
 * Specifies the drag source contract.
 * Only `beginDrag` function is required.
 */
const cardSource = {
  beginDrag(props) {
    // Return the data describing the dragged item
    const item = { id: props.id };
    return item;
  },

  endDrag(props, monitor, component) {
    if (!monitor.didDrop()) {
      return;
    }

    // When dropped on a compatible target, do something
    const item = monitor.getItem();
    const dropResult = monitor.getDropResult();
    CardActions.moveCardToList(item.id, dropResult.listId);
  }
};

// Use the decorator syntax
@DragSource(Types.CARD, cardSource, (connect, monitor) => ({
  // Call this function inside render()
  // to let React DnD handle the drag events:
  connectDragSource: connect.dragSource(),
  // You can ask the monitor about the current drag state:
  isDragging: monitor.isDragging()
}))
export default class Card {
  render() {
    // Your component receives its own props as usual
    const { id } = this.props;

    // These two props are injected by React DnD,
    // as defined by your `collect` function above:
    const { isDragging, connectDragSource } = this.props;

    return connectDragSource(
      <div>
        I am a draggable card number {id}
        {isDragging && ' (and I am being dragged now)'}
      </div>
    );
  }
}
```

## 마치며



## 참고 링크
- [React-dnd](http://react-dnd.github.io/react-dnd/docs-overview.html)
- [Higher-Order Components](https://facebook.github.io/react/docs/higher-order-components.html)
- [ES7 decorators](https://medium.com/google-developers/exploring-es7-decorators-76ecb65fb841)