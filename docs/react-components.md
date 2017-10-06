# Introduction

Here we will describe how to write Components.

## Component, Pure or Stateless Functional ?

Basically the best is to always start with **Stateless Functional Component**. But a lot of times we need to have state for our component.
In that case we should use **Pure Component**, it's much faster and control `shouldComponentUpdate` on its own.
Which prevents unnecessary re-rendering of the component whenever props/state changes with same values.
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
Another important aspect of your components are property types (aka PropTypes). Every component had to have
properly implemented propTypes. It makes using component much easier and making less prone to error.
Basic syntax of propTypes look like this:

```js
//... import
import { number, string } from 'prop-types'; // always deconstruct

//... inside your PureComponent/Component
static propTypes = {
  itemId: number.isRequired,
  label: string,
};
// for functional we add propTypes into the object/component.
// As you can see in the functional component example
```

?> Don't forget to specify `isRequired` properties, which brakes component if not supplied.

!> Beware of using `any, node`, since they are too generic. And making propTypes useless.

## Refs
> Avoid using refs for anything that can be done declaratively.
For example, instead of exposing `open()` and `close()` methods on a Dialog component, pass an `isOpen` prop to it.
