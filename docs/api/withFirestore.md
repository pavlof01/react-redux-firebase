<!-- Generated by documentation.js. Update this documentation by updating the source code. -->

### Table of Contents

-   [createWithFirestore](#createwithfirestore)
-   [withFirestore](#withfirestore)

## createWithFirestore

Function that creates a Higher Order Component that
which provides `firebase`, `firestore`, and `dispatch` to React Components.

**WARNING!!** This is an advanced feature, and should only be used when
needing to access a firebase instance created under a different store key.

**Parameters**

-   `storeKey` **[String](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)** Name of redux store which contains
    Firebase state (`state.firebase`) (optional, default `'store'`)

**Examples**

_Basic_

```javascript
import { createWithFirestore } from 'react-redux-firebase'

// create withFirestore that uses another redux store
const withFirestore = createWithFirestore('anotherStore')

// use the withFirestore to wrap a component
export default withFirestore(SomeComponent)
```

Returns **[Function](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Statements/function)** Higher Order Component which accepts an array of
watchers config and wraps a React Component

## withFirestore

**Extends React.Component**

Higher Order Component that attaches `firestore`, `firebase`
and `dispatch` as props to React Components. Firebase instance is gathered
from `store.firestore`, which is attached to store by the store enhancer
(`reduxFirestore`) during setup of
[`redux-firestore`](https://github.com/prescottprue/redux-firestore)

**Examples**

_Basic_

```javascript
import { withFirestore } from 'react-redux-firebase'

const AddTodo = ({ firestore: { add } }) =>
  <div>
    <button onClick={() => add('todos', { done: false, text: 'Sample' })}>
      Add Sample Todo
    </button>
  </div>

export default withFirestore(AddTodo)
```

_Within HOC Composition_

```javascript
import { compose } from 'redux' // can also come from recompose
import { withHandlers } from 'recompose'
import { withFirestore } from 'react-redux-firebase'

const AddTodo = ({ addTodo }) =>
  <div>
    <button onClick={addTodo}>
      Add Sample Todo
    </button>
  </div>

export default compose(
  withFirestore(AddTodo),
  withHandlers({
    addTodo: props => () =>
       props.firestore.add(
         { collection: 'todos' },
         { done: false, text: 'Sample' }
       )
  })
)
```

Returns **[Function](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Statements/function)** Which accepts a component to wrap and returns the
wrapped component