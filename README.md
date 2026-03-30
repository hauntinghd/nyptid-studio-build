# NYPTID Studio Build

This repository only exists to publish a deployable container image for the
private Studio source repository.

The image build workflow:

- clones `hauntinghd/studionyptixd` with a read-only deploy key
- checks out the `codex/render-studio-backend` branch
- builds the production Docker image from the private source tree
- publishes `ghcr.io/hauntinghd/nyptid-studio-api`
