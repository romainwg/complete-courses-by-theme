# Conventional Comments Writing Tutorial

<!-- https://conventionalcomments.org/ -->

Conventional Comments provide a structured way to give feedback during reviews, using specific labels to clarify the intention behind each comment. Here's a simple guide to help you use them effectively.

- [Conventional Comments Writing Tutorial](#conventional-comments-writing-tutorial)
  - [1. Understanding the Format](#1-understanding-the-format)
  - [2. Using Labels](#2-using-labels)
  - [3. Adding Decorations](#3-adding-decorations)
  - [4. Providing Discussion](#4-providing-discussion)
  - [5. Best Practices](#5-best-practices)

---

## 1. Understanding the Format

A Conventional Comment follows this format:

```text
<label> [decorations]: <subject>
[discussion]
```

- **Label**: Indicates the type of comment.
- **Decorations**: (Optional) Provides additional context.
- **Subject**: The main message of the comment.
- **Discussion**: (Optional) Additional details or justification.

---

## 2. Using Labels

Here are some commonly used labels:

- **praise**: To compliment something.
- **nitpick**: For a minor detail or personal preference.
- **suggestion**: To propose an improvement.
- **issue**: To report a problem.
- **question**: To ask a question or seek clarification.
- **todo**: To indicate a small task to be completed.

**Examples**:

```text
praise: Great work on this function!
nitpick: Could you align these variables for better readability?
suggestion: Using a for loop here could make the code cleaner.
issue: This method might cause a memory leak.
question: Why did we choose this approach over another?
todo: Add comments to clarify this section.
```

---

## 3. Adding Decorations

Decorations provide additional context. Here are some common decorations:

- **(non-blocking)**: The comment should not prevent approval.
- **(blocking)**: The comment needs to be resolved before approval.

**Examples**:

```text
suggestion (non-blocking): Maybe we could add an animation here?
issue (blocking): This function doesn't check inputs, which could lead to bugs.
```

---

## 4. Providing Discussion

The discussion section is where you can add details, justification, or steps to resolve the comment.

**Example**:

```text
suggestion: Using a for loop here could make the code cleaner.
It would be more efficient and facilitate long-term maintenance.
```

---

## 5. Best Practices

- **Be Constructive**: Aim to assist, not to criticize.
- **Be Clear**: Ensure your comment is understandable.
- **Use "We" Instead of "You"**: This creates a sense of collaboration.
- **Balance Positive and Negative Feedback**: Try to find positive points to mention.

---

By following this guide, you'll be able to provide clear, constructive, and understandable feedback, making the review process more efficient and enjoyable for everyone.
