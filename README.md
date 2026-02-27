# sdk

## Recommended

A collection of existing widely adopted tools that every project should include by default that doesn't inflate bundle size.

### Libraries

- [lodash-es](https://www.npmjs.com/package/lodash-es) - Micro utils such as `sum(1,2,3)`
- [type-fest](https://www.npmjs.com/package/type-fest) - Type utils such as `JsonValue`

### Polyfills

- [iterator-helpers-polyfill](https://www.npmjs.com/package/iterator-helpers-polyfill)
- [urlpattern-polyfill](https://www.npmjs.com/package/urlpattern-polyfill)
- [temporal-polyfill](https://www.npmjs.com/package/temporal-polyfill)

Even though these may result in bundle size increase up to 100kb gzip, there are assumed to be already shipped.
You can conditionally import polyfills that they are excluded from bundle and downloaded only if user's browser misses needed support.

#### Example

**`polyfills.ts`**
```ts
/* requestIdleCallback */

window.requestIdleCallback ??= callback => {
  const start = Date.now()
  return setTimeout(() => callback({
    didTimeout: false,
    timeRemaining: () => Math.max(0, 50 - (Date.now() - start))
  }), 1) as unknown as number
}
window.cancelIdleCallback ??= clearTimeout


/* `Array.prototype.at` */

Array.prototype.at ??= function (index) {
  if (index < 0) return this[this.length - 1 + index]
  return this[index]
}

/* iterator-helpers-polyfill */

if (window.Iterator?.prototype.filter == null) {
  const { installIntoGlobal } = await import("iterator-helpers-polyfill")
  installIntoGlobal()
}

/* URLPattern */

// @ts-expect-error `URLPattern` exists in `Global`.
if (window.URLPattern == null) {
  await import("urlpattern-polyfill")
}
```

**`index.ts`**
```ts
import "./polyfills.ts"
```

### Specific Libraries

There are more specific libraries that solve one specific problem, [here's a list](./specific-tools.md).

## SDK

### Install

```bash
bun i @denshya/sdk
```

### Tools

|Name||
|---|---|
|`bem`||
|`isRecord`||
|`interpolate`||
|`stopPropagation`||
|`inputValue`||
|`BiMap`||
|`Enum`||
|`FileTranform` (fetch/url)||
|`percentage`||
|`phonenumber`||
|`price`||
|`progress`||
|`Time`||
|`TimeSpan`||
|`Units`||
|`predicates`||
|`getCircularReplacer`||
|`KeyChain`||
|`measurePerformance`||
|`TextNodeUtils`||
|`AudioTools`||
|`Viewport`||
|`ClientSocket`||
|`FilePreview`||
|`FormRecord`||
|`FormIssues`||
|`FormDataEnhanced`||
|`WindowTab`||

### Types

- URL*
- FormElements
- ExtractInterpolations
