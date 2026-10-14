# Issue #7: TypeScript with React

Finish Exercise 06 and merge it before you start. Convert only the files listed here. Leave the rest of the app in JavaScript.

## 1. Open this branch

```bash
git switch main
git pull origin main
git switch -c exercise-07-typescript-react
```

## 2. Turn on TypeScript

From `ecommerce-frontend`:

```bash
npm install -D typescript
```

Create `ecommerce-frontend/tsconfig.json` with `"strict": true`, `"jsx": "react-jsx"`, `"noEmit": true`, and `"include": ["src"]`.

Add this script to `ecommerce-frontend/package.json`:

```json
"typecheck": "tsc -p tsconfig.json --pretty false"
```

## 3. Do this

1. Add `ecommerce-frontend/src/types/product.ts` with a `Product` type that matches the product JSON this app already uses: `_id`, `name`, `price`, `image`, `category`, `description`, `rating`, `numReviews`, and `countInStock`. Mark a field optional only if the UI already runs when that field is missing.
2. Rename these files from `.jsx` to `.tsx` and type their props and state. Do not use `any`.
   - `ecommerce-frontend/src/pages/ProductDetails.jsx`
   - `ecommerce-frontend/src/components/ProtectedRoute.jsx`
3. Move `ecommerce-frontend/src/hooks/useWindowEvent.js` to `useWindowEvent.ts`. Type the handler so a `keydown` listener receives `KeyboardEvent` and the scroll listener still typechecks. Delete the `.js` file.
4. In `.github/workflows/validate-exercise.yml`, add a step after **Lint frontend**:

```yaml
      - name: Typecheck frontend
        run: npm run typecheck --prefix ecommerce-frontend
```

## 4. Use these prompts

Copy the whole block. Paste it into your AI assistant. Do not edit the text.

### Explore — copy and paste

```text
Act as a senior React tutor. I am on branch exercise-07-typescript-react in this clothing-store repo.

Inspect ecommerce-frontend/src/pages/ProductDetails.jsx and how product JSON is used from the API. List the runtime shapes, including missing fields and failure cases. Propose which fields belong on a Product type and which should be optional, with reasons from the code. Do not assume the API is safer than the UI already handles. Do not edit files. Do not write the full conversion.
```

### Plan — copy and paste

```text
Act as a senior React tutor. I am implementing Exercise 07 on branch exercise-07-typescript-react.

I must add strict tsconfig and a typecheck script, create src/types/product.ts, convert ProductDetails and ProtectedRoute to .tsx, move useWindowEvent to .ts, and add a Typecheck frontend step to validate-exercise.yml. Avoid any.

Give a short plan, then one hint for tsconfig.json and the typecheck script only. Wait for me before the next hint. Do not write the full conversion. Do not edit files.
```

### Review — copy and paste

```text
Act as a code reviewer for Exercise 07. Review my current git diff only.

Check strict TypeScript setup, Product type, typed ProductDetails and ProtectedRoute, typed useWindowEvent, no any, and the CI typecheck step. Map each requirement to the diff. List gaps. Do not edit files.
```

## 5. Check your work

```bash
npm run typecheck --prefix ecommerce-frontend
npm run lint --prefix ecommerce-frontend
npm run build --prefix ecommerce-frontend
```

`npm run typecheck` must exit 0. Opening a product, a missing product, and `/cart` while logged out must still behave as they did after Exercise 02.

## 6. Submit

```bash
git add ecommerce-frontend/package.json ecommerce-frontend/package-lock.json ecommerce-frontend/tsconfig.json ecommerce-frontend/src .github/workflows/validate-exercise.yml
git commit -m "Type the product page and protected route"
git push -u origin HEAD
```

Open a pull request into `main`. Merge it after **Validate exercise** is green. Then close this issue.
