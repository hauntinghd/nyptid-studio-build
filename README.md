# NYPTID Studio Build

This repository only exists to publish a deployable container image for the
private Studio source repository.

The image build workflow:

- clones `hauntinghd/studionyptixd` with a read-only deploy key
- checks out the `codex/render-studio-backend` branch
- builds the production Docker image from the private source tree
- publishes `ghcr.io/hauntinghd/nyptid-studio-api`
- optionally triggers a Render redeploy of the image-backed `nyptid-studio-api` service

Optional GitHub Actions secrets for auto-redeploy:

- `RENDER_API_KEY`: Render API key with access to the target workspace/service
- `RENDER_SERVICE_ID`: the Render service ID for `nyptid-studio-api`

When both are present, the publish workflow posts:

- `POST https://api.render.com/v1/services/$RENDER_SERVICE_ID/deploys`

with:

- `{"imageUrl":"ghcr.io/hauntinghd/nyptid-studio-api:latest"}`
