# ITMGT 45.03 — Git Activity: Hello Pull Request

**Goal:** every one of you runs the full loop once: branch, file, commit, push, Pull Request, review, merge. You add **one new file**, so nothing can conflict.

**Your numbers (from the roster):** Group ___ · Member # ___ · GitHub username ___
Member **k** reviews Member **k+1** (the last member reviews Member 1). **Member 1 is the Captain** and merges.

---

## 0. Before class (15 min)

1. **Install Git**
   - **Mac** (Terminal): `git --version`. If a popup offers developer tools, click Install, then run it again.
   - **Windows** (PowerShell, not cmd): `winget install --id Git.Git -e --source winget`, then **close and reopen PowerShell** and run `git --version`. No `winget`? Use the installer at git-scm.com/download/win.
2. **Tell Git who you are**
   ```
   git config --global user.name "Your Full Name"
   git config --global user.email "you@example.com"
   git config --global init.defaultBranch main
   git config --global pull.rebase false
   ```
3. **Sign in** (GitHub doesn't accept your password in the terminal)
   - **Windows:** the first push usually opens a browser sign-in. Complete it.
   - **Mac:** install GitHub CLI (`brew install gh` or cli.github.com), run `gh auth login` (GitHub.com → HTTPS → Yes → browser), then check `gh auth status`.
4. **Clone** into a plain folder (not iCloud, OneDrive, Desktop or Documents):
   ```
   cd ~
   mkdir itmgt4503
   cd itmgt4503
   git clone https://github.com/YOUR-ORG/YOUR-REPO.git
   cd YOUR-REPO
   git status
   ```
   You should see `On branch main` and `nothing to commit, working tree clean`. Open it in VS Code with `code .`

Stuck? Use **GitHub Desktop**, or the **browser-only path** at the bottom. Never let someone else commit for you.

---

## 1. What you edit

You create **one file**: `team/group-<G>/<your-github-username>.txt`, copied from `team/_template.txt`. Fill all 7 lines and **save**.

Never touch the template, anyone else's file, or other groups' folders. Edit in VS Code, not Notepad.

## 2. Branching in one minute

`main` is the official copy and GitHub blocks direct pushes to it. A **branch** is your own line of history that joins `main` only through a reviewed Pull Request.

Branch name: `g<group>/m<member>-hello`, so Group 2, Member 4 is `g2/m4-hello`.

```
git switch main
git pull
git switch -c g2/m4-hello
```

Before every `git add`, check that `git status` says `On branch g2/m4-hello`, not `main`.

---

## 3. The steps (example: Group 2, Member 4)

### Member 1 goes first: create the group folder
```
git switch main
git pull
git switch -c g2/m1-hello
mkdir team/group-2
cp team/_template.txt team/group-2/your-username.txt
```
Fill in the file, save, then:
```
git add team/group-2/your-username.txt
git commit -m "Add Member 1 profile (Group 2)"
git push -u origin g2/m1-hello
```
On GitHub: **Compare & pull request**, title `[G2-M1] Add profile (creates group folder)`, **Create pull request**. The last member reviews and approves it first, then **Member 1 merges** (Create a merge commit, Confirm, Delete branch) and announces **"Folder's in!"**

### Members 2 to N: wait for "Folder's in!", then
While waiting, draft your 7 lines in a scratch note.
```
git switch main
git pull
ls team
git switch -c g2/m4-hello
cp team/_template.txt team/group-2/your-username.txt
```
`ls team` must show `group-2`. If it doesn't, Member 1 hasn't merged yet.

Fill in the file, save, then:
```
git status
git add team/group-2/your-username.txt
git commit -m "Add Member 4 profile (Group 2)"
git push -u origin g2/m4-hello
```
On GitHub: **Compare & pull request**, title `[G2-M4] Add profile`, **Create pull request**.

### Review and merge
- **Reviewer:** open the PR → **Files changed** → check 1 file, correct folder, filename = author's username, all 7 lines filled → leave **at least one comment** → **Review changes → Approve**.
- **Captain:** **Merge pull request → Create a merge commit → Confirm → Delete branch**.

### Everyone, to finish
```
git switch main
git pull
git log --oneline --graph -8
ls team/group-2
```
**Done when** all your group's profile files (5 or 6) are on `main`.

> If you ever run `git push origin main`, GitHub refuses. That's not a bug. That's the rule.

---

## 4. If you see this

| Message | Fix |
|---|---|
| `git: command not found` | Close the terminal, open a new one. Still failing? Reinstall. |
| `fatal: not a git repository` | Wrong folder. `cd ~/itmgt4503/YOUR-REPO` |
| `Please tell me who you are` | Run the `git config` lines in step 0.3 |
| `403` / `Permission denied` / password rejected | Accept the invite, then `gh auth login` |
| `cp: … No such file` | `git switch main`, `git pull`, `ls team`. If `group-2` is missing, wait for Member 1. |
| `nothing to commit` | You didn't save, or you're on the wrong branch (`git status`) |
| Screen full of `~` | Git opened vim. Press `Esc`, type `:wq`, press Enter |
| **Push to `main` rejected** | You committed on `main`. Rescue: `git switch -c g2/m4-hello`, `git switch main`, `git reset --hard origin/main`, `git switch g2/m4-hello`, then push the branch |

**Browser-only path:** on the repo page, **Add file → Create new file**, type `team/group-2/your-username.txt` (typing `/` makes the folder), paste the template, **Commit changes → Create a new branch and start a pull request** (name it `g2/m4-hello`) → **Propose changes → Create pull request**.
