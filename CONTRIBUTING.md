# Contributing to Rarible Protocol

Thank you for investing your time towards contributing to the Rarible Protocol!

[docs.rarible.org](https://docs.rarible.org/) — documentation of Rarible Protocol.

## Getting Started

### Communication Channels

For open discussions, we encourage you to use [Discord](https://discord.gg/zqsZsEWBbN) and [Github Discussions](https://github.com/rarible/protocol/discussions) channels.

### Submitting an Issue

If you find a bug while working with the Rarible Protocol, you can help us by [submitting an issue here](https://github.com/rarible/protocol/issues). Please keep in mind that you can contribute to the protocol by submitting a pull request with the fix.

Before you submit an issue, please look through the history of closed issues/discussion since it's likely you will find out a fix or workaround for the problem you're encountering.

## Contributor Workflow

The codebase is maintained using the "contributor workflow" where everyone without exception contributes patch proposals using "pull requests" (PRs). This facilitates social contribution, easy testing, and peer review.

Before submitting your PR, search GitHub for an open or closed PR related to your submission. You don't want to duplicate effort.

**To contribute to Rarible Protocol:**

1. Fork the repository

   Fork the repository by clicking on the button on the right-top corner. This will create a copy of the repository in your account.
   
   ![image](https://user-images.githubusercontent.com/39627934/149868568-bf8a1700-f882-4039-b8a7-182d37c23d5d.png)

2. Clone the repository

   Clone the forked repository to your machine:

   ```shell
   git clone https://github.com/username/protocol.git
   ```

3. Create a branch

   ```shell
   cd protocol
   git checkout -b feature/your-new-branch-name
   ```

   Recommended branch types:

    * `feature/...` — for new features
    * `bugfix/...` — for bug fixes


4. Make necessary changes and commit them.

   ```shell
   git add example.md
   git commit -m "type: description"
   ```

   Where `type` is one of the following:

    * `feat` — a new feature
    * `fix` — a bug fix
    * `docs` — documentation


5. Push the changes to GitHub

   ```shell
   git push origin feature/your-new-branch-name
   ```

6. Create a pull request

   Go to the forked project and click a Compare & pull request. And after that, click Create pull request button. Your changes will be submitted for review. 

7. Keep an eye on the pull request

   There's a good chance we'll request a few changes to your pull requests once it's out, so keeping an eye on it will only make the merging process faster.
