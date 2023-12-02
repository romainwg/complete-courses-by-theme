# Conventional Commits Writing Tutorial

<!-- https://www.conventionalcommits.org/en/v1.0.0/ -->
<!-- https://github.com/conventional-changelog/commitlint/blob/master/%40commitlint/config-conventional/README.md -->

Conventional Commits are a commit naming system that adds clarity and a standardized structure to commit messages. This tutorial will guide you through the steps and best practices for writing Conventional Commits.

- [Conventional Commits Writing Tutorial](#conventional-commits-writing-tutorial)
  - [What is a Conventional Commit?](#what-is-a-conventional-commit)
  - [Basic Structure of a Conventional Commit](#basic-structure-of-a-conventional-commit)
    - [Structural Elements](#structural-elements)
    - [Common Commit Types](#common-commit-types)
    - [Extended Commit Types](#extended-commit-types)
  - [How to Write a Conventional Commit](#how-to-write-a-conventional-commit)
  - [Best Practices](#best-practices)
  - [Benefits of Conventional Commits](#benefits-of-conventional-commits)
  - [Examples](#examples)
  - [Usage in VSCode with vscode-conventional-commits](#usage-in-vscode-with-vscode-conventional-commits)
    - [Usage](#usage)
  - [Linting Rules with `@commitlint/config-conventional`](#linting-rules-with-commitlintconfig-conventional)
    - [Linting Rules - Conventional Commits](#linting-rules---conventional-commits)

---

## What is a Conventional Commit?

A Conventional Commit is a commit message that follows a certain structure and specific conventions to describe the changes in a commit in a clear and concise way. This specification aims to make commit messages readable by both humans and machines.

## Basic Structure of a Conventional Commit

A Conventional Commit message should follow this structure:

```text
<type>[optional scope]: <description>

[optional body]

[optional footer(s)]
```

### Structural Elements

1. **Type**: Indicates the nature of the commit (e.g., `fix`, `feat`).
2. **Scope** (Optional): Additional context (e.g., `feat(parser):`).
3. **Description**: A concise summary of the changes.
4. **Body** (Optional): Additional details and context.
5. **Footer(s)** (Optional): Additional information, such as `BREAKING CHANGE`.

### Common Commit Types

- `fix`: Fixes a bug (corresponds to PATCH in SemVer).
- `feat`: Adds a new feature (corresponds to MINOR in SemVer).
- `BREAKING CHANGE`: A major change (corresponds to MAJOR in SemVer).

### Extended Commit Types

In addition to the basic types `fix` and `feat`, Conventional Commits can use the following types for better categorization:

- `build`: Changes affecting the build system or external dependencies.
- `chore`: Minor updates or maintenance tasks not altering source code or tests.
- `ci`: Changes related to CI configuration files and scripts.
- `docs`: Adding or modifying documentation.
- `perf`: Performance improvements.
- `refactor`: Code refactoring that doesn't fix a bug or add a feature.
- `revert`: Reverts a previous commit.
- `style`: Changes that do not affect the meaning of the code (formatting, missing semicolons, etc.).
- `test`: Adding or modifying tests.

## How to Write a Conventional Commit

1. **Determine the Type**: Start by identifying if your commit is a fix (`fix`), a new feature (`feat`), or another type (`docs`, `refactor`, `test`, etc.).

2. **Add a Scope (if necessary)**: If your commit pertains to a specific part of the project, add a scope. For example, `feat(parser):`.

3. **Write a Clear Description**: Write a concise summary of what the commit does.

4. **Add a Body (optional)**: Provide additional details about the changes if necessary.

5. **Include One or More Footers (optional)**: Use this section for additional information, like indicating a `BREAKING CHANGE`.

## Best Practices

- Prefix commits with a type, followed by an optional scope, and an exclamation mark for major changes.
- Ensure that the description immediately follows the type/scope.
- Separate the body and footers from the description with a blank line.
- Feel free to use other types than just `feat` and `fix`.

## Benefits of Conventional Commits

- Facilitates automatic generation of CHANGELOGs.
- Allows automatic determination of versions according to SemVer.
- Ensures clear communication about the nature of changes.
- Improves contributions and project maintenance.

By following these guidelines, your commit messages will not only be informative and structured but also extremely useful for automation tools and version management of your project.

## Examples

1. **Commit with Major Change**:

   ```text
   feat: allow provided config object to extend other configs

   BREAKING CHANGE: `extends` key in config file is now used for extending other config files
   ```

2. **Commit with Major Change and !**:

   ```text
   feat!: send an email to the customer when a product is shipped
   ```

3. **Commit with Scope and !**:

   ```text
   feat(api)!: send an email to the customer when a product is shipped
   ```

4. **Commit with Body and Multiple Footers**:

   ```text
   fix: prevent racing of requests

   Introduce a request id and a reference to latest request. Dismiss
   incoming responses other than from latest request.

   Reviewed-by: Z
   Refs: #123
   ```

## Usage in VSCode with [vscode-conventional-commits](https://marketplace.visualstudio.com/items?itemName=vivaxy.vscode-conventional-commits)

The "Conventional Commits" extension for Visual Studio Code assists in

 formulating commit messages conforming to Conventional Commits.

⚠️ By default, the tool commits automatically after specifying the conventional commit.

### Usage

- Access the extension in two ways:
  1. Command + Shift + P or Ctrl + Shift + P, enter "Conventional Commits," and press Enter.
  2. Click the icon in the Source Control menu.

## Linting Rules with `@commitlint/config-conventional`

To ensure that Conventional Commits adhere to established standards, using `@commitlint/config-conventional` is recommended. Here is a summary of linting rules and examples:

### Linting Rules - Conventional Commits

1. **type-enum**
   - Ensures that the `type` is in the predefined list.
   - `error` if not followed.
   - Examples: `echo "foo: some message"` fails, `echo "fix: some message"` passes.

2. **type-case**
   - Checks that the `type` is in lowercase.
   - `error` if not followed.
   - Examples: `echo "FIX: some message"` fails, `echo "fix: some message"` passes.

3. **type-empty**
   - Prohibits an empty `type`.
   - `error` if not followed.
   - Examples: `echo ": some message"` fails, `echo "fix: some message"` passes.

4. **subject-case**
   - Prohibits certain cases for the `subject`.
   - `error` if not followed.
   - Examples: `echo "fix(SCOPE): Some message"` fails, `echo "fix(scope): some message"` passes.

5. **subject-empty**
   - Prohibits an empty `subject`.
   - `error` if not followed.
   - Examples: `echo "fix:"` fails, `echo "fix: some message"` passes.

6. **subject-full-stop**
   - Prohibits a `subject` ending with a period.
   - `error` if not followed.
   - Examples: `echo "fix: some message."` fails, `echo "fix: some message"` passes.

7. **header-max-length**
   - Limits the `header` length to 100 characters.
   - `error` if not followed.
   - Examples: `echo "fix: some message that is way too long..."` fails, `echo "fix: some message"` passes.

8. **footer-leading-blank**
   - Requires a blank line at the beginning of the `footer`.
   - `warning` if not followed.
   - Examples: `echo "fix: some message\nBREAKING CHANGE: It will be significant"` warns.

9. **footer-max-line-length**
   - Limits the `footer` line length to 100 characters.
   - `error` if not followed.
   - Examples: `echo "fix: some message\nBREAKING CHANGE: footer too long..."` fails.

10. **body-leading-blank**
    - Requires a blank line at the beginning of the `body`.
    - `warning` if not followed.
    - Examples: `echo "fix: some message\nbody"` warns.

11. **body-max-line-length**
    - Limits the `body` line length to 100 characters.
    - `error` if not followed.
    - Examples: `echo "fix: some message\nbody too long..."` fails.

By adhering to these rules, your commits will not only conform to the Conventional Commits standards but also be easier to read and understand for anyone contributing to your project.
