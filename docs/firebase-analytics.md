# Firebase analytics

Purpose of this page is to describe conventions of analytics, which are collected through Firebase Analytics.

## Log Events

Each event has to be defined via `Flow` in `logEvent` utility.

The param have this shape:

```js
type EventParams = {|
  event: "name_of_event",
  params: {|
    id: string,
    step: Step,
    origin?: Origin
  |}
|};
```

> Don't forget to always put origin in Origin type, to prevent duplicates and keep track of all of
> them from one place.

### Debug View

By default debug view should be enabled. Just go to `Firebase Console > Debug View`

#### Enable Debug View for Firebase in XCode

1.  Open Xcode
2.  Click on `SKNativeAppDev`
3.  Scroll down -> Click on `Edit Scheme…`
4.  Go to `Run`
5.  Switch to `Arguments`
6.  Inside: `Arguments Passed on Launch` add this:
    1.  `-FIRDebugEnabled`
7.  Run the build on real device, thats it 🙌
