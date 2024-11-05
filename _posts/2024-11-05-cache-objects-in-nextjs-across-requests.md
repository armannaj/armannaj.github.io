---
title: How to cache an object in Next.js across requests and deployments
tags:
  - nextjs
  - next-js
  - react
  - reactjs
  - typescript
date: '2024-11-05'
---
In today’s world, search engine optimization (SEO) feels like a battle. Websites compete to be in the top 10 results on search engines. One key factor that affects ranking is how quickly a web page loads for users.

I regularly use PageSpeed to check the performance of my websites. Recently, I noticed that the Largest Contentful Paint (LCP) metric was higher than it should be, so I decided to lower it as much as possible.

Each time a page is requested, there can be database calls or other resource-heavy operations. Some of these database requests can be cached for a while, which saves time and helps the page load faster.

Next.js provides various caching options for different levels. I am particularly interested in a cache that remains available across different requests and deployments, acting as a separate caching layer.

Next.js offers two ways to achieve this:

## 1) React cache function

React 18 introduced the `cache` function, which is meant to be used only in Server Components. This function acts as a caching layer for server-side rendering. It takes a function as an argument and saves the value it returns.

Here’s how you can use it:

```javascript
// server-side Next.js code
import { cache } from 'react';

export const getCachedItem = cache(async (id: string) => {
  const item = await db.item.findUnique({ id });
  return item;
})
```

You can use the React cache, but there are a few points to consider that might affect your choice:

1.  Each time you call the `cache` function, it creates a new memoized function. This means that if you call `cache` multiple times with the same function, each call will have its own separate cache that doesn't share data with the others.
    
2.  The `cache` function stores both successful results and errors. So if a function fails with certain arguments, that error will be saved and thrown again the next time you call it with those same arguments.
    
3.  It appears to cache results indefinitely, and I’m not quite sure how cache invalidation works. You may want to check the React or [Next.js documentation](https://nextjs.org/docs/app/building-your-application/caching#react-cache-function) for more details on this.
    
4.  It’s also unclear to me what caching component is used behind the scenes on Vercel and what that involves.
    

## 2) Next.js unstable\_cache

Next.js 14 introduced a persistent cache called `unstable_cache`. It uses [Data Cache](https://nextjs.org/docs/app/building-your-application/caching#data-cache) behind the scenes and works across requests and deployments. I really like this feature because it provides clear options for cache invalidation, timeouts, and tags.

Here’s how to use it:

```javascript
import { unstable_cache } from 'next/cache';
 
const getCachedUser = unstable_cache(
  async (id) => getUser(id),
  ['my-app-user'],
  {
	revalidate: 10, // seconds
	tags: ["user-cache-tag"]
  }
);
```

The first parameter is an asynchronous function, similar to React’s cache. The second parameter is an array of strings that serves as the cache item key. If you don’t provide this or pass `undefined`, it will automatically generate a key based on the function name (`getUser`) and its parameters (`id`).

The third parameter is for options. You can find more details in [its documentation](https://nextjs.org/docs/14/app/api-reference/functions/unstable_cache#parameters).

The `unstable_cache` function returns a new function that, when called, returns a Promise resolving to the cached data. When called, If the data isn’t in the cache, the provided function is executed, and its result is cached and returned.

Cache revalidation works in two ways:

1.  **Time-based revalidation:** If the cached data has exceeded a specified timeout (defined by the `revalidate` option in `unstable_cache`), the function will be called again, and its new result will be cached and returned.
    
2.  **On-demand revalidation:** You can manually revalidate a cache item whenever you need to by using the `revalidateTag()` or `revalidatePath()` methods. For more details, check the documentation [here](https://nextjs.org/docs/app/building-your-application/caching#revalidatepath) .
    

I prefer `unstable_cache` over React’s cache because it integrates more smoothly with Vercel’s infrastructure and provides a more effective invalidation API.
