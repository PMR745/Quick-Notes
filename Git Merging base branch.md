# 🧾 General Git Branching Strategy

Here’s a basic Git workflow we usually follow:

---

### 1. Always pull the latest `main` before starting anything

Run this before creating a new branch:

```bash
git checkout main
git pull origin main
```

---

### 2. Create a new branch from the updated `main`

```bash
git switch -c feature/your-task-name
```

---

### 3. Work on your branch and commit your changes

Make sure your commits are clean and meaningful.

---

### 4. Before merging your branch, sync with `main` again  
_(a.k.a. down-merge or rebase)_

You have two options:

**Option A: Rebase directly from remote**

```bash
git pull origin main --rebase
```

**Option B: Rebase using local `main`**

Make sure your `main` is up to date first:

```bash
git checkout main
git pull origin main
git checkout feature/your-task-name
git rebase main
```

---

### 5. Resolve any conflicts if they come up

During a rebase or merge, Git might show conflicts like this:

```plaintext
<<<<<<< HEAD
// Your changes (current branch)
=======
// Changes from main branch (incoming)
>>>>>>> main
```

To resolve:
- Keep what you want from both or either section.
- Remove the conflict markers (`<<<<<<<`, `=======`, `>>>>>>>`).
- Save the file.

Then continue the rebase:

```bash
git add .
git rebase --continue
```

Or if you're merging:

```bash
git add .
git commit
```

---

### 6. Push your branch and create a PR (pull request)

```bash
git push origin feature/your-task-name
```

---

### 7. After your PR is reviewed and approved, merge it into `main`

Make sure your branch is clean and up to date with `main` before merging.

---
