# Issue #5: Server-State Management with TanStack Query

Finish Exercise 04 and merge it before you start.

## 1. Open this branch

```bash
git switch main
git pull origin main
git switch -c exercise-05-tanstack-query
```

## 2. Install the library

From `ecommerce-frontend`:

```bash
npm install @tanstack/react-query
```

## 3. Open these files

- `ecommerce-frontend/src/main.jsx`
- `ecommerce-frontend/src/pages/Home.jsx`
- `ecommerce-frontend/src/pages/ProductDetails.jsx`

## 4. Do this

1. In `main.jsx`, wrap the app in `QueryClientProvider`. Create the client in `ecommerce-frontend/src/queryClient.js` with `staleTime: 60_000` and `retry: 1`. Export that client.
2. In `Home.jsx`, delete the `useEffect` that calls `api.get` for the product list. Load the first page with `useQuery`. The query key must be `['products', { search: searchQuery, category }]`.
3. Keep "load more" as a `useInfiniteQuery` or as a `fetchNextPage` flow on that same key family. The Next button or the existing scroll loader must request the next `pageNumber` and append products. Show three different UI states: `Loading products...`, the error message from the failed request, and `No products found` when the list is empty.
4. In `ProductDetails.jsx`, load the product with `useQuery` and key `['product', id]`.
5. Change add-to-cart in `ProductDetails.jsx` to `useMutation`. On success, invalidate the `['cart']` query. Do not invalidate the product list.

Write the retry and stale-time choice in a 5-line comment at the top of `queryClient.js`.

## 5. Use these prompts

Copy the whole block. Paste it into your AI assistant. Do not edit the text.

### Explore — copy and paste

```text
Act as a senior React tutor. I am on branch exercise-05-tanstack-query in this clothing-store repo.

Trace the product list fetch in ecommerce-frontend/src/pages/Home.jsx and the product fetch in ecommerce-frontend/src/pages/ProductDetails.jsx. Classify each piece of state as server state, local UI state, or global client state, and say which parts TanStack Query should own. End with one short quiz question. Do not edit files. Do not write a solution.
```

### Plan — copy and paste

```text
Act as a senior React tutor. I am implementing Exercise 05 on branch exercise-05-tanstack-query.

I must add QueryClientProvider with staleTime 60000 and retry 1, load Home with key ['products', { search, category }], load ProductDetails with key ['product', id], show loading/error/empty states, and use a mutation for add-to-cart that invalidates ['cart'] only.

Give a short plan, then one hint for queryClient.js and main.jsx only. Wait for me before the next hint. Do not generate the full implementation. Do not edit files.
```

### Review — copy and paste

```text
Act as a code reviewer for Exercise 05. Review my current git diff only.

Check query keys, cache reuse when returning to Home, loading/error/empty UI, mutation invalidates ['cart'] and not the product list, and the staleTime/retry comment in queryClient.js. Map each requirement to the diff. List gaps. Do not edit files.
```

## 6. Check your work

```bash
npm run lint --prefix ecommerce-frontend
npm run build --prefix ecommerce-frontend
```

In the storefront:

- Open Home, go to a product, then go back. The product list does not send a second request within 60 seconds (check the Network tab).
- Changing `?search=` does send a new request.
- Stop the backend and reload Home. You see the error message, not a blank page.
- Add a product to the cart. The navbar count updates after the mutation succeeds.

## 7. Submit

```bash
git add ecommerce-frontend/package.json ecommerce-frontend/package-lock.json ecommerce-frontend/src/main.jsx ecommerce-frontend/src/queryClient.js ecommerce-frontend/src/pages/Home.jsx ecommerce-frontend/src/pages/ProductDetails.jsx
git commit -m "Load products and cart updates with TanStack Query"
git push -u origin HEAD
```

Open a pull request into `main`. Merge it after **Validate exercise** is green. Then close this issue.
