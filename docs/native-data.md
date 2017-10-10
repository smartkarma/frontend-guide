# Data
Data are stored locally in component state or globally in Redux store.

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
