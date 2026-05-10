# GitHub Repo Export Workflow

This workflow creates an Excel file with these columns:

- `Repo name`
- `repo hyper link`
- `Last committed to repo`
- `owner name of the repo`

It is read-only:

- It only calls the GitHub API with `GET` requests.
- It does not push, edit, or delete anything in GitHub.
- The Excel file is uploaded as a workflow artifact, not committed back to the repository.

## What you need

1. A repository where you can add a GitHub Actions workflow.
2. A GitHub personal access token saved as a repository secret named `GH_ACCOUNT_READ_TOKEN`.

## Recommended token permissions

Use a token that is read-only.

For private repositories, the simplest option is usually a classic personal access token with:

- `repo` read access

For public repositories only, a token may not even be needed, but keeping one secret makes the workflow more reliable and avoids rate limits.

## Setup

1. Create a repository for this workflow, or use an existing safe utility repository.
2. Copy these files into that repository:
   - `.github/workflows/export-github-repos.yml`
   - `scripts/export_github_repos_to_excel.py`
3. In GitHub, open:
   - `Settings` -> `Secrets and variables` -> `Actions`
4. Add a new repository secret:
   - Name: `GH_ACCOUNT_READ_TOKEN`
   - Value: your read-only GitHub token
5. Commit and push these files.

## Run it

1. Open the repository on GitHub.
2. Open the `Actions` tab.
3. Select `Export GitHub Repos To Excel`.
4. Click `Run workflow`.

## Download the Excel file

1. Open the completed workflow run.
2. Scroll to `Artifacts`.
3. Download `github-repo-export`.

## Notes

- `Last committed to repo` is the author of the latest commit on the repository's default branch.
- The repo count is printed in the workflow logs.
- The export includes repositories visible to the token, including owned repos, collaborator repos, and organization repos.
