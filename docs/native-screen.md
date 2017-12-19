# Screen

Put your component here and fetch for data. It's that simple!

?> All screens are inside `screens` folder.

## Add new Screen

1. Create new folder with name of the screen
2. Create `index.js`
3. Add React `Component` code and give name to screen: `ExampleScreen`
4. Import screen in `navigation/RootStackNavigation.js`:
```js
import ExampleScreen from 'screens/example';
```
5. Add screen to `StackNavigator` object:
```js
//...end of StackNavigator
  Example: { screen: ExampleScreen },
},
```

!> If you are using Hot Reload, you need to reload the app.

## Define navigation top bar
By default screen will render this topbar (Launch icon, search bar and private messages icon).

![DefaultBar](https://d26dzxoao6i3hh.cloudfront.net/items/3B1A470Y2s39453T1w0l/Image%202017-10-06%20at%2011.02.34%20AM.public.20153B402N03.png)

Defined in: `navigation/RootStackNavigator.js`

#### Nested screens
For nested screens we use combination
of Title and Back button. You can customize how top bar will look like, by overriding the  `navigationOptions`
inside screen component.
```js
import NavigationBar from 'components/NavigationBar';
import HeaderBackButton from 'components/HeaderBackButton';
// ...screen component
static navigationOptions = ({ navigation }) => {
  header: (
    <NavigationBar
      title={navigation.state.params.navigationTitle}
      left={<HeaderBackButton goBack={navigation.goBack} />}
      // `right` prop is also available, look inside <NavigationBar> for more info.
    />
  )
}
```

## Navigate to Screen
There are two different ways to use navigation. Easiest way is inside screen component.

### Screen component
Navigation is achieved with `navigation` property.

```js
// skipped All imports...

export default class ExampleScreen extends PureComponent {
  static propTypes = {
    navigation: object,
  }

  onPress = () => {
    const { data, navigation } = this.props;
    navigation.navigate('ExampleScreen', {
      navigationTitle: 'Welcome to ExampleScreen',
      data, // custom params, stored in: navigation.state.params
    });
  }

  render(<Text onPress={this.onPress}>Go to ExampleScreen</Text>)
}
```

### Components
In normal component, we don't have available `navigation`. There are two ways to perform navigation.
 1. - use HOC `@withNavigation` (recommended)
 2. - dispatch redux action `NAVIGATE`
 
 
#### withNavigation

Use as decorator or wrap componet in separate export.

```js
import { withNavigation } from 'react-navigation';

@withNavigation
export default class MyComponent extends React.PureComponent {
  this.props.navigation.navigate(
    'ExampleScreen', 
    {
      myParam: 'hello',
    },
   );
}

```


#### dispatch action

Alternative way to navigate. The only disadvantage is that syntax is different and might be consufins when using `withNavigation` and dispatch action `NAVIGATE`.

```js
import { NAVIGATE } from 'constants/action-types';

//... inside component
static propTypes = {
  dispatch: func,
}

onPress = () => {
  this.props.dispatch({
    type: NAVIGATE,
    routeName: 'ExampleScreen',
    // accessed via: navigation.state.params
    params: {
      myParam: 'hello',
    },
  });
}
```
