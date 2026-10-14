# Issue #8: Performance Optimization

Finish Exercise 07 and merge it before you start. Change one list. Do not memoize the whole app.

## 1. Open this branch

```bash
git switch main
git pull origin main
git switch -c exercise-08-performance
```

## 2. Open this file

- `ecommerce-frontend/src/pages/Home.jsx`

## 3. Do this

1. Create `ecommerce-frontend/src/components/ProductCard.jsx` (or `.tsx` if you prefer). Move the single product card markup out of `Home.jsx` into this component. Props are the product and `onOpen`.
2. Wrap `ProductCard` in `React.memo`.
3. In `Home.jsx`, stop passing an inline `() => handleProductClick(product)` on every render. Pass `handleProductClick` and let `ProductCard` call it with the product id.
4. Create `ecommerce-frontend/src/PERFORMANCE.md` and fill these lines with your own numbers:
   - Interaction you measured: scroll the home catalog until "load more" runs once
   - Tool: React DevTools Profiler
   - Before: commit SHA, how many `Home` or card renders you saw for that one scroll
   - Change: `ProductCard` extracted and memoized
   - After: same scroll, same machine, the new render count
   - What you did not memoize, and why

Measure before you add `memo`, then measure again after. Use the same page, the same scroll, and a production build (`npm run build` and `npm run preview --prefix ecommerce-frontend`).

## 4. Use these prompts

Copy the whole block. Paste it into your AI assistant. Do not edit the text.

### Explore — copy and paste

```text
Act as a senior React tutor. I am on branch exercise-08-performance in this clothing-store repo.

Open ecommerce-frontend/src/pages/Home.jsx. Explain why scrolling the catalog and loading more products can cause extra renders of the product list. Form one measurable hypothesis I can check with React DevTools Profiler on a production preview build. Do not suggest memoization yet. Do not edit files.
```

### Plan — copy and paste

```text
Act as a senior React tutor. I am implementing Exercise 08 on branch exercise-08-performance.

I must extract ProductCard, wrap it in React.memo, pass a stable onOpen handler instead of an inline arrow per item, measure before and after with the same scroll, and write ecommerce-frontend/src/PERFORMANCE.md.

Give a short plan for measuring first, then one hint for extracting ProductCard. Wait for me before the next hint. Do not edit files. Do not rewrite Home.jsx for me.
```

### Review — copy and paste

```text
Act as a code reviewer for Exercise 08. Review my current git diff and PERFORMANCE.md.

Check that ProductCard is extracted and memoized, onOpen is stable, before/after numbers are recorded for the same scroll, and behavior still opens /product/:id. Challenge whether memo helped or only added complexity. List gaps. Do not edit files.
```

## 5. Check your work

```bash
npm run lint --prefix ecommerce-frontend
npm run typecheck --prefix ecommerce-frontend
npm run build --prefix ecommerce-frontend
```

Clicking a product still opens `/product/:id`. Search and category pages still list the right products.

## 6. Submit

```bash
git add ecommerce-frontend/src/pages/Home.jsx ecommerce-frontend/src/components/ProductCard.jsx ecommerce-frontend/src/PERFORMANCE.md
git commit -m "Memoize the home product card after a profiler pass"
git push -u origin HEAD
```

If the card file is `.tsx`, add that path instead. Open a pull request into `main`. Merge it after **Validate exercise** is green. Then close this issue.
