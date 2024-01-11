# Ansible OctoPrint Role -  How to contribute

*ansible-octoprint* is a volunteer project and we appreciate any contribution, from fixing a grammar mistake in a comment to extending test coverage or implementing new functionality. Please read this section if you are contributing your work.

Being one of our contributors, you agree and confirm that:

* The work is all your own.
* Your work will be distributed under a BSD 2-Clause License once your pull request is merged.
* You submitted work fulfils or mostly fulfils our styles and standards.

Please help us keep our issue list small by adding fixes: #{$ISSUE_NO} to the commit message of pull requests that resolve open issues. GitHub will use this tag to auto close the issue when the PR is merged.

## Coding conventions

* This is open source software. Code should be as simple and transparent as possible. Favour clarity over brevity.
* The code should be compatible with Ansible >= 2.15.
* Commits should be [signed](https://docs.github.com/en/authentication/managing-commit-signature-verification/signing-commits).

## Testing

Please ensure your changes are tested on as wide a variety of target devices as possible, including where possible the latest versions of Debian, Ubuntu and Raspbian.

## Submitting changes

Please send a [GitHub Pull Request to Ansible-OctoPrint](https://github.com/loelkes/ansible-octoprint/pulls) with a clear list of what you've done (read more about [pull requests](https://docs.github.com/en/free-pro-team@latest/github/collaborating-with-issues-and-pull-requests/about-pull-requests)). Please follow our coding conventions (below) and make sure all of your commits are atomic (one feature per commit).

Please sign all commits - see [Signing GitHub Commits](https://docs.github.com/en/authentication/managing-commit-signature-verification/signing-commits) for instructions.

Always write a clear log message for your commits. One-line messages are fine for small changes, but bigger changes should look like this:

    $ git commit -m "A brief summary of the commit
    > 
    > A paragraph describing what changed and its impact."


Thanks