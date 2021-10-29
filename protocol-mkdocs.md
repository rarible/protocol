# How to work with MkDocs

[docs.rarible.org](docs.rarible.org) is building with MkDocs and deploying to GitHub Pages. Documentation source files have been written in Markdown and configured with the `mkdocs.yml`.

[Requirements](https://www.mkdocs.org/user-guide/installation/#requirements) for work with MkDocs:

- Python
- pip

## Installation

1. Install [MkDocs](https://www.mkdocs.org/user-guide/installation/#installing-mkdocs):

    ```shell
    pip install mkdocs
    ```

2. Install [Material Theme](https://squidfunk.github.io/mkdocs-material/getting-started/#installation) for MkDocs:

    ```shell
    pip install mkdocs-material
    ```

## Usage

1. Clone the [repository with docs](https://github.com/rarible/protocol).
2. Switch to the required branch or create it.
3. Make changes, commit and push.
4. For checking the changes locally, run the command in the project directory:

    ```shell
    mkdocs serve
    ```

5. Open up `http://127.0.0.1:8000/` in your browser.

Changes in the documentation will be displayed immediately.

## Deploying

1. Run from the project directory:

    ```shell
    mkdocs gh-deploy
    ```

2. MkDocs send the commit and push to the `gh-pages` branch. The site will be updated within a few minutes.

You should never edit files in your pages repository by hand if you're using the `gh-deploy` command because you will lose your work the next time you run the command.

## Configuration

- [MkDocs documentation](https://www.mkdocs.org/user-guide/configuration/) for configurate settings.
- [Material documentation](https://squidfunk.github.io/mkdocs-material/setup/changing-the-colors/) for configurate theme and [extentions](https://squidfunk.github.io/mkdocs-material/setup/extensions/python-markdown/).
