# IDE Python Environment

- [IDE Python Environment](#ide-python-environment)
  - [VSCode - Python formater plugins](#vscode---python-formater-plugins)
    - [Black](#black)
      - [Black - Installation](#black---installation)
      - [Black - pyproject.toml - Configuration](#black---pyprojecttoml---configuration)
      - [Black - VSCode - Configuration](#black---vscode---configuration)

## VSCode - Python formater plugins

### Black

Black provides a hassle-free and consistent code formatting solution for Python projects, enhancing readability, saving time on code reviews and discussions, and improving overall development workflow.

#### Black - Installation

```bash
pip install black
```

#### Black - pyproject.toml - Configuration

```toml
[tool.black]
line-length = 115
```

#### Black - VSCode - Configuration

Install [ms-python.black-formatter plugin](https://marketplace.visualstudio.com/items?itemName=ms-python.black-formatter): A Visual Studio Code extension with support for the black formatter.

Configure the project `.vscode/settings.json`

```json
{
    "[python]": {
        "editor.defaultFormatter": "ms-python.black-formatter",
        "editor.formatOnSave": true
    },
    "autoDocstring.customTemplatePath": "docstring_template_google.mustache",
}
```
