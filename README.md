# Advanced React Architecture Lab

[![Copy the exercise](https://img.shields.io/badge/COPY%20THE%20EXERCISE-%E2%86%92-2ea44f?style=for-the-badge&logo=github&logoColor=white)](https://github.com/vaishnavi-qb/ecommerce-shopping-store/generate)

An issue-driven learning track for production React architecture. It uses a Vite/React storefront and Express/MongoDB backend as the learning codebase; the exercises progressively introduce advanced architecture without replacing the app in advance.

## Start the track

You are looking at the starter repo. Do the steps in order. Each exercise is one branch and one pull request.

1. Click **Copy the exercise** and create the repository under your GitHub account.
2. Clone that new repository to your machine. Open a terminal in the repo root.
3. On GitHub, open the **Actions** tab and run **Initialize exercises** on `main`. Wait until it is green.
4. Open the **Exercise 01** issue. Follow it from the top. It tells you the branch name, the files to open, the edits, three AI tutor prompts (Explore, Plan, Review), the commands to run, and the commit command.
5. Push that branch and open a pull request into `main`. Wait until **Validate exercise** is green. Merge the pull request. Then close the issue.
6. The next issue appears after that merge is validated and the current issue is closed. Repeat step 4 on the new issue. Always start the new branch from an updated `main`:

```bash
git switch main
git pull origin main
git switch -c exercise-0N-short-name
```

7. Stop at Exercise 10. Closing it finishes the track. There is no Exercise 11.

The same instructions are in `.github/exercises/`. If a step is unclear, follow the issue, not this page.

## How the GitHub automation works (beginner guide)

You do not need to be a GitHub Actions expert. Think of three small robots in the **Actions** tab. Each one has one job.

| Robot name | Simple job |
| --- | --- |
| **Initialize exercises** | Opens the first homework issue (Exercise 01) |
| **Validate exercise** | Checks that your code installs, lints, and builds |
| **Advance exercise** | Opens the next homework issue after you finish the current one |

**You** still write the code, open the pull request, merge it, and close the issue. The robots never write code for you and never close an issue for you.

### Simple path from start to finish

1. You copy this template → you get your own repo.  
2. You run **Initialize exercises** → GitHub creates **Issue: Exercise 01**.  
3. You follow that issue on a new branch, push, and open a pull request.  
4. **Validate exercise** runs on your pull request (green = checks passed).  
5. You merge into `main`. **Validate exercise** runs again on `main`.  
6. You close the Exercise 01 issue.  
7. **Advance exercise** checks that `main` is green and that you did not skip earlier issues → it creates **Exercise 02**.  
8. You repeat until Exercise 10. Then it posts a “complete” message. There is no Exercise 11.

```text
You copy the repo
        ↓
Robot: Initialize  →  Issue 01 appears
        ↓
You code on a branch → open a pull request
        ↓
Robot: Validate  →  checks your PR (green or red)
        ↓
You merge to main
        ↓
Robot: Validate  →  checks main again
        ↓
You close the issue
        ↓
Robot: Advance  →  Issue 02 appears (same pattern up to 10)
```

### Where do the exercise instructions come from?

The homework text is already in the repo as Markdown files:

- `.github/exercises/01-advanced-hooks.md` → becomes **Exercise 01**  
- `.github/exercises/02-advanced-routing.md` → becomes **Exercise 02**  
- … up to `10-capstone.md` → **Exercise 10**

When a robot creates an issue, it copies that file into a GitHub Issue so you can read it on the **Issues** tab. Follow the issue. That is your assignment.

### Robot 1 — Initialize exercises

**What it does:** Creates Exercise 01 one time.

**When it runs:** When someone pushes to `main`, or when you click **Run workflow** in the Actions tab.

**What you should do after copying the template:**

1. Open your repo on GitHub.  
2. Click **Actions**.  
3. Click **Initialize exercises**.  
4. Click **Run workflow**.  
5. Wait until it shows a green check.  
6. Open the **Issues** tab — **Exercise 01** should be there.

If Exercise 01 already exists, this robot does nothing. That is normal.

### Robot 2 — Validate exercise

**What it does:** Runs automatic checks on your code. It does **not** create issues.

**When it runs:** Every time you push a branch, open or update a pull request, or merge to `main`.

**What it checks today:**

- Install packages  
- Backend JavaScript syntax  
- Frontend lint  
- Small tests for the exercise scripts  
- Frontend production build  

Later exercises (07 and 09) ask you to add more checks (TypeScript and Next.js). Until you merge those, only the list above runs.

**Green on the pull request** means “this branch looks good.”  
**Green on `main` after merge** is what unlocks the next exercise. Always wait for the `main` check after you merge.

### Robot 3 — Advance exercise

**What it does:** Creates the next exercise issue (02, then 03, …) or says you finished all 10.

**When it runs:** When you close an exercise issue, or when **Validate exercise** finishes successfully on `main`.

**It only creates the next issue if all of these are true:**

1. The issue you closed is a real exercise issue.  
2. That issue is closed.  
3. Every earlier exercise issue is also closed (no skipping).  
4. The next exercise does not already exist.  
5. **Validate exercise** is green for the **latest commit on `main`**.

If something is missing (for example you closed the issue before merge finished), the next issue will not appear yet. Fix the missing step; the Advance robot will try again when validation on `main` succeeds.

### You vs the robots

| Step | Who |
| --- | --- |
| Copy the template and clone | You |
| Run **Initialize exercises** | You click; robot creates Issue 01 |
| Create branch, write code, open PR | You |
| Check that the code builds | Robot: Validate |
| Merge the PR into `main` | You |
| Close the exercise issue | You |
| Open the next exercise issue | Robot: Advance |

### “The next issue did not appear” — checklist

Go through these in order:

1. Is the current exercise issue **closed**?  
2. Are older exercise issues closed too?  
3. Did you **merge** into `main` (not only open a PR)?  
4. On **Actions**, is **Validate exercise** green for the latest commit on `main`?  
5. In **Settings → Actions → General → Workflow permissions**, is write access allowed for workflows? (Needed so issues can be created.)

### Extra detail (optional)

<details>
<summary>Workflow files and scripts (for curious readers)</summary>

| Workflow file | Name you see in Actions |
| --- | --- |
| `.github/workflows/initialize-exercises.yml` | Initialize exercises |
| `.github/workflows/validate-exercise.yml` | Validate exercise |
| `.github/workflows/advance-exercise.yml` | Advance exercise |

| Script | Role |
| --- | --- |
| `.github/scripts/initialize-exercises.mjs` | Creates Exercise 01 from the Markdown file |
| `.github/scripts/advance-exercise.mjs` | Creates the next issue or posts “complete” |
| `.github/scripts/exercise-workflow.mjs` | Shared rules (titles, “can we advance?”) |
| `.github/scripts/github-api.mjs` | Talks to GitHub to create issues |
| `.github/scripts/exercise-workflow.test.mjs` | Tests for those rules (`npm test`) |

Each created issue gets a hidden marker like `<!-- advanced-react-exercise: 1 -->` so the scripts can find it later even if the title changes.

The robots use GitHub’s built-in `GITHUB_TOKEN`. You do not need to create a personal access token for this track.

</details>

## Prompt-based learning

Each issue has three prompts under **Use these prompts**. Each one is labeled **copy and paste**.

1. Select everything inside the ` ```text ` block  
2. Paste it into your AI assistant  
3. Send it as-is — do not fill in blanks or rewrite the prompt  

Order: **Explore** → **Plan** → **Review**. You write the code. Full guide: [.github/PROMPTING.md](.github/PROMPTING.md). Do not paste credentials, tokens, cookies, or `.env` contents.

## Track

Do these in order. The branch name is what you pass to `git switch -c`.

| Issue | Branch | What you do |
| --- | --- | --- |
| 01 | `exercise-01-advanced-hooks` | Stop stale product and cart responses. Share one window-listener hook. |
| 02 | `exercise-02-advanced-routing` | Protect `/cart` and `/checkout`. Read search from the URL. Show a missing product. |
| 03 | `exercise-03-complex-forms` | Validate the checkout address with React Hook Form and Zod. |
| 04 | `exercise-04-authentication-cors` | Move the JWT into an HTTP-only cookie and allow only `CLIENT_URL`. |
| 05 | `exercise-05-tanstack-query` | Load the catalog and product with TanStack Query. |
| 06 | `exercise-06-global-state` | Add a theme Context and a small Zustand UI store. Leave cart and auth in Redux. |
| 07 | `exercise-07-typescript-react` | Type the product page and protected route. Run `tsc` in CI. |
| 08 | `exercise-08-performance` | Measure the home list, then memoize the product card. |
| 09 | `exercise-09-nextjs` | Add a separate Next.js app that serves one product page. |
| 10 | `exercise-10-capstone` | Write the architecture note and confirm the shopper path still works. |

## Local development

Requirements: Node.js 22 or later and npm. The backend also needs the environment variables and services documented in [the backend README](ecommerce-backend/README.md).

```sh
npm ci
npm ci --prefix ecommerce-frontend
npm run start
```

Run the frontend separately with `npm run dev --prefix ecommerce-frontend`. Checks used by CI:

```sh
npm test
npm run lint --prefix ecommerce-frontend
npm run build --prefix ecommerce-frontend
```

The starter application is JavaScript, so CI checks backend syntax, frontend lint, workflow tests, and the production build. Exercise 07 adds strict TypeScript checking, and Exercise 09 adds a separate Next.js build.

The validation workflow uses Node.js 22 and installs the Linux Rolldown binding required by the current Vite toolchain. Later exercises should extend the workflow when they add a TypeScript project or a separate Next.js app so those new checks are part of the same progression gate.
