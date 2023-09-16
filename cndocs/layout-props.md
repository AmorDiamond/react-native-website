---
id: layout-props
title: 布局属性
---

import Tabs from '@theme/Tabs'; import TabItem from '@theme/TabItem'; import constants from '@site/core/TabsConstants';

> More detailed examples about those properties can be found on the [Layout with Flexbox](flexbox) page.

### 示例

The following example shows how different properties can affect or shape a React Native layout. You can try for example to add or remove squares from the UI while changing the values of the property `flexWrap`.

<Tabs groupId="language" queryString defaultValue={constants.defaultSnackLanguage} values={constants.snackLanguages}>
<TabItem value="javascript">

```SnackPlayer name=LayoutProps%20Example&ext=js
import React, {useState} from 'react';
import {
  Button,
  ScrollView,
  StatusBar,
  StyleSheet,
  Text,
  View,
} from 'react-native';

const App = () => {
  const flexDirections = ['row', 'row-reverse', 'column', 'column-reverse'];
  const justifyContents = [
    'flex-start',
    'flex-end',
    'center',
    'space-between',
    'space-around',
    'space-evenly',
  ];
  const alignItemsArr = [
    'flex-start',
    'flex-end',
    'center',
    'stretch',
    'baseline',
  ];
  const wraps = ['nowrap', 'wrap', 'wrap-reverse'];
  const directions = ['inherit', 'ltr', 'rtl'];
  const [flexDirection, setFlexDirection] = useState(0);
  const [justifyContent, setJustifyContent] = useState(0);
  const [alignItems, setAlignItems] = useState(0);
  const [direction, setDirection] = useState(0);
  const [wrap, setWrap] = useState(0);

  const hookedStyles = {
    flexDirection: flexDirections[flexDirection],
    justifyContent: justifyContents[justifyContent],
    alignItems: alignItemsArr[alignItems],
    direction: directions[direction],
    flexWrap: wraps[wrap],
  };

  const changeSetting = (value, options, setterFunction) => {
    if (value === options.length - 1) {
      setterFunction(0);
      return;
    }
    setterFunction(value + 1);
  };
  const [squares, setSquares] = useState([<Square />, <Square />, <Square />]);
  return (
    <>
      <View style={{paddingTop: StatusBar.currentHeight}} />
      <View style={[styles.container, styles.playingSpace, hookedStyles]}>
        {squares.map(elem => elem)}
      </View>
      <ScrollView style={styles.container}>
        <View style={styles.controlSpace}>
          <View style={styles.buttonView}>
            <Button
              title="Change Flex Direction"
              onPress={() =>
                changeSetting(flexDirection, flexDirections, setFlexDirection)
              }
            />
            <Text style={styles.text}>{flexDirections[flexDirection]}</Text>
          </View>
          <View style={styles.buttonView}>
            <Button
              title="Change Justify Content"
              onPress={() =>
                changeSetting(
                  justifyContent,
                  justifyContents,
                  setJustifyContent,
                )
              }
            />
            <Text style={styles.text}>{justifyContents[justifyContent]}</Text>
          </View>
          <View style={styles.buttonView}>
            <Button
              title="Change Align Items"
              onPress={() =>
                changeSetting(alignItems, alignItemsArr, setAlignItems)
              }
            />
            <Text style={styles.text}>{alignItemsArr[alignItems]}</Text>
          </View>
          <View style={styles.buttonView}>
            <Button
              title="Change Direction"
              onPress={() => changeSetting(direction, directions, setDirection)}
            />
            <Text style={styles.text}>{directions[direction]}</Text>
          </View>
          <View style={styles.buttonView}>
            <Button
              title="Change Flex Wrap"
              onPress={() => changeSetting(wrap, wraps, setWrap)}
            />
            <Text style={styles.text}>{wraps[wrap]}</Text>
          </View>
          <View style={styles.buttonView}>
            <Button
              title="Add Square"
              onPress={() => setSquares([...squares, <Square />])}
            />
          </View>
          <View style={styles.buttonView}>
            <Button
              title="Delete Square"
              onPress={() =>
                setSquares(squares.filter((v, i) => i !== squares.length - 1))
              }
            />
          </View>
        </View>
      </ScrollView>
    </>
  );
};

const styles = StyleSheet.create({
  container: {
    height: '50%',
  },
  playingSpace: {
    backgroundColor: 'white',
    borderColor: 'blue',
    borderWidth: 3,
  },
  controlSpace: {
    flexDirection: 'row',
    flexWrap: 'wrap',
    backgroundColor: '#F5F5F5',
  },
  buttonView: {
    width: '50%',
    padding: 10,
  },
  text: {textAlign: 'center'},
});

const Square = () => (
  <View
    style={{
      width: 50,
      height: 50,
      backgroundColor: randomHexColor(),
    }}
  />
);

const randomHexColor = () => {
  return '#000000'.replace(/0/g, () => {
    return Math.round(Math.random() * 16).toString(16);
  });
};

export default App;
```

</TabItem>
<TabItem value="typescript">

```SnackPlayer name=LayoutProps%20Example&ext=tsx
import React, {useState} from 'react';
import {
  Button,
  ScrollView,
  StatusBar,
  StyleSheet,
  Text,
  View,
} from 'react-native';

const App = () => {
  const flexDirections = [
    'row',
    'row-reverse',
    'column',
    'column-reverse',
  ] as const;
  const justifyContents = [
    'flex-start',
    'flex-end',
    'center',
    'space-between',
    'space-around',
    'space-evenly',
  ] as const;
  const alignItemsArr = [
    'flex-start',
    'flex-end',
    'center',
    'stretch',
    'baseline',
  ] as const;
  const wraps = ['nowrap', 'wrap', 'wrap-reverse'] as const;
  const directions = ['inherit', 'ltr', 'rtl'] as const;
  const [flexDirection, setFlexDirection] = useState(0);
  const [justifyContent, setJustifyContent] = useState(0);
  const [alignItems, setAlignItems] = useState(0);
  const [direction, setDirection] = useState(0);
  const [wrap, setWrap] = useState(0);

  const hookedStyles = {
    flexDirection: flexDirections[flexDirection],
    justifyContent: justifyContents[justifyContent],
    alignItems: alignItemsArr[alignItems],
    direction: directions[direction],
    flexWrap: wraps[wrap],
  };

  const changeSetting = (
    value: number,
    options: readonly unknown[],
    setterFunction: (index: number) => void,
  ) => {
    if (value === options.length - 1) {
      setterFunction(0);
      return;
    }
    setterFunction(value + 1);
  };
  const [squares, setSquares] = useState([<Square />, <Square />, <Square />]);
  return (
    <>
      <View style={{paddingTop: StatusBar.currentHeight}} />
      <View style={[styles.container, styles.playingSpace, hookedStyles]}>
        {squares.map(elem => elem)}
      </View>
      <ScrollView style={styles.container}>
        <View style={styles.controlSpace}>
          <View style={styles.buttonView}>
            <Button
              title="Change Flex Direction"
              onPress={() =>
                changeSetting(flexDirection, flexDirections, setFlexDirection)
              }
            />
            <Text style={styles.text}>{flexDirections[flexDirection]}</Text>
          </View>
          <View style={styles.buttonView}>
            <Button
              title="Change Justify Content"
              onPress={() =>
                changeSetting(
                  justifyContent,
                  justifyContents,
                  setJustifyContent,
                )
              }
            />
            <Text style={styles.text}>{justifyContents[justifyContent]}</Text>
          </View>
          <View style={styles.buttonView}>
            <Button
              title="Change Align Items"
              onPress={() =>
                changeSetting(alignItems, alignItemsArr, setAlignItems)
              }
            />
            <Text style={styles.text}>{alignItemsArr[alignItems]}</Text>
          </View>
          <View style={styles.buttonView}>
            <Button
              title="Change Direction"
              onPress={() => changeSetting(direction, directions, setDirection)}
            />
            <Text style={styles.text}>{directions[direction]}</Text>
          </View>
          <View style={styles.buttonView}>
            <Button
              title="Change Flex Wrap"
              onPress={() => changeSetting(wrap, wraps, setWrap)}
            />
            <Text style={styles.text}>{wraps[wrap]}</Text>
          </View>
          <View style={styles.buttonView}>
            <Button
              title="Add Square"
              onPress={() => setSquares([...squares, <Square />])}
            />
          </View>
          <View style={styles.buttonView}>
            <Button
              title="Delete Square"
              onPress={() =>
                setSquares(squares.filter((v, i) => i !== squares.length - 1))
              }
            />
          </View>
        </View>
      </ScrollView>
    </>
  );
};

const styles = StyleSheet.create({
  container: {
    height: '50%',
  },
  playingSpace: {
    backgroundColor: 'white',
    borderColor: 'blue',
    borderWidth: 3,
  },
  controlSpace: {
    flexDirection: 'row',
    flexWrap: 'wrap',
    backgroundColor: '#F5F5F5',
  },
  buttonView: {
    width: '50%',
    padding: 10,
  },
  text: {textAlign: 'center'},
});

const Square = () => (
  <View
    style={{
      width: 50,
      height: 50,
      backgroundColor: randomHexColor(),
    }}
  />
);

const randomHexColor = () => {
  return '#000000'.replace(/0/g, () => {
    return Math.round(Math.random() * 16).toString(16);
  });
};

export default App;
```

</TabItem>
</Tabs>

---

# 文档

## 属性

### `alignContent`

`alignContent` controls how rows align in the cross direction, overriding the `alignContent` of the parent. 访问 https://developer.mozilla.org/en-US/docs/Web/CSS/align-content 来进一步了解。

| 类型                                                                                 | 必需 |
| ------------------------------------------------------------------------------------ | ---- |
| enum('flex-start', 'flex-end', 'center', 'stretch', 'space-between', 'space-around') | 否   |

---

### `alignItems`

`alignItems` aligns children in the cross direction. For example, if children are flowing vertically, `alignItems` controls how they align horizontally. It works like `align-items` in CSS (default: stretch). See https://developer.mozilla.org/en-US/docs/Web/CSS/align-items for more details.

| Type                                                            | Required |
| --------------------------------------------------------------- | -------- |
| enum('flex-start', 'flex-end', 'center', 'stretch', 'baseline') | No       |

---

### `alignSelf`

`alignSelf` controls how a child aligns in the cross direction, overriding the `alignItems` of the parent. It works like `align-self` in CSS (default: auto). See https://developer.mozilla.org/en-US/docs/Web/CSS/align-self for more details.

| Type                                                                    | Required |
| ----------------------------------------------------------------------- | -------- |
| enum('auto', 'flex-start', 'flex-end', 'center', 'stretch', 'baseline') | No       |

---

### `aspectRatio`

Aspect ratio controls the size of the undefined dimension of a node. See https://developer.mozilla.org/en-US/docs/Web/CSS/aspect-ratio for more details.

- On a node with a set width/height, aspect ratio controls the size of the unset dimension
- On a node with a set flex basis, aspect ratio controls the size of the node in the cross axis if unset
- On a node with a measure function, aspect ratio works as though the measure function measures the flex basis
- On a node with flex grow/shrink, aspect ratio controls the size of the node in the cross axis if unset
- Aspect ratio takes min/max dimensions into account

| Type           | Required |
| -------------- | -------- |
| number, string | No       |

---

### `borderBottomWidth`

`borderBottomWidth` works like `border-bottom-width` in CSS. See https://developer.mozilla.org/en-US/docs/Web/CSS/border-bottom-width for more details.

| Type   | Required |
| ------ | -------- |
| number | No       |

---

### `borderEndWidth`

When direction is `ltr`, `borderEndWidth` is equivalent to `borderRightWidth`. When direction is `rtl`, `borderEndWidth` is equivalent to `borderLeftWidth`.

| Type   | Required |
| ------ | -------- |
| number | No       |

---

### `borderLeftWidth`

`borderLeftWidth` works like `border-left-width` in CSS. See https://developer.mozilla.org/en-US/docs/Web/CSS/border-left-width for more details.

| Type   | Required |
| ------ | -------- |
| number | No       |

---

### `borderRightWidth`

`borderRightWidth` works like `border-right-width` in CSS. See https://developer.mozilla.org/en-US/docs/Web/CSS/border-right-width for more details.

| Type   | Required |
| ------ | -------- |
| number | No       |

---

### `borderStartWidth`

When direction is `ltr`, `borderStartWidth` is equivalent to `borderLeftWidth`. When direction is `rtl`, `borderStartWidth` is equivalent to `borderRightWidth`.

| Type   | Required |
| ------ | -------- |
| number | No       |

---

### `borderTopWidth`

`borderTopWidth` works like `border-top-width` in CSS. See https://developer.mozilla.org/en-US/docs/Web/CSS/border-top-width for more details.

| Type   | Required |
| ------ | -------- |
| number | No       |

---

### `borderWidth`

`borderWidth` works like `border-width` in CSS. See https://developer.mozilla.org/en-US/docs/Web/CSS/border-width for more details.

| Type   | Required |
| ------ | -------- |
| number | No       |

---

### `bottom`

`bottom` is the number of logical pixels to offset the bottom edge of this component.

It works similarly to `bottom` in CSS, but in React Native you must use points or percentages. Ems and other units are not supported.

See https://developer.mozilla.org/en-US/docs/Web/CSS/bottom for more details of how `bottom` affects layout.

| Type           | Required |
| -------------- | -------- |
| number, string | No       |

---

### `columnGap`

`columnGap` works like `column-gap` in CSS. Only pixel units are supported in React Native. See https://developer.mozilla.org/en-US/docs/Web/CSS/column-gap for more details.

| Type   | Required |
| ------ | -------- |
| number | No       |

---

### `direction`

`direction`指定了用户界面的阅读顺序。`ltr`表示 left to right，即从左往右阅读。反之`rtl`为从右往左阅读。默认值为`inherit`，但根节点的值会根据用户所在地的不同而不同。访问 https://yogalayout.com/docs/layout-direction 来进一步了解。

| 类型                          | 必需 | 平台 |
| ----------------------------- | ---- | ---- |
| enum('inherit', 'ltr', 'rtl') | 否   | iOS  |

---

### `display`

`display`设置组件的显示类型。可用于元素的显示和隐藏。

它的表现和 CSS 上的`display`类似，但目前只支持'flex'和'none'两个值。默认值是'flex'。

| 类型                 | 必需 |
| -------------------- | ---- |
| enum('none', 'flex') | 否   |

---

### `end`

当`direction`设置为`ltr`时，`end`等同于`right`。当`direction`设置为`rtl`，`end`等同于`left`。

此样式的优先级高于`left`和`right`。

| 类型           | 必需 |
| -------------- | ---- |
| number, string | 否   |

---

### `flex`

在 React Native 中`flex`的表现和 CSS 有些区别。`flex`在 RN 中只能为整数值，其具体表现请参考`yoga`布局引擎的文档，其地址为 https://github.com/facebook/yoga

当`flex`为一个正整数时，组件尺寸会具有弹性，并根据具体的 flex 值来按比例分配。比如两个组件在同一个父容器中，一个`flex`为 2，另一个`flex`为 1，则两者的尺寸比为 2：1。 `flex: <positive number>` equates to `flexGrow: <positive number>, flexShrink: 1, flexBasis: 0`.

当`flex`为 0 时，组件尺寸由`width`和`height`决定，此时不再具有弹性。

当`flex`为-1 时，组件尺寸一般还是由`width`和`height`决定。但是当空间不够时，组件尺寸会收缩到`minWidth`和`minHeight`所设定的值。

`flexGrow`、`flexShrink`、`flexBasis`和在 CSS 上表现一致。

| 类型   | 必需 |
| ------ | ---- |
| number | 否   |

---

### `flexBasis`

`flexBasis` is an axis-independent way of providing the default size of an item along the main axis. Setting the `flexBasis` of a child is similar to setting the `width` of that child if its parent is a container with `flexDirection: row` or setting the `height` of a child if its parent is a container with `flexDirection: column`. The `flexBasis` of an item is the default size of that item, the size of the item before any `flexGrow` and `flexShrink` calculations are performed.

| 类型           | 必需 |
| -------------- | ---- |
| number, string | 否   |

---

### `flexDirection`

`flexDirection` controls which directions children of a container go. `row` goes left to right, `column` goes top to bottom, and you may be able to guess what the other two do. It works like `flex-direction` in CSS, except the default is `column`. 访问 https://developer.mozilla.org/en-US/docs/Web/CSS/flex-direction 来进一步了解。

| 类型                                                   | 必需 |
| ------------------------------------------------------ | ---- |
| enum('row', 'row-reverse', 'column', 'column-reverse') | 否   |

---

### `flexGrow`

`flexGrow` describes how any space within a container should be distributed among its children along the main axis. After laying out its children, a container will distribute any remaining space according to the flex grow values specified by its children.

`flexGrow` accepts any floating point value >= 0, with 0 being the default value. A container will distribute any remaining space among its children weighted by the children’s `flexGrow` values.

| 类型   | 必需 |
| ------ | ---- |
| number | 否   |

---

### `flexShrink`

[`flexShrink`](layout-props#flexshrink) describes how to shrink children along the main axis in the case in which the total size of the children overflows the size of the container on the main axis. `flexShrink` is very similar to `flexGrow` and can be thought of in the same way if any overflowing size is considered to be negative remaining space. These two properties also work well together by allowing children to grow and shrink as needed.

`flexShrink` accepts any floating point value >= 0, with 0 being the default value. A container will shrink its children weighted by the children’s `flexShrink` values.

| 类型   | 必需 |
| ------ | ---- |
| number | 否   |

---

### `flexWrap`

`flexWrap` controls whether children can wrap around after they hit the end of a flex container. It works like `flex-wrap` in CSS (default: nowrap). 访问 https://developer.mozilla.org/en-US/docs/Web/CSS/flex-wrap 来进一步了解。Note it does not work anymore with `alignItems: stretch` (the default), so you may want to use `alignItems: flex-start` for example (breaking change details: https://github.com/facebook/react-native/releases/tag/v0.28.0).

| 类型                                   | 必需 |
| -------------------------------------- | ---- |
| enum('wrap', 'nowrap', 'wrap-reverse') | 否   |

---

### `gap`

`gap` works like `gap` in CSS. Only pixel units are supported in React Native. See https://developer.mozilla.org/en-US/docs/Web/CSS/gap for more details.

| Type   | Required |
| ------ | -------- |
| number | No       |

---

### `height`

`height`用于设置组件的高度。

它的表现和 CSS 上的`height`类似， but in React Native 只能使用逻辑像素值（数字单位）或百分比，而不能使用 em 或是任何其他单位。 访问 https://developer.mozilla.org/en-US/docs/Web/CSS/height 来进一步了解。

| 类型           | 必需 |
| -------------- | ---- |
| number, string | 否   |

---

### `justifyContent`

`justifyContent` aligns children in the main direction. For example, if children are flowing vertically, `justifyContent` controls how they align vertically. It works like `justify-content` in CSS (default: flex-start). 访问 https://developer.mozilla.org/en-US/docs/Web/CSS/justify-content 来进一步了解。

| 类型                                                                                      | 必需 |
| ----------------------------------------------------------------------------------------- | ---- |
| enum('flex-start', 'flex-end', 'center', 'space-between', 'space-around', 'space-evenly') | 否   |

---

### `left`

`left`值是指将本组件定位到距离左边多少个逻辑像素（左边的定义取决于`position`属性）。

它的表现和 CSS 上的`left`类似， but in React Native 只能使用逻辑像素值（数字单位）或百分比，而不能使用 em 或是任何其他单位。

访问 https://developer.mozilla.org/en-US/docs/Web/CSS/left for more details of how `left` affects layout.

| 类型           | 必需 |
| -------------- | ---- |
| number, string | 否   |

---

### `margin`

设置`margin`相同于同时设置`marginTop`、`marginLeft`、`marginBottom`以及`marginRight`。访问 https://developer.mozilla.org/en-US/docs/Web/CSS/margin 来进一步了解。

| 类型           | 必需 |
| -------------- | ---- |
| number, string | 否   |

---

### `marginBottom`

`marginBottom`和 CSS 上的`margin-bottom`表现一致。访问 https://developer.mozilla.org/en-US/docs/Web/CSS/margin-bottom 来进一步了解。

| 类型           | 必需 |
| -------------- | ---- |
| number, string | 否   |

---

### `marginEnd`

When direction is `ltr`, `marginEnd` is equivalent to `marginRight`. When direction is `rtl`, `marginEnd` is equivalent to `marginLeft`.

| 类型           | 必需 |
| -------------- | ---- |
| number, string | 否   |

---

### `marginHorizontal`

设置`marginHorizontal`相同于同时设置`marginLeft`和`marginRight`。

| 类型           | 必需 |
| -------------- | ---- |
| number, string | 否   |

---

### `marginLeft`

`marginLeft`和 CSS 上的`margin-left`表现一致。访问 https://developer.mozilla.org/en-US/docs/Web/CSS/margin-left 来进一步了解。

| 类型           | 必需 |
| -------------- | ---- |
| number, string | 否   |

---

### `marginRight`

`marginRight`和 CSS 上的`margin-right`表现一致。访问 https://developer.mozilla.org/en-US/docs/Web/CSS/margin-right 来进一步了解。

| 类型           | 必需 |
| -------------- | ---- |
| number, string | 否   |

---

### `marginStart`

When direction is `ltr`, `marginStart` is equivalent to `marginLeft`. When direction is `rtl`, `marginStart` is equivalent to `marginRight`.

| 类型           | 必需 |
| -------------- | ---- |
| number, string | 否   |

---

### `marginTop`

`marginTop`和 CSS 上的`margin-top`表现一致。访问 https://developer.mozilla.org/en-US/docs/Web/CSS/margin-top 来进一步了解。

| 类型           | 必需 |
| -------------- | ---- |
| number, string | 否   |

---

### `marginVertical`

设置`marginVertical`相同于同时设置`marginTop`和`marginBottom`。

| 类型           | 必需 |
| -------------- | ---- |
| number, string | 否   |

---

### `maxHeight`

`maxHeight` is the maximum height for this component, in logical pixels.

它的表现和 CSS 上的`max-height`类似，但是在 React Native 上只能使用逻辑像素值（数字单位）或百分比，而不能使用 em 或是任何其他单位。

访问 https://developer.mozilla.org/en-US/docs/Web/CSS/max-height 来进一步了解。

| 类型           | 必需 |
| -------------- | ---- |
| number, string | 否   |

---

### `maxWidth`

`maxWidth` is the maximum width for this component, in logical pixels.

它的表现和 CSS 上的`max-width`类似，但是在 React Native 上只能使用逻辑像素值（数字单位）或百分比，而不能使用 em 或是任何其他单位。

访问 https://developer.mozilla.org/en-US/docs/Web/CSS/max-width 来进一步了解。

| 类型           | 必需 |
| -------------- | ---- |
| number, string | 否   |

---

### `minHeight`

`minHeight` is the minimum height for this component, in logical pixels.

它的表现和 CSS 上的`min-height`类似，但是在 React Native 上只能使用逻辑像素值（数字单位）或百分比，而不能使用 em 或是任何其他单位。

访问 https://developer.mozilla.org/en-US/docs/Web/CSS/min-height 来进一步了解。

| 类型           | 必需 |
| -------------- | ---- |
| number, string | 否   |

---

### `minWidth`

`minWidth` is the minimum width for this component, in logical pixels.

它的表现和 CSS 上的`min-width`类似，但是在 React Native 上只能使用逻辑像素值（数字单位）或百分比，而不能使用 em 或是任何其他单位。

访问 https://developer.mozilla.org/en-US/docs/Web/CSS/min-width 来进一步了解。

| 类型           | 必需 |
| -------------- | ---- |
| number, string | 否   |

---

### `overflow`

`overflow` controls how children are measured and displayed. `overflow: hidden` causes views to be clipped while `overflow: scroll` causes views to be measured independently of their parents main axis. It works like `overflow` in CSS (default: visible). 访问 https://developer.mozilla.org/en/docs/Web/CSS/overflow 来进一步了解。

| 类型                                | 必需 |
| ----------------------------------- | ---- |
| enum('visible', 'hidden', 'scroll') | 否   |

---

### `padding`

设置`padding`相同于同时设置`paddingTop`、`paddingBottom`、`paddingLeft`以及`paddingRight`。访问 https://developer.mozilla.org/en-US/docs/Web/CSS/padding 来进一步了解。

| 类型           | 必需 |
| -------------- | ---- |
| number, string | 否   |

---

### `paddingBottom`

`paddingBottom`和 CSS 上的`padding-bottom`表现一致。访问 https://developer.mozilla.org/en-US/docs/Web/CSS/padding-bottom 来进一步了解。

| 类型           | 必需 |
| -------------- | ---- |
| number, string | 否   |

---

### `paddingEnd`

When direction is `ltr`, `paddingEnd` is equivalent to `paddingRight`. When direction is `rtl`, `paddingEnd` is equivalent to `paddingLeft`.

| 类型           | 必需 |
| -------------- | ---- |
| number, string | 否   |

---

### `paddingHorizontal`

设置`paddingHorizontal`相同于同时设置`paddingLeft`和`paddingRight`。

| 类型           | 必需 |
| -------------- | ---- |
| number, string | 否   |

---

### `paddingLeft`

`paddingLeft`和 CSS 上的`padding-left`表现一致。访问 https://developer.mozilla.org/en-US/docs/Web/CSS/padding-left 来进一步了解。

| 类型           | 必需 |
| -------------- | ---- |
| number, string | 否   |

---

### `paddingRight`

`paddingRight`和 CSS 上的`padding-right`表现一致。访问 https://developer.mozilla.org/en-US/docs/Web/CSS/padding-right 来进一步了解。

| 类型           | 必需 |
| -------------- | ---- |
| number, string | 否   |

---

### `paddingStart`

When direction is `ltr`, `paddingStart` is equivalent to `paddingLeft`. When direction is `rtl`, `paddingStart` is equivalent to `paddingRight`.

| 类型           | 必需 |
| -------------- | ---- |
| number, string | 否   |

---

### `paddingTop`

`paddingTop`和 CSS 上的`padding-top`表现一致。访问 https://developer.mozilla.org/en-US/docs/Web/CSS/padding-top 来进一步了解。

| 类型           | 必需 |
| -------------- | ---- |
| number, string | 否   |

---

### `paddingVertical`

设置`paddingVertical`相同于同时设置`paddingTop`和`paddingBottom`。

| 类型           | 必需 |
| -------------- | ---- |
| number, string | 否   |

---

### `position`

`position` in React Native is similar to regular CSS, but everything is set to `relative` by default, so `absolute` positioning is always relative to the parent.

If you want to position a child using specific numbers of logical pixels relative to its parent, set the child to have `absolute` position.

If you want to position a child relative to something that is not its parent, don't use styles for that. Use the component tree.

See https://github.com/facebook/yoga for more details on how `position` differs between React Native and CSS.

| 类型                         | 必需 |
| ---------------------------- | ---- |
| enum('absolute', 'relative') | 否   |

---

### `right`

`right`值是指将本组件定位到距离右边多少个逻辑像素（右边的定义取决于`position`属性）。

它的表现和 CSS 上的`right`类似，但是在 React Native 上只能使用逻辑像素值（数字单位）或百分比，而不能使用 em 或是任何其他单位。

访问 https://developer.mozilla.org/en-US/docs/Web/CSS/right for more details of how `right` affects layout.

| 类型           | 必需 |
| -------------- | ---- |
| number, string | 否   |

---

### `rowGap`

`rowGap` works like `row-gap` in CSS. Only pixel units are supported in React Native. See https://developer.mozilla.org/en-US/docs/Web/CSS/row-gap for more details.

| Type   | Required |
| ------ | -------- |
| number | No       |

---

### `start`

当`direction`设置为`ltr`时，`start`等同于`left`。当`direction`设置为`rtl`，`start`等同于`right`。

此样式的优先级高于`left`、`right`和`end`。

| 类型           | 必需 |
| -------------- | ---- |
| number, string | 否   |

---

### `top`

`top`值是指将本组件定位到距离顶部多少个逻辑像素（顶部的定义取决于`position`属性）。

它的表现和 CSS 上的`top`类似，但是在 React Native 上只能使用逻辑像素值（数字单位）或百分比，而不能使用 em 或是任何其他单位。

访问 https://developer.mozilla.org/en-US/docs/Web/CSS/top for more details of how `top` affects layout.

| 类型           | 必需 |
| -------------- | ---- |
| number, string | 否   |

---

### `width`

`width`设置组件的宽度。

它的表现和 CSS 上的`width`类似，但是在 React Native 上只能使用逻辑像素值（数字单位）或百分比，而不能使用 em 或是任何其他单位。 访问 https://developer.mozilla.org/en-US/docs/Web/CSS/width 来进一步了解。

| 类型           | 必需 |
| -------------- | ---- |
| number, string | 否   |

---

### `zIndex`

`zIndex`控制着组件的堆叠覆盖顺序。多数情况下你不会用到此样式。默认情况下组件按其在文档树的顺序依次渲染，所以在代码结构上靠后的组件会覆盖前面的组件（如果它们在布局上有重叠的部分）。有时候在写一些动画或者自定义的模态窗口时，你可能会需要设置`zIndex`样式来改变层叠覆盖顺序。

它的表现和 CSS 上的`z-index`一致——`zIndex`大的在上面。这里面的`z`意味着三维空间中的`z轴`，你可以想象成垂直于手机屏幕指向你的眼睛的坐标轴。访问 https://developer.mozilla.org/en-US/docs/Web/CSS/z-index 来进一步了解。

在 iOS 上，使用`zIndex`可能需要`View`彼此为兄弟节点才能生效。

| 类型   | 必需 |
| ------ | ---- |
| number | 否   |

---
