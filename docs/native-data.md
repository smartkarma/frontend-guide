# Data
Actions, Epics, Reducers and Selectors are inside `sk-redux` folder.

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

