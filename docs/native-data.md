# Data
Most of the data are stored in Redux. Logic is placed inside `sk-redux` folder.

# Redux (Action, Epic, Reducer, Selector)
For storing data we use redux action, which get observed by Epic (`redux-observer`) function.
State is finally update with reducer.
For accessing the data we use `redux-reselect`.

## Create an Action
Actions are always nested inside `modules` folder.
Basic action looks like this:
```js
export const fetchDiscussions = (type: string, id: string, options: OptionType) => ({
  type: 'Discussion/FETCH_DISCUSSIONS',
  payload: {
    id,
    type,
    options,
  },
});
```
This action has to be imported in `actions.js`.

## Create an Epic
Epics actually do the heavy lifting job. Most of the logic is stored there.
Example of epic:
```js
export const fetchDiscussionsEpic = (action$: ActionType) =>
  action$.ofType('Discussion/FETCH_DISCUSSIONS').flatMap(action =>
    Observable.fromPromise(ApiController.api.findAll('comments', action.payload.options))
      .flatMap(response =>
        Observable.concat(
          Observable.of({
            // all data from API has to be normalised first
            type: 'Data/NORMALISE_RESPONSE',
            payload: action.payload,
            response,
          }),
          Observable.of({
            type: 'Discussion/FETCH_DISCUSSIONS_SUCCESS',
            payload: action.payload,
            response,
          })
        )
      )
      .takeUntil(action$.ofType('Navigation/BACK'))
      .catch(() =>
        Observable.of(
          showToast({
            message: 'Something went wrong, please try again.',
            messageType: 'error',
          })
        )
      )
  );
```
This epic has to be imported in `epics.js`. After importing all epics are added to `epics=[]`.

## Create Reducer
In reducer we only update the redux store.
Example:
```js
// just one case from switch
case 'Discussion/FETCH_DISCUSSIONS': {
  const key = `${action.payload.type}-${action.payload.id}`;
  const discussionState = state[key] || DEFAULT_DISCCUSSION_STATE;

  return {
    ...state,
    [key]: {
      ...discussionState,
      isLoading: true,
    },
  };
}
```

## Create a Selector
Example:
```js
export const commentSelector = (state: StoreState, props: { id: string }) =>
  selectors.comments(state.data, props.id);
```

----

!> **DEPRECATED**: All things below were deprecated, in favour of new way of storing data

# JSON API
Data are fetched from our JSON API backend. There is one exception and that is **Datacloud**, which
response with normal JSON.

# Models
Please read Devour docs first: [Devour](https://github.com/twg/devour)

All models are defined inside `models` folder. Structure is based on Devour library + custom computed
functions.


## How to fetch data
Please read Devour docs first: [Devour](https://github.com/twg/devour)

```js
// fetch one Insight
this.props.jsonAPI
      .one('insight', insight.id)
      .all('comment-thread')
      .get({
        include:
          'commenter,commentable,commentable-entities,attachment,children,children.commenter,children.attachment',
      })
      .then(({ data }) => {
        this.setState({
          comments: data,
          isLoading: false,
        });
      })
      .catch(() => {
        this.setState({
          isLoading: false,
          hasError: true,
        });
      });
```
