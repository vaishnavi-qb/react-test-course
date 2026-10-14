# Issue #9: Moving from Vite to Next.js

Finish Exercise 08 and merge it before you start. Leave the Vite app in `ecommerce-frontend` working.

## 1. Open this branch

```bash
git switch main
git pull origin main
git switch -c exercise-09-nextjs
```

## 2. Create the Next.js app

From the repo root:

```bash
npx create-next-app@latest ecommerce-next --js --app --eslint --no-tailwind --no-src-dir --import-alias "@/*"
```

Use the current stable Next.js. Do not put this app inside `ecommerce-frontend`.

## 3. Do this

1. Copy only the product-details feature. Add `ecommerce-next/app/product/[id]/page.js`.
2. That page is a Server Component. It fetches `process.env.API_PUBLIC_URL + '/api/products/' + id` on the server. If the product is missing, call `notFound()`.
3. Add `ecommerce-next/app/product/[id]/AddToCartButton.js` with `'use client'` at the top. The button is the only client component. It does not fetch the product.
4. Add `ecommerce-next/README.md` with these exact headings and fill them in:
   - How to run (`npm install` and `npm run dev` inside `ecommerce-next`)
   - Env vars (`API_PUBLIC_URL` only; no secret values)
   - What is rendered on the server (the product page)
   - What is a client component (the add-to-cart button) and why
5. In `.github/workflows/validate-exercise.yml`, add a step after the Vite build:

```yaml
      - name: Build Next.js app
        working-directory: ecommerce-next
        run: |
          npm ci
          npm run build
        env:
          API_PUBLIC_URL: http://localhost:3000
```

Commit `ecommerce-next/package-lock.json`.

## 4. Use these prompts

Copy the whole block. Paste it into your AI assistant. Do not edit the text.

### Explore — copy and paste

```text
Act as a senior React tutor. I am on branch exercise-09-nextjs in this clothing-store repo.

Trace the product detail feature in the Vite app (route, data fetch, add-to-cart in ecommerce-frontend). Explain which parts need the browser and how that maps to a Server Component product page plus a client AddToCartButton in a new ecommerce-next app. End with one short quiz question. Do not edit files. Do not generate the Next.js app.
```

### Plan — copy and paste

```text
Act as a senior React tutor. I am implementing Exercise 09 on branch exercise-09-nextjs.

I must create ecommerce-next with create-next-app, add app/product/[id]/page.js as a Server Component that fetches from API_PUBLIC_URL, call notFound() when missing, add a client AddToCartButton.js, write ecommerce-next/README.md with the required headings, and add a Next.js build step to validate-exercise.yml. Keep ecommerce-frontend working.

Give a short plan, then one hint for the Server Component page only. Wait for me before the next hint. Do not generate the whole app. Do not edit files.
```

### Review — copy and paste

```text
Act as a code reviewer for Exercise 09. Review my current git diff only.

Check Server/Client boundaries, notFound for missing products, Vite still builds, Next.js CI build step, README headings, and that ecommerce-frontend was not replaced. Map each requirement to the diff. List gaps. Do not edit files.
```

## 5. Check your work

```bash
npm run build --prefix ecommerce-frontend
npm ci --prefix ecommerce-next
npm run build --prefix ecommerce-next
```

Vite `npm run dev --prefix ecommerce-frontend` still opens the existing store. `npm run dev --prefix ecommerce-next` opens the product page at `/product/<a real id>` and shows the product name without a client-side fetch in the Network tab.

## 6. Submit

```bash
git add ecommerce-next .github/workflows/validate-exercise.yml
git commit -m "Serve one product page from a separate Next.js app"
git push -u origin HEAD
```

Open a pull request into `main`. Merge it after **Validate exercise** is green. Then close this issue.
