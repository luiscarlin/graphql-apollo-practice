# graphql-apollo-practice

# Notes

## Apollo Client

### Cache

- After you do a fetch, apollo will break apart the response and normalize data
- Once the data is broken apart and normalized, it will update it when the same object is returned through any other query
- To normalize, it assigns a unique id to each fetched object. You can specfy how to build that. Idelly, you want to return `id` from the backend because that's the default. By default, it will look for `id`
  ```js
  const cache = new InMemoryCache({
    typePolicies: {
      Todo: {
        // The unique identifier for a todo was actually listed
        // as "todoId", so let's use this instead.
        keyFields: ["todoId"],
      },
    },
  });
  ```
- All the data is flattened in the cache
- Apollo Client stores the query (including vars) + result both queries and mutations
- Use `cache.extract()` to take a snapshot of the cache and `cache.restore(snapshot)` to restore
- On a query, Apollo Client goes to the cache. If query and result are there, then it returns that data. If query is asking for more fields, it will do the network call.
- "fetch policies" dicatate how the cache works
- Make sure mutations return the updated data. It will get updated by default in the cache.

https://www.apollographql.com/blog/demystifying-cache-normalization/
