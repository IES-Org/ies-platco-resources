# <img src="./assets/images/IES-logo-dark.png" alt="IES Logo" width="50" align="absmiddle"> IES Platform and Communications Team resources

**Repository:** `ies-platco-resources`  
**Description:** `This repository contains administrative material used by the IES Platform and Communications team to support automation workflows in the IES organisation.`

This repository contains administrative material used by the IES Platform and Communications team to support automation workflows in the IES organisation. It includes reusable GitHub Actions workflows and other resources to support the Platform and Communications team's technical needs and ensure consistency across IES repositories.

> This repository is public and forms part of the Information Exchange Standard initiative and is currently under the custodianship of the Department for Business, Innovation, Science and Trade (UK), acting on behalf of a cross-government group of stakeholders.

This code is licensed under the MIT License (see [LICENSE.md](LICENSE.md)).

**Note:** All documentation in this repository is licensed under the Open Government Licence v3.0 (OGL-3.0).

For full terms, see [OGL_LICENSE.md](OGL_LICENSE.md).

## Using the `synchronise-platco-workflows` GitHub Action

To use the `synchronise-platco-workflows` GitHub Action, a private GitHub application must be installed in your GitHub organisation. This is because the workflow requires `workflow:write` permissions to add content to the `.github/workflows` directory, which cannot currently be achieved using the [`GITHUB_TOKEN`](https://docs.github.com/en/actions/how-tos/writing-workflows/choosing-what-your-workflow-does/controlling-permissions-for-github_token) authorisation context.

Guidance on installing a GitHub application can be found here: [Installing your own GitHub App](https://docs.github.com/en/apps/using-github-apps/installing-your-own-github-app)

### Required GitHub App permissions

The GitHub application must have the following **repository permissions**:

1. `contents:read`  
2. `contents:write`  
3. `workflows:read`  
4. `workflows:write`

### Setting up secrets

Once your GitHub application has been created, the `synchronise-platco-workflows` action must be able to assume the identity of the application. To do this, two repository secrets are required:

- `IES_PLATCO_APP_CLIENT_ID`  
- `IES_PLATCO_APP_PRIVATE_KEY`

For ease of administration, these secrets can be set once as **organisation-level secrets**, with access delegated to trusted repositories, rather than adding them to each repository individually.

Guidance on managing organisation secrets is available here:  
[Creating and managing organisation secrets](https://docs.github.com/en/actions/security-guides/encrypted-secrets#creating-organization-secrets)

### Granting repository access

Assign repository access to your GitHub application for each trusted repository where you want to use the `synchronise-platco-workflows` workflow.

### Organisational repository ruleset

To trigger the `synchronise-platco-workflows` workflow when pull requests are made in repositories within your organisation, a [repository ruleset](https://docs.github.com/en/enterprise-cloud@latest/organizations/managing-organization-settings/creating-rulesets-for-repositories-in-your-organization) must be created with the following settings enabled:

- **Require workflows to pass before merging**  
- **Do not require workflows on creation**

The workflow configuration section of the ruleset should reference the `synchronise-platco-workflows` workflow found in the repository housing these assets.

Because the status check is marked as *required* at the organisation level, the workflow will be triggered automatically - unlike with standard repository rulesets.

## Features  

- **Workflow distribution solution**
    - [synchronise-platco-workflows.yml](./.github/workflows/synchronise-platco-workflows.yml) - this action can be used to distribute GitHub Actions across repositories in a GitHub organisation, using organisation-level repository rulesets.
- **Centralised Pull request labelling solution** - labels pull requests using the https://github.com/actions/labeler GitHub Action. A base configuration for use with GitFlow can be found at [labeler.yml](./.github/workflows/pull-request-labeler.yml).

## Pull Requests

Any proposed changes to the main branch must be navigated via a Pull Request, which has been enforced using branch protection policies. Pull requests must include the details in the [PULL_REQUEST_TEMPLATE.md](./.github/PULL_REQUEST_TEMPLATE.md) file.

## Acknowledgements

This repository has benefited from collaboration with various organisations. For a list of acknowledgments, see [ACKNOWLEDGEMENTS.md](ACKNOWLEDGEMENTS.md).

## Changelog

See [CHANGELOG.md](CHANGELOG.md) for a list of changes in each release.

## Contributions and Feedback

We welcome:

- Feedback and structured suggestions
- Bug reports and clarifications
- Requests for extensions or additional documentation

Please see:

- [CONTRIBUTING.md](CONTRIBUTING.md) for contribution guidelines
- [CODE_OF_CONDUCT.md](CODE_OF_CONDUCT.md) for expected behaviour and reporting concerns
- [MAINTAINERS.md](MAINTAINERS.md) for maintainer contact information

## Security and Responsible Disclosure

We take security seriously. If you believe you have found a security vulnerability in this repository, please follow our responsible disclosure process outlined in [SECURITY.md](SECURITY.md).

---

**Maintained as part of the Information Exchange Standard initiative.**

© Crown Copyright. This work forms part of the Information Exchange Standard initiative and is currently under the custodianship of the UK's Department for Business, Innovation, Science and Trade (BIST), acting on behalf of a cross-government group of stakeholders.
  
Licensed under the Open Government Licence v3.0.

For full licensing terms, see [OGL_LICENSE.md](OGL_LICENSE.md).