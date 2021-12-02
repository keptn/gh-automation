# Keptn GH Actions DevOps Collection

This repo contains shared GitHub Actions workflows that are used by multiple repos under the Keptn GitHub organization.

## Workflows
| Name                    | Filename                      | Description | Inputs | Outputs |
|-------------------------|-------------------------------|-------------|--------|---------|
| DCO                     | `dco.yml`                     | Checks the [Developer Certificate of Origin](https://developercertificate.org/) on a PR or on a default branch. |`exclude-emails`: Comma-separated list of emails that should be ignored during DCO checks | None |
| Validate Semantic PR    | `validate-semantic-pr.yml`    | Checks for [Semantic PR messages](https://www.conventionalcommits.org/en/v1.0.0/) in order to enhance release note generation | `types`: List of types <br/>`scopes`: List of scopes | None |
| Pre-Release Integration | `pre-release-integration.yml` | Creates a pre-release of a Keptn integration | `PRERELEASE_KEYWORD`: Keyword for pre-releases, e.g., `alpha`, `next` | `RELEASE_TAG` |
| Release Integration     | `release-integration.yml`     | Creates a release of a Keptn integration | None | `RELEASE_TAG` |
