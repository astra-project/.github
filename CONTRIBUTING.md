# Contributing to the ASTRA Project

Thank you for your interest in contributing to the **ASTRA Project**! We welcome contributions from everyone, whether it's reporting bugs, suggesting features, or contributing directly to the code base.

This document provides **general guidelines** for contributing to any repository in this organization. Individual projects may have additional or specific rules, so always check the project’s own `CONTRIBUTING.md` or `README.md` for further details.

---

## Code of Conduct

All participants are expected to follow our **[Code of Conduct](CODE_OF_CONDUCT.md)**. By participating, you agree to uphold this code. Please report unacceptable behavior to [lhparker@berkeley.edu](mailto:lhparker@berkeley.edu) or [francois.lanusse@cnrs.fr](mailto:francois.lanusse@cnrs.fr).

---

## How Can I Contribute?

### Reporting Bugs

- **Check existing issues**: Search the repository’s issues to ensure the bug hasn’t already been reported.
- **Use templates**: The repositories provide a bug report and documentation update templates. Use them to structure your issue report.

### Suggesting Enhancements

- **Use the template**: We provide a feature request template, explain the use case, the problem it solves, and any alternatives you’ve considered.
- **Tips for a better proposal**: Include examples, mockups, or references to similar features in other projects.

### Submitting Pull Requests

- **Fork the repository**: Create a fork and work on your changes in a dedicated branch and make sure your work is based off of `main`.
- **Write tests**: Add or update tests to cover your changes.
- **Update documentation**: Ensure all relevant documentation is up-to-date.
- **Keep commits atomic**: Each commit should represent a single logical change to facilitate review process.
- **Use draft until ready**: Keep a PR as a draft until ready, then convert it to ready for review. It will avoid triggering all the CI elements.
- **Reference issues**: Use keywords like `closes #123` or `fixes #456` to link your PR to the relevant issue.

**Review Process**: project maintainers will review PRs and issues on a best effort basis, and will engage with the authors to potentially request changes, as part of the collaborative work. Not all PRs will eventually be merged.

---

## DCO Sign-Off of Pull Requests

All contributions require a [Developer Certificate of Origin](https://developercertificate.org/) sign-off.
This certifies that you have the right to submit the code under the BSD 3-Clause license.

Sign-off happens at the **pull request level**, not per-commit. Here's how it works:

1. A reviewer approves your PR.
2. A bot posts a comment asking all PR contributors to sign the DCO.
3. Each contributor replies with the exact comment:

   > I have read the Developer Certificate of Origin and I hereby sign the DCO for this PR

4. Once all contributors have signed, the DCO check passes and the PR can be merged.

The bot tracks sign-off status in its comment and automatically adds `Signed-off-by`
trailers to the squash merge commit. If new commits are pushed after sign-off,
the signatures are invalidated and the PR must be re-approved and re-signed.
