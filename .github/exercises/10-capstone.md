# Issue #10: Build a Production-Ready React Application

Finish Exercises 01–09 and merge them before you start. Do not create a second store. You are finishing the store you already have.

## 1. Open this branch

```bash
git switch main
git pull origin main
git switch -c exercise-10-capstone
```

## 2. Do this

1. Create `docs/ARCHITECTURE.md` with these headings, and write 5–10 lines under each one using the code that is already on `main`:
   - Routes (`ProtectedRoute`, public pages)
   - Auth (HTTP-only cookie, what is not stored in `localStorage`)
   - Checkout form (Zod rules)
   - Server state (TanStack Query keys)
   - Client state (Redux, Context, Zustand)
   - The Next.js product page versus the Vite app
2. Walk this path in the Vite app and fix only what is broken on it:
   - Sign up or log in
   - Open a product from Home
   - Add it to the cart
   - Open `/checkout`
   - Submit an empty address form and see field errors
   - Log out and open `/checkout`; you must land on `/login`
3. In `README.md`, add a **Run the store** section at the top of **Local development** with the commands a new person needs:
   - `npm ci` at the repo root
   - `npm ci --prefix ecommerce-frontend`
   - `npm run start` for the API
   - `npm run dev --prefix ecommerce-frontend` for the store
   - `npm ci --prefix ecommerce-next` and `npm run dev --prefix ecommerce-next` for the Next.js product page
   List the env variable names (`MONGO_URI`, `JWT_SECRET`, `CLIENT_URL`, `VITE_API_BASE_URL`, `API_PUBLIC_URL`). Do not put secret values in the file.

## 3. Use these prompts

Copy the whole block. Paste it into your AI assistant. Do not edit the text.

### Explore — copy and paste

```text
Act as a senior React tutor. I am on branch exercise-10-capstone in this clothing-store repo.

Walk the existing shopper path in this codebase: login, open product, add to cart, checkout validation, logout redirect to login for /checkout. Summarize what docs/ARCHITECTURE.md must cover for routes, auth cookie, Zod checkout, TanStack Query, Redux/Context/Zustand, and the Next.js product page. Do not design a new app. Do not edit files.
```

### Plan — copy and paste

```text
Act as a senior React tutor. I am implementing Exercise 10 on branch exercise-10-capstone.

I must write docs/ARCHITECTURE.md with the required headings, fix only what is broken on the shopper path, and add a Run the store section to README.md with the install/run commands and env variable names (no secret values).

Give a short outline for ARCHITECTURE.md based on the current code, then one hint for the README Run the store section. Wait for me before writing more. Do not generate the full documents. Do not edit files.
```

### Review — copy and paste

```text
Act as a skeptical production reviewer for Exercise 10. Review my current git diff only.

Map login, product, cart, checkout field errors, logout redirect, ARCHITECTURE.md headings, Run the store README section, and CI builds to evidence. Prioritize blockers first, then smaller gaps. Do not edit files.
```

## 4. Check your work

```bash
npm test
npm run lint --prefix ecommerce-frontend
npm run typecheck --prefix ecommerce-frontend
npm run build --prefix ecommerce-frontend
npm ci --prefix ecommerce-next
npm run build --prefix ecommerce-next
```

Every command must exit 0. The path in step 2 must work in the browser.

## 5. Submit

```bash
git add docs/ARCHITECTURE.md README.md
git commit -m "Document the store architecture and the local run steps"
git push -u origin HEAD
```

Open a pull request into `main`. Merge it after **Validate exercise** is green. Then close this issue. The workflow marks the track complete and does not open an 11th issue.
