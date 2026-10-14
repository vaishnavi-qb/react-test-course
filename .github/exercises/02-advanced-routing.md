# Issue #2: Dynamic Routing and Protected Routes

Finish Exercise 01 and merge it before you start. Do only the steps below.

## 1. Open this branch

```bash
git switch main
git pull origin main
git switch -c exercise-02-advanced-routing
```

## 2. Open these files

- `ecommerce-frontend/src/App.jsx`
- `ecommerce-frontend/src/pages/Home.jsx`
- `ecommerce-frontend/src/pages/ProductDetails.jsx`
- `ecommerce-frontend/src/pages/Login.jsx`
- `ecommerce-frontend/src/components/Navbar.jsx`

## 3. Do this

1. Create `ecommerce-frontend/src/components/ProtectedRoute.jsx`. It reads `isAuthenticated` from the Redux auth state. If the user is not logged in, render `<Navigate to="/login" replace state={{ from: location.pathname + location.search }} />`. If they are logged in, render `<Outlet />`.
2. In `App.jsx`, put `/cart` and `/checkout` inside that protected route. Leave `/`, `/product/:id`, `/login`, `/signup`, and `/order-success` public.
3. In `Login.jsx`, after a successful login, go to `location.state?.from` when it is a path that starts with `/` and does not start with `//`. Otherwise go to `/`. Remove the old `redirectToProductId` branch.
4. In `Home.jsx`, stop reading the query string with `new URLSearchParams(location.search)`. Use `useSearchParams` from `react-router-dom`. Keep the existing `search` query parameter. When `search` is missing, show the normal catalog.
5. In `ProductDetails.jsx`, if the product request fails or returns no product, stop the loader and show the text `Product not found` plus a link back to `/`. Do not leave the previous product on screen.

## 4. Use these prompts

Copy the whole block. Paste it into your AI assistant. Do not edit the text.

### Explore — copy and paste

```text
Act as a senior React tutor. I am on branch exercise-02-advanced-routing in this clothing-store repo.

Trace how a URL becomes a page: open ecommerce-frontend/src/App.jsx for routes, ecommerce-frontend/src/pages/ProductDetails.jsx for /product/:id, ecommerce-frontend/src/pages/Home.jsx for search, and the Redux auth state used for login.

Explain the current behavior for (1) an unknown product id and (2) visiting /cart while logged out. End with one short quiz question. Do not edit files. Do not write a solution.
```

### Plan — copy and paste

```text
Act as a senior React tutor. I am implementing Exercise 02 on branch exercise-02-advanced-routing.

I must:
1. Create ecommerce-frontend/src/components/ProtectedRoute.jsx and wrap /cart and /checkout.
2. After login, redirect to location.state.from when it is a safe same-origin path.
3. Switch Home to useSearchParams for the search query.
4. Show "Product not found" with a link home when the product request fails.

Give a short file plan, then one hint for ProtectedRoute only. Wait for me before the next hint. Do not write the full solution. Do not edit files.
```

### Review — copy and paste

```text
Act as a code reviewer for Exercise 02. Review my current git diff only.

Check ProtectedRoute, /cart and /checkout protection, safe post-login redirect, useSearchParams on Home, and Product not found. Note if protected content can flash before auth is known. Map each requirement to the diff. List gaps. Do not edit files.
```

## 5. Check your work

```bash
npm run lint --prefix ecommerce-frontend
npm run build --prefix ecommerce-frontend
```

In the running storefront:

- Visit `/cart` while logged out. You land on `/login`. After login you return to `/cart`.
- Visit `/product/this-id-does-not-exist`. You see `Product not found`.
- Visit `/?search=shirt`, refresh, then press the browser Back button. The search box and the product list match the URL.

## 6. Submit

```bash
git add ecommerce-frontend/src/App.jsx ecommerce-frontend/src/components/ProtectedRoute.jsx ecommerce-frontend/src/pages/Home.jsx ecommerce-frontend/src/pages/ProductDetails.jsx ecommerce-frontend/src/pages/Login.jsx
git commit -m "Protect cart and checkout and sync search with the URL"
git push -u origin HEAD
```

Open a pull request into `main`. Merge it after **Validate exercise** is green. Then close this issue.
