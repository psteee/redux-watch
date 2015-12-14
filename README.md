redux-watch
===========

Watch/observe [Redux](http://redux.js.org/) store state changes.


Why?
----

Redux provides you with a `subscribe()` method so that you can be notified when
the state changes. However, it does not let you know what changed. `redux-watch`
will let you know what changed.


Install
-------

    npm i --save redux-watch



Usage
-----

### watch()

**Signature:**  `watch(getState, [objectPath], [comparison])`

**Parameters:**

- `getState`: A `function` that is used to return the state. Also useful in conjunction
with selectors.
- `objectPath`: An **optional** `string` or `Array` that represents the path in an object. Fully compatible with
[npm/object-path](https://www.npmjs.com/package/object-path).
- `comparison`: An **optional** function to pass for comparison of the fields. Defaults to strict
equal comparison (`===`). Could use [npm/deep-equal](https://www.npmjs.com/package/deep-equal).

**Returns:** A `function` that can be used to watch for the changes.

**Example (basic):**

```js
// ... other imports requires
// ...
import watch from 'redux-watch'

// store is THE redux store
// assuming you have an admin reducer
let w = watch(store.getState, 'admin.name')
store.subscribe(w(function(newVal, oldVal) {
  console.log(newval)
  console.log(oldVal)
}))
```

**Example (w/ [reselect](https://github.com/rackt/reselect) selectors):**

When using with selectors, you often times won't need to pass the object path.
Most times the selectors will handle this for you.

```js
// ... other imports requires
// ...
import watch from 'redux-watch'

// assuming mySelector is a reselect selector defined somewhere
let w = watch(() => mySelector(store.getState()))
store.subscribe(w(function(newVal, oldVal) {
  console.log(newval)
  console.log(oldVal)
}))
```


License
-------

MIT

Copyright (c) [JP Richardson](https://github.com/jprichardson)