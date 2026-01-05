# Change Assurance Window

A reusable GitHub Actions workflow that enforces **production change freezes** using centrally managed change assurance windows.

This repository enables teams to:
- Detect changes to `/prod/` paths
- Block pull requests during active change assurance windows
- Separate policy (dates) from enforcement logic
- Reuse the same control across multiple repositories

---

## How it works

1. A reusable workflow checks whether a pull request modifies any `/prod/` paths  
2. The current date is evaluated against defined change assurance windows  
3. If a window is active, the workflow:
   - Comments on the pull request  
   - Closes the pull request to prevent merging  

Change windows are defined once and applied consistently everywhere.

---

## Repository structure
```
.
├── change-windows.yml
└── .github
└── workflows
└── enforce-prod-change-assurance.yml
```

- **change-windows.yml**  
  Source of truth for all change assurance windows

- **enforce-prod-change-assurance.yml**  
  Reusable workflow containing the enforcement logic

---

## Usage

Reference this workflow from another repository:

```yaml
jobs:
  enforce-ca:
    uses: beckyshaw/change-assurance-window/.github/workflows/enforce-prod-change-assurance.yml@v1
```
## Updating change windows

Update change-windows.yml to add, remove, or amend change assurance windows.
No changes are required in consuming repositories.

## Intended use

#### This repository is designed to support:

- Production change freezes

- Compliance and audit requirements

- Consistent governance across teams
