# GitHub Workflows & Automation

This directory contains continuous integration and maintenance workflows for the profile repository.

---

## 🐍 Snake Contribution Animation (`snake.yml`)

The workflow defined in [.github/workflows/snake.yml](../.github/workflows/snake.yml) generates an interactive snake game animation based on your GitHub contribution graph.

### How It Works

1. **Trigger**:
   - **Scheduled Execution**: Runs daily at midnight UTC (`0 0 * * *`).
   - **Manual Execution**: Can be dispatched manually via GitHub Actions (`workflow_dispatch`).
   - **Push Event**: Automatically triggers on changes pushed to the `main` branch.

2. **Generation**:
   - Uses the [`Platane/snk`](https://github.com/Platane/snk) action to fetch public contribution data for the repository owner.
   - Outputs generated asset files into a temporary `./dist` directory:
     - `github-snake.svg` (Standard light theme)
     - `github-snake-dark.svg` (Dark theme palette)
     - `ocean.gif` (Alternative color palette)

3. **Deployment**:
   - Deploys the built assets from `./dist` to the dedicated `output` orphan branch using [`peaceiris/actions-gh-pages`](https://github.com/peaceiris/actions-gh-pages).
   - The main `README.md` references the generated asset directly from the `output` branch:
     ```markdown
     ![snake gif](https://github.com/<USERNAME>/<USERNAME>/blob/output/github-snake-dark.svg)
     ```

---

## ⚙️ Required Setup & Permissions

For the workflow to commit and push changes to the `output` branch, the default `GITHUB_TOKEN` must have write access:

1. Go to your repository on GitHub: **Settings** → **Actions** → **General**.
2. Scroll to **Workflow permissions**.
3. Select **Read and write permissions**.
4. Check **Allow GitHub Actions to create and approve pull requests** (if applicable).
5. Click **Save**.

### Manual Run

To trigger an immediate update without waiting for midnight:
1. Navigate to the **Actions** tab on GitHub.
2. Select **GitHub Snake Game** from the left sidebar.
3. Click **Run workflow** → select branch `main` → click **Run workflow**.
