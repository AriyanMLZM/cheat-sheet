`npm i react-query`

## Setup Provider

`import { QueryClient, QueryClientProvider } from 'react-query'`

`import { ReactQueryDevtools } from 'react-query/devtools'`

`const queryClient = new QueryClient()`  
declare a queryClient.

```
<QueryClientProvider client={queryClient}>
  <App />
  <ReactQueryDevtools initialIsOpen />
</QueryClientProvider>
```

wrap the app in react query provider.  
we can use ReactQueryDevtools. it is only shown in dev mode.

## Use Query Client

`import { useQuery, useMutation, useQueryClient } from "react-query"`  
we use each hook for cruds implementation.

`const queryClient = useQueryClient()`  
get the query client.

### useQuery

```
const {
  isLoading,
  isError,
  error,
  data
} = useQuery('tagNameCache', getDataFunc, {
    select: data => data.sort((a, b) => b.id - a.id)
})
```

used for get based query.  
data will be cached by tagName.  
we can also use axios function for getting data.
select allow us to transform data when needed like sorting it.

### useMutation

```
const addDataMutation = useMutation(addDataFunc, {
  onSuccess: () => {
    queryClient.invalidateQueries("tagNameCache")
  }
})

addDataMutation.mutate(data)
```

used for update, delete and add methods.  
invalidateQueries will invalidate the cached of tagName and make refetching data possible.
