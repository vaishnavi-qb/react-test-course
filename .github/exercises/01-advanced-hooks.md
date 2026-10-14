# Issue #1: Advanced Hooks and Lifecycle Management

You have the clothing-store repo. Do only the steps in this issue. Work on one branch.

## 1. Open this branch

From the repo root:

```bash
git switch main
git pull origin main
git switch -c exercise-01-advanced-hooks
```

If your default branch is not `main`, use that name instead of `main`.

## 2. Open these files

- `ecommerce-frontend/src/pages/ProductDetails.jsx`
- `ecommerce-frontend/src/components/Navbar.jsx`
- `ecommerce-frontend/src/pages/Home.jsx`

## 3. Do this

1. In `ProductDetails.jsx`, the `useEffect` that calls `api.get(\`/products/${id}\`)` can finish after the user has already opened a different product. Add a `cancelled` flag. Set it to `true` in the effect cleanup. After `await`, update state only when `cancelled` is still `false`. When `id` changes, set `product` back to `null` before the new request.
2. In `Navbar.jsx`, the `useEffect` that calls `api.get('/cart')` has the same problem. Use the same `cancelled` flag so a response after logout or unmount does not call `dispatch(setCart(...))`.
3. Create `ecommerce-frontend/src/hooks/useWindowEvent.js`. It takes an event name and a handler, calls `window.addEventListener`, and removes that listener in the cleanup. Use it in `Home.jsx` for the scroll listener that calls `handleLoadMore`. Delete the manual `addEventListener` / `removeEventListener` block in that effect.
4. Use `useWindowEvent` a second time in `ProductDetails.jsx`: listen for `keydown` and, when the key is `Escape` and the login modal is open, close the modal.

Do not change cart, login, or checkout behavior beyond the steps above.

## 4. Use these prompts

Copy the whole block under Explore, Plan, or Review. Paste it into your AI assistant. Do not edit the text. Read [the prompting guide](../PROMPTING.md) if needed.

### Explore — copy and paste

```text
Act as a senior React tutor. I am on branch exercise-01-advanced-hooks in this clothing-store repo.

Open ecommerce-frontend/src/pages/ProductDetails.jsx and explain the product fetch useEffect from render through cleanup: dependencies, when it runs, and what happens if the user opens product A then product B before A returns.

Then briefly check the cart useEffect in ecommerce-frontend/src/components/Navbar.jsx and the scroll listener in ecommerce-frontend/src/pages/Home.jsx.

End with one short quiz question about stale responses. Do not edit files. Do not write a solution.
```

### Plan — copy and paste

```text
Act as a senior React tutor. I am implementing Exercise 01 on branch exercise-01-advanced-hooks.

I must:
1. Add a cancelled flag to the ProductDetails product fetch and the Navbar cart fetch so late responses do not update state.
2. Create ecommerce-frontend/src/hooks/useWindowEvent.js and use it for the Home scroll listener and for Escape closing the login modal in ProductDetails.

Give me a short plan with the files to touch, then one hint for step 1 only. Wait for me before the next hint. Do not write the implementation. Do not edit files.
```

### Review — copy and paste

```text
Act as a code reviewer for Exercise 01. Review my current git diff only.

Check that:
- ProductDetails and Navbar effects use a cancelled flag and cleanup
- product is cleared when id changes
- useWindowEvent exists and is used in Home (scroll) and ProductDetails (Escape)
- cart, login, and checkout behavior were not changed beyond that

Map each item to evidence in the diff. List anything missing. Do not edit files or rewrite the code.
```

## 5. Check your work

```bash
npm run lint --prefix ecommerce-frontend
npm run build --prefix ecommerce-frontend
```

Then run the storefront (`npm run dev --prefix ecommerce-frontend`) and confirm:

- Open a product, then open another product quickly. The page shows the second product, not the first.
- Scroll the home page to the bottom. More products still load, and leaving the page does not throw a state-update warning.
- On a product page, open the login modal and press Escape. The modal closes.

## 6. Submit

```bash
git add ecommerce-frontend/src/pages/ProductDetails.jsx ecommerce-frontend/src/components/Navbar.jsx ecommerce-frontend/src/pages/Home.jsx ecommerce-frontend/src/hooks/useWindowEvent.js
git commit -m "Fix stale effects and share the window listener hook"
git push -u origin HEAD
```

Open a pull request into `main`. Wait until **Validate exercise** is green. Merge the pull request. Close this issue only after the merge.
