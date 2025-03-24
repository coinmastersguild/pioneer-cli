# Pull Request Protocol for DegenQuest

## Overview
This document outlines the standardized procedure for creating, reviewing, and merging pull requests within the DegenQuest project. Following these guidelines ensures consistency, improves code quality, and maintains proper documentation of changes.

## Branch Structure
- `master`: Production-ready code
- `develop`: Integration branch for feature development
- Feature branches: Created from and merged back to `develop`
- Hotfix branches: Created from `master` for critical fixes

## Branch Naming Convention
- Feature branches: `feature/descriptive-name`
- Bug fix branches: `fix/issue-description`
- Hotfix branches: `hotfix/critical-issue`
- Release branches: `release/version-number`

## Pull Request Creation Process

### 1. Prepare Your Changes
1. Make sure your branch is up to date with its base branch
   ```bash
   git checkout develop
   git pull
   git checkout your-branch
   git rebase develop
   ```
2. Ensure all tests pass and the code builds successfully
3. Update documentation as necessary

### 2. Creating a PR with GitHub CLI
The GitHub CLI (`gh`) is the preferred tool for creating pull requests. Follow these steps:

1. Push your changes to the remote repository
   ```bash
   git push -u origin your-branch
   ```

2. Create the pull request using the GitHub CLI
   ```bash
   gh pr create --base master --head your-branch --title "Your PR Title" --body-file path/to/pr-template.md
   ```

   If submitting to develop instead:
   ```bash
   gh pr create --base develop --head your-branch --title "Your PR Title" --body-file path/to/pr-template.md
   ```

3. Alternative approach (if you need to write the PR body in-line):
   ```bash
   gh pr create --base master --head your-branch --title "Your PR Title"
   ```
   This will open an editor where you can paste the PR template and fill it out.

### 3. PR Template
Every pull request should follow this template:

```markdown
## PR Overview
[Provide a brief overview of what this PR accomplishes]

## Related Issue
[Link to the related issue or ticket]

## Changes Made
- [Item 1: Description of specific change]
- [Item 2: Description of specific change]
- [Item 3: Description of specific change]

## Testing Performed
[Describe how you tested these changes]

## Screenshots (if applicable)
[Add screenshots demonstrating the changes if relevant]

## Performance Impact
[Describe any performance implications of this change]

## Documentation
[List documentation that was added or updated]

## Checklist
- [ ] Tests added/updated
- [ ] Documentation updated
- [ ] Sprint report updated
- [ ] All CI checks pass
- [ ] No new warnings introduced
```

### 4. Pull Request Review
1. Request reviews from at least two team members
2. Address all comments and resolve discussions
3. Get required approvals before merging

### 5. Merging
1. Ensure all CI checks pass
2. Use the "Squash and merge" option for feature branches to keep history clean
3. Use "Create a merge commit" for release branches to preserve history
4. Delete the branch after merging (option in GitHub PR interface)

## Tips for Successful PRs
1. Keep PRs small and focused on a single issue or feature
2. Include screenshots or videos for UI changes
3. Provide clear descriptions of what changed and why
4. Reference related issues or PRs
5. Respond promptly to review comments

## Common PR Commands with GitHub CLI

### List Pull Requests
```bash
gh pr list
```

### Check PR Status
```bash
gh pr status
```

### View a PR in the Browser
```bash
gh pr view --web
```

### Add Reviewers
```bash
gh pr edit --add-reviewer username1,username2
```

### Checking Out a PR Locally
```bash
gh pr checkout PR_NUMBER
```

### Merging a PR from CLI
```bash
gh pr merge PR_NUMBER
```

## References
- [GitHub CLI Documentation](https://cli.github.com/manual/)
- [GitHub Flow Documentation](https://docs.github.com/en/get-started/quickstart/github-flow)
