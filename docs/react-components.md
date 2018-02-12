# Introduction

Here we will describe how to write Components.

## Component, Pure or Stateless Functional ?

Basically the best is to always start with **Stateless Functional Component**. But a lot of times we need state for our component.
In that case we should use **Pure Component**, it's much faster and control `shouldComponentUpdate` on its own.
It prevents unnecessary re-rendering of the component whenever props/state changes with same values.
Your last option should be normal  **Component**.

* **Pure Component** - preferred
* **Stateless Functional Component** - if no state needed
* **Component** - slowest

```js
/* StatelessFunctionalComponent/index.js */
import React from 'react';
import { Text } from 'react-native';
import { string } from 'prop-types';

const StatelessComponent = ({ nameOfProperty }) => (
  <Text>{nameOfProperty}</Text>
);

StatelessComponent.propTypes = {
  nameOfProperty: string.isRequired,
};

StatelessComponent.defaultProps = {
  nameOfProperty: 'Hello World',
};

export default StatelessComponent;

}
```

## Prop Types
`prop-types` were deprecated in favour of **Flow**.
---
More examples and guide can be found on official [documentation for Flow](https://flow.org/en/docs/). Especially useful is part focused on [React Components](https://flow.org/en/docs/react/components/).

Example of `Props` written with Flow.


```js
type Props = {
  position: Animated.Value,
  jumpToIndex: (index: number) => mixed,
  getLabel: (scene: *) => string,
  renderIcon: (scene: *) => React.Element<any>,
  inactiveTintColor: string,
  tabStyle?: Style,
};

type State = {
  isPostOpen: boolean,
  animate: Animated.Value,
};

export default class TabBar extends React.Component<Props, State> {
// rest of component code...
```

?> If there is few props, we can use shorthand: `Component<{ inactiveTintColor: string }>`

## Refs
> Avoid using refs for anything that can be done declaratively.
For example, instead of exposing `open()` and `close()` methods on a Dialog component, pass an `isOpen` prop to it.

## Props
Properties of component.
Whenever we can, we should combine related properties to object. Otherwise we endup with huge ammount of props in root level.
Good example is this:
```js
type Props = {
  addLabel: string,
  addOnPress: Function,
  addIcon: string,
  label: string,
  onPress: Function,
}
```
we can rewrite related props like this:
```js
type Props = {
  add: {
    label: string,
    onPress: Function,
    icon: string,
  },
  label: string,
  onPress: Function,
}
```

## Exporting
For components which we test and we apply HOC to them, we should use this way of exporting:
```js
class FollowButtonComponent extends React.PureComponent {}

export { FollowButtonComponent as PureFollowButton };
const FollowButton = connect((state, props) => ({
  canFollow: canFollowSelector(state, props),
}))(FollowButtonComponent);
export default FollowButton;
```


