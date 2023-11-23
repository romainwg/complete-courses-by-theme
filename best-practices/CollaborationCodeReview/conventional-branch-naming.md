# Branch Naming Convention Guidelines

<!-- https://stackoverflow.com/a/6065944 -->
<!-- https://idiv-biodiversity.github.io/git-knowledge-base/branch-naming-conventions.html -->
<!-- https://www.atlassian.com/git/tutorials/comparing-workflows/gitflow-workflow -->
<!-- https://www.gitkraken.com/blog/gitflow -->
<!-- https://nvie.com/posts/a-successful-git-branching-model/ -->

- [Branch Naming Convention Guidelines](#branch-naming-convention-guidelines)
  - [Introduction](#introduction)
  - [Branch Naming Convention](#branch-naming-convention)
  - [Categories Explained](#categories-explained)
  - [How to Use the Branch Naming Convention](#how-to-use-the-branch-naming-convention)
    - [Examples](#examples)
  - [Practical Tips for Using the Convention](#practical-tips-for-using-the-convention)
  - [Regular Expression for Validation](#regular-expression-for-validation)
  - [Conclusion](#conclusion)

## Introduction

In software development, maintaining clarity and organization in code repositories is crucial for effective collaboration and project management. A well-defined branch naming convention in GitLab or any version control system plays a pivotal role in achieving this. It helps in categorizing work, linking branches to specific tasks or issues, and simplifying navigation within the repository. The goal of this document is to outline our standardized branch naming convention and provide guidance on its usage, ensuring that our development process is streamlined, transparent, and efficient.

![alt git-flow-nvie](git-flow-nvie.png "gitflow")

## Branch Naming Convention

The branch naming convention follows the format: `[category]/[issue-number-?][description]`

The components of this format are:

1. **Category**: The type of work (e.g., `feature`, `bugfix`, `ci`, `configuration`).
2. **Issue Number (Optional)**: If linked to a specific issue or ticket, include the number.
3. **Description**: A brief, descriptive name of the work.

## Categories Explained

- `feature`: New features or significant changes.
- `bugfix`: Bug fixes or issue resolutions.
- `documentation`: Updates to documentation.
- `refactor`: Code refactoring.
- `test`: Adding or updating tests.
- `hotfix`: Urgent fixes for production issues.
- `experiment`: Experimental features or code.
- `release`: Preparing release versions.
- `ci`: Continuous Integration and DevOps modifications.
- `configuration`: Changes to configuration files.

## How to Use the Branch Naming Convention

1. **Choosing the Right Category**: Select a category that best describes the nature of your work.
2. **Issue Number (If Applicable)**: If your work corresponds to a specific issue, include its number right after the category.
3. **Descriptive Naming**: Choose a name that concisely describes the work or changes made in the branch.

### Examples

- `ci/update-gitlab-pipeline`
- `configuration/update-env-example`
- `feature/123-add-payment-gateway`
- `bugfix/321-fix-checkout-error`
- `documentation/api-endpoints-update`

## Practical Tips for Using the Convention

- **Tab Expansion**: Use the TAB key to auto-complete branch names. For instance, typing `git checkout feat<TAB>` in the terminal will display a list of branches starting with `feat/`. This feature enhances speed and accuracy in navigating branches.

- **Branch Searching**: Employ commands like `git branch --list "feature/*"` to filter and find specific branches. This method is particularly useful for quickly locating branches in a category, especially in repositories with numerous branches.

## Regular Expression for Validation

To ensure that the branch names adhere to the convention, you can use a regular expression (regex). This regex will check if the branch name follows the specified format:

```regex
^(feature|bugfix|documentation|refactor|test|hotfix|experiment|release|ci|configuration)\/(\d+-)?[a-z0-9-]+$
```

## Conclusion

By adhering to this branch naming convention, we ensure a well-organized and navigable codebase, facilitating better communication and efficiency in our development process. It's important for every team member to understand and consistently apply this convention. This standardization not only benefits individual developers but also enhances our collective ability to manage and scale our software projects effectively.
