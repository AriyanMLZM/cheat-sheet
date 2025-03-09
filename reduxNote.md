`npm i @reduxjs/toolkit react-redux`

## Setup Store

`src/store/store.js`

```
import { configureStore } from "@reduxjs/toolkit";
import sliceReducer from './slices/counterSlice';

export const store = configureStore({
  reducer: {
    counter: sliceReducer,
  }
})
```

set the reducer the slices reducers that we create for each feature.

## Setup Provider

```
import { Provider } from 'react-redux';
import { store } from './store/store.js';

<Provider store={store}>
  <App />
</Provider>
```

wrap the app with provider of redux.

## Setup Slice

`./slices/sliceName.js`

```
import { createSlice } from "@reduxjs/toolkit";

const initialState = {
  prop: 0
}

export const nameSlice = createSlice({
  name: 'sliceName',
  initialState,
  reducers: {
    actionName: (state) => {
      state.prop += 1;
    },
    actionName2: (state) => {
      state.prop -= 1;
    },
    actionName3: (state, action) => {
      state.prop += action.payload;
    }
  }
});

export const { actionName, actionName2, actionName3 } = nameSlice.actions;

export default nameSlice.reducer;
```

declare the reducer actions.  
export the actions.  
export the reducer that will be used in store.js.

```
reducers: {
  actionName: {
    reducer(state, action) {
      state.push(action.payload)
    },
    prepare(prop1, prop2, prop3) {
      return {
        payload: {
          prop1,
          prop2,
          prop3
        }
      }
    }
  },
}
```

we can customize the payload with prepare and send it to the reducer.

## Usage

`import { useDispatch, useSelector } from 'react-redux`

`const count = useSelector((state: RootStateType) => state.sliceNam.prop)`  
we use the selector to access the states value.

`import { actionName } from './slices/sliceName.js'`  
`useDispatch(actionName())`  
we use the dispatch to run a slice action.

## Setup Async Thunk

```
export const fetchPosts = createAsyncThunk('sliceName/thunkName', async () => {
  const response = await axios.get(URL)
  return response.data
})
```

we use the thunk for implementing async operations like fetching data.

```
createSlice({
  extraReducers(builder) {
    builder
      .addCase(thunkName.pending, (state, action) => {
        state.status = 'loading'
      })
  }
})
```

we use the thunk in slice config.
we can declare a status prop.
cases of async thunk function:

- pending
- fulfilled
- rejected

## Entity Adapter

we use this to make working with data based state more easy and optimized way and create auto selectors.

`import { createEntityAdapter } from '@reduxjs/toolkit'`

```
const dataAdapter = createEntityAdapter({
  sortComparer: (a, b) => b.date.localeCompare(a.date)
})
```

we can declare the adaptor with a sorter to sort the data automatically.

```
const initialState = dataAdapter.getInitialState({
  prop1: 1,
  prop2: 2
})
```

set the initial state with adaptor and use it in slice.

### Adaptor Methods

`dataAdapter.upsertMany(state, datas)`  
add multi records of data.

`dataAdapter.addOne(state, data)`  
add one record of data.

`dataAdapter.upsertOne(state, updatedData)`  
update one record automatically.

`dataAdapter.removeOne(state, id)`  
remove one record with id.

### Auto Generated Selectors

```
export const {
  selectAll,
  selectById,
  selectIds
} = dataAdapter.getSelectors(state => state.sliceName)
```

## Types

`export type RootStore = ReturnType<typeof store.getSate>`  
get the type of root state of store.

`export type AppDispatch = typeof store.dispatch`  
get the dispatch type of store.  
`useDispatch<AppDispatch>()`  
use the AppDispatch type.
