import Callout from 'nextra-theme-docs/callout'

# File

## import_file "$url"

```sh
#!/usr/bin/env import

ruby "$(import_file https://import.sh/importpw/import/test/static/sum.rb)" 9 10 11 12
# 42
```

Uses the same download and caching infrastructure as import, but prints the local file path instead of sourcing the file. This enables working with arbitrary files such as scripts from other languages, simple data files, binary files, etc.


## import_file "$url"

```sh
#!/usr/bin/env import
import "https://import.sh/string@0.2.0"

echo InPuT | string_upper
# INPUT
```
The core import function downloads the $url parameter and caches it to the file system. Finally, it sources the downloaded script.


All SWR hooks inside `<Page/>` will read and write from that Map instance. You can also use other cache provider implementations as well for your specific use case.

<Callout>
  In the example above, when the `<App/>` component is re-mounted, the provider will also be re-created. Cache providers should be put higher in the component tree, or outside of render.
</Callout>

import { Cache } from 'components/diagrams/cache'

<div className="my-8">
  <Cache/>
</div>

When nested, SWR hooks will use the upper-level cache provider. If there is no upper-level cache provider, it fallbacks to the default cache provider, which is an empty `Map`.

<Callout emoji="⚠️">
   If a cache provider is used, the global `mutate` will **not** work for SWR hooks under that `<SWRConfig>` boundary. Please use [this](#access-current-cache-provider) instead. 
</Callout>

## Access Current Cache Provider

When inside a React component, you need to use the [`useSWRConfig`](/docs/global-configuration#access-to-global-configurations) hook to get access to the current cache provider as well as other configurations including `mutate`:

```jsx
import { useSWRConfig } from 'swr'

function Avatar() {
  const { cache, mutate, ...extraConfig } = useSWRConfig()
  // ...
}
```

If it's not under any `<SWRConfig>`, it will return the default configurations.

## Experimental: Extend Cache Provider

<Callout emoji="🧪">
   This is an experimental feature, the behavior might change in future upgrades.
</Callout>

When multiple `<SWRConfig>` components are nested, cache provider can be extended.

The first argument for the `provider` function is the cache provider of the upper-level `<SWRConfig>` (or the default cache if there's no parent `<SWRConfig>`), you can use it to extend the cache provider:

```jsx
<SWRConfig value={{ provider: (cache) => newCache }}>
  ...
</SWRConfig>
```

## Examples

### Mutate Multiple Keys from RegEx

With the flexibility of the cache provider API, you can even build a "partial mutation" helper.

In the example below, `matchMutate` can receive a regex expression as key, and be used to mutate the ones who matched this pattern.

```js
function useMatchMutate() {
  const { cache, mutate } = useSWRConfig()
  return (matcher, ...args) => {
    if (!(cache instanceof Map)) {
      throw new Error('matchMutate requires the cache provider to be a Map instance')
    }

    const keys = []

    for (const key of cache.keys()) {
      if (matcher.test(key)) {
        keys.push(key)
      }
    }

    const mutations = keys.map((key) => mutate(key, ...args))
    return Promise.all(mutations)
  }
}
```

Then inside your component:

```jsx
function Button() {
  const matchMutate = useMatchMutate()
  return <button onClick={() => matchMutate(/^\/api\//)}>
    Revalidate all keys start with "/api/"
  </button>
}
```

<Callout>
  Note that this example requires the cache provider to be a Map instance.
</Callout>

### LocalStorage Based Persistent Cache

You might want to sync your cache to `localStorage`. Here's an example implementation:

```jsx
function localStorageProvider() {
  // When initializing, we restore the data from `localStorage` into a map.
  const map = new Map(JSON.parse(localStorage.getItem('app-cache') || '[]'))

  // Before unloading the app, we write back all the data into `localStorage`.
  window.addEventListener('beforeunload', () => {
    const appCache = JSON.stringify(Array.from(map.entries()))
    localStorage.setItem('app-cache', appCache)
  })

  // We still use the map for write & read for performance.
  return map
}
```

Then use it as a provider:

```jsx
<SWRConfig value={{ provider: localStorageProvider }}>
  <App/>
</SWRConfig>
```

<Callout>
  As an improvement, you can also use the memory cache as a buffer, and write to `localStorage` periodically. You can also implement a similar layered cache with IndexedDB or WebSQL.
</Callout>

### Reset Cache Between Test Cases

When testing your application, you might want to reset the SWR cache between test cases. You can simply wrap your application with an empty cache provider. Here's an example with Jest:

```jsx
describe('test suite', async () => {
  it('test case', async () => {
    render(
      <SWRConfig value={{ provider: () => new Map() }}>
        <App/>
      </SWRConfig>
    )
  })
})
```

### Access to the Cache

Alert: you should not write to the cache directly, it might cause undefined behavior.

```jsx
const { cache } = useSWRConfig()

cache.get(key) // Get the current data for a key.
cache.clear()  // ⚠️ Clear all the cache. SWR will revalidate upon re-render.
```
