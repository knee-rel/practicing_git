# ITMGT 45.03 — Git Activity: Hello Pull Request

**Goal:** every one of you runs the full loop once: branch, file, commit, push, Pull Request, review, merge. You add **one new file**, so nothing can conflict.

**Your numbers (from the roster):** Group ___ · Member # ___ · GitHub username ___
**Member 1 is the Captain.** The Captain owns your group's repo, **reviews and merges** your PRs, and gets their own PR reviewed by Member 2.

---

## 0. Before class (15 min)

### Captain only (Member 1)
1. On the instructor's repo page, click **Use this template → Create a new repository**. Name it `itmgt4503-group<N>-git` (for example `itmgt4503-group2-git`), choose **Public**, and click **Create repository**.
2. In your new repo: **Settings → Collaborators → Add people**. Invite every teammate by GitHub username. They have 7 days to accept.
3. Send your teammates the repo link, and send it to the instructor too.
4. *(Optional)* Make `main` safe: **Settings → Rules → Rulesets → New branch ruleset**, target the default branch, tick **Require a pull request before merging** and **Block force pushes**, and set **Active**. Then a push straight to `main` is refused.

### Everyone
1. **GitHub account:** create one at github.com/signup, send your username to your Captain, and **accept the email invitation** (or open `https://github.com/<captain-username>/<repo-name>/invitations`).
2. **Install Git**
   - **Mac** (Terminal): `git --version`. If a popup offers developer tools, click Install, then run it again.
   - **Windows** (PowerShell, not cmd): `winget install --id Git.Git -e --source winget`, then **close and reopen PowerShell** and run `git --version`. No `winget`? Use the installer at git-scm.com/download/win.
3. **Tell Git who you are**
   ```
   git config --global user.name "Your Full Name"
   git config --global user.email "you@example.com"
   git config --global init.defaultBranch main
   git config --global pull.rebase false
   ```
4. **Sign in** (GitHub doesn't accept your password in the terminal)
   - **Windows:** the first push usually opens a browser sign-in. Complete it.
   - **Mac:** install GitHub CLI (`brew install gh` or cli.github.com), run `gh auth login` (GitHub.com → HTTPS → Yes → browser), then check `gh auth status`.
5. **Clone your group's repo** (the link your Captain sent) into a plain folder (not iCloud, OneDrive, Desktop or Documents):
   ```
   cd ~
   mkdir itmgt4503
   cd itmgt4503
   git clone https://github.com/CAPTAIN-USERNAME/REPO-NAME.git
   cd REPO-NAME
   git status
   ```
   You should see `On branch main` and `nothing to commit, working tree clean`. Open it in VS Code with `code .`

Stuck? Use **GitHub Desktop**, or the **browser-only path** at the bottom. Never let someone else commit for you.

---

## 1. What you edit

You create **one file**: `team/<your-github-username>.txt`, copied from `team/_template.txt`. Fill all 7 lines and **save**.

Never touch the template or anyone else's file. Edit in VS Code, not Notepad.

## 2. Branching in one minute

`main` is the official copy. A **branch** is your own line of history that joins `main` only through a reviewed Pull Request.

Branch name: `g<group>/m<member>-hello`, so Group 2, Member 4 is `g2/m4-hello`.

```
git switch main
git pull
git switch -c g2/m4-hello
```

Before every `git add`, check that `git status` says `On branch g2/m4-hello`, not `main`.

---

## 3. The steps (example: Group 2, Member 4)

Everyone does this at the same time, Captain included:
```
git switch main
git pull
git switch -c g2/m4-hello
cp team/_template.txt team/your-username.txt
```
Open `team/your-username.txt` in VS Code, fill in all 7 lines, **save**, then:
```
git status
git add team/your-username.txt
git commit -m "Add Member 4 profile (Group 2)"
git push -u origin g2/m4-hello
```
On GitHub: click **Compare & pull request**, set the title to `[G2-M4] Add profile`, and click **Create pull request**.

### Review and merge
- **Captain (reviewer):** for each teammate's PR, open **Files changed** and check 1 file, inside `team/`, filename = author's username, all 7 lines filled. Leave **at least one comment**, then **Review changes → Approve**, then **Merge pull request → Create a merge commit → Confirm → Delete branch**.
- **Captain's own PR:** **Member 2** reviews and approves it, then the Captain merges it.

### Everyone, to finish
```
git switch main
git pull
git log --oneline --graph -8
ls team
```
**Done when** `team/` on `main` holds your whole group's profile files (5 or 6, plus `_template.txt`).

---

## 4. If you see this

| Message | Fix |
|---|---|
| `git: command not found` | Close the terminal, open a new one. Still failing? Reinstall. |
| `fatal: not a git repository` | Wrong folder. `cd ~/itmgt4503/REPO-NAME` |
| `Please tell me who you are` | Run the `git config` lines in step 0.3 |
| `403` / `Permission denied` / password rejected | Accept the Captain's invitation, then `gh auth login` |
| `cp: … No such file` | Wrong folder or typo. Run `pwd`, then `ls team`. |
| `nothing to commit` | You didn't save, or you're on the wrong branch (`git status`) |
| Screen full of `~` | Git opened vim. Press `Esc`, type `:wq`, press Enter |
| **You committed on `main` by mistake** | If you haven't pushed: `git switch -c g2/m4-hello`, `git switch main`, `git reset --hard origin/main`, `git switch g2/m4-hello`, then push the branch. If a push to `main` was refused, the same steps work. |

**Browser-only path:** on the repo page, **Add file → Create new file**, type `team/your-username.txt`, paste the template, **Commit changes → Create a new branch and start a pull request** (name it `g2/m4-hello`) → **Propose changes → Create pull request**.
