# React Query

[공식문서](https://react-query.tanstack.com/quick-start)

- React application에서 서버 상태의 fetching, caching, synchronizing and updating을 도와주는 라이브러리

```
import {
  useQuery,
  useMutation,
  useQueryClient,
  QueryClient,
  QueryClientProvider,
} from 'react-query'
import { getTodos, postTodo } from '../my-api'

// Create a client
const queryClient = new QueryClient()

function App() {
  return (
    // Provide the client to your App
    <QueryClientProvider client={queryClient}>
      <Todos />
    </QueryClientProvider>
  )
}
```

- `fetcher`함수에 `argument`가 필요한 경우 익명함수를 만들어 `fetcher`함수를 리턴함
- `key`는 캐시 시스템에 저장되고 작동하기 위해 고유한 값이어야 함

```
function Todos() {
  // Access the client
  const queryClient = useQueryClient()

  // Queries
  const query = useQuery('todos', getTodos)
  // TypeScript and argument
  const { isLoading, data } = useQuery<Interface>('todos', () => getTodos(argument))

  // Mutations
  const mutation = useMutation(postTodo, {
    onSuccess: () => {
      // Invalidate and refetch
      queryClient.invalidateQueries('todos')
    },
  })

  return (
    <div>
      <ul>
        {query.data.map(todo => (
          <li key={todo.id}>{todo.title}</li>
        ))}
      </ul>

      <button
        onClick={() => {
          mutation.mutate({
            id: Date.now(),
            title: 'Do Laundry',
          })
        }}
      >
        Add Todo
      </button>
    </div>
  )
}

render(<App />, document.getElementById('root'))
```

## React Query Devtools

[공식문서](https://react-query.tanstack.com/devtools)

- React Query의 모든 내부 작동을 시각화 하여 보여줌
- 캐시에 어떤 query가 있는지와 Data Explorer 제공

### Import the Devtools

```
import { ReactQueryDevtools } from "react-query/devtools";
```

### Floating Mode

```
function App() {
  return (
    <QueryClientProvider client={queryClient}>
      // The rest of your application
      <ReactQueryDevtools initialIsOpen={false} />
    </QueryClientProvider>
  )
}
```
