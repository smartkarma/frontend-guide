# Introduction

Here we will describe how to write Components.

## Component vs PureComponent vs Stateless Functional

Basically the best is to use always Functional Component. But a lot of times we need to have state for component.
In that case preferred is **PureComponent**, its much faster and control `shouldComponentUpdate` by default. It's
checking previous state/props and new ones. If there is no change it will not trigger re-render.
For normal **Component** whenever we pass new props or change state, but the values are same it will get
re-rendered. So we need to write our own condition to compare objects of state/props.

* **PureComponent** - preferred/fastest - `compare state and re-render only when state is different`
* **Stateless** Functional Component - if no state needed
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


## Refs
> Avoid using refs for anything that can be done declaratively.
For example, instead of exposing `open()` and `close()` methods on a Dialog component, pass an `isOpen` prop to it.
