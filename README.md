# Keptn GH Actions DevOps Collection

This repo contains shared GitHub Actions workflows that are used by multiple repos under the Keptn GitHub organization.

## Workflows

The following re-usable workflows are available:

| Name                    | Filename                      | Description | Inputs | Outputs |
|-------------------------|-------------------------------|-------------|--------|---------|
| DCO                     | `dco.yml`                     | Checks the [Developer Certificate of Origin](https://developercertificate.org/) on a PR or on a default branch. |`exclude-emails`: Comma-separated list of emails that should be ignored during DCO checks | None |
| Validate Semantic PR    | `validate-semantic-pr.yml`    | Checks for [Semantic PR messages](https://www.conventionalcommits.org/en/v1.0.0/) in order to enhance release note generation | `types`: List of types <br/>`scopes`: List of scopes | None |
| Pre-Release Integration | `pre-release-integration.yml` | Creates a pre-release of a Keptn integration | `PRERELEASE_KEYWORD`: Keyword for pre-releases, e.g., `alpha`, `next` | `RELEASE_TAG` |
| Release Integration     | `release-integration.yml`     | Creates a release of a Keptn integration | None | `RELEASE_TAG` |

## Actions

The following re-usable actions are available:

| Name                    | Filename                                     | Description                        | Inputs                    | Outputs     |
|-------------------------|----------------------------------------------|------------------------------------|---------------------------|-------------|
| Docker Build            | `actions/docker-build/action.yaml`           | Docker Login, Build and Push       | See [Docker Build Action](#docker-build-action) | -           |


### Docker Build Action


**Inputs**:
* `TAGS`: List of images/tags to be pushed, e.g., keptncontrib/my-service:1.2.3
* `BUILD_ARGS`: List of build arguments
* `REGISTRY_USER`: DockerHub User used for pushing to docker.io - leave empty if you don't want to push to docker.io
* `REGISTRY_PASSWORD`: DockerHub token or password used for pushing to docker.io - leave empty if you don't want to push to docker.io
* `GITHUB_TOKEN`: Github Access token used for pushing to ghcr.io - leave empty if you don't want to push to ghcr.io
* `DOCKERFILE`: Dockerfile to be used in docker build
* `TARGET`: Target to be built using docker build

**Outputs**:
* `BUILD_METADATA`: Docker build Metadata, see [Docker Build Push Action Docs](https://github.com/docker/build-push-action#outputs)


**Example Usage**:
```yaml
      - name: Docker Build
        id: docker_build
        uses: keptn/gh-automation/.github/actions/docker-build@v1
        with:
          TAGS: |
            ghcr.io/${{ github.repository_owner }}/${{ env.IMAGE }}:${{ env.VERSION }}
            ghcr.io/${{ github.repository_owner }}/${{ env.IMAGE }}:${{ env.VERSION }}.${{ env.DATETIME }}
            ${{ env.DOCKER_ORGANIZATION }}/${{ env.IMAGE_INITCONTAINER }}:${{ env.VERSION }}
            ${{ env.DOCKER_ORGANIZATION }}/${{ env.IMAGE_INITCONTAINER }}:${{ env.VERSION }}.${{ env.DATETIME }}
          BUILD_ARGS: |
            version=${{ env.VERSION }}
            datetime=${{ env.DATETIME }}
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
          REGISTRY_USER: ${{ secrets.REGISTRY_USER }}
          REGISTRY_PASSWORD: ${{ secrets.REGISTRY_PASSWORD }}
          DOCKERFILE: Dockerfile
```