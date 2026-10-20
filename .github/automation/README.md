# Upstream automation policy

- Daily and manual source sync follows `Huxpro/huxblog-boilerplate:master` into `sync-only/upstream-master`. It does not build or publish.
- Local workflows and maintenance policy are retained; conflicting upstream changes stop rather than force-push.
- Existing historical tags and releases are never recreated or overwritten. Baseline deployment does not backfill releases.
- No recognized new upstream formal release means no automatic heavyweight build or publication. A source commit, website rebuild, tag alone, or dependency update is not a release signal.
- Manual build and promotion remain separate where the repository has a real deliverable. Repositories without a build/publisher do not gain a fabricated release route.
- Lightweight read-only safety checks remain enabled. This policy does not enable third-party dispatch, credentials, external AI, or repository security settings.
- Website repositories sync into a non-publishing source branch. Publication requires an explicit manual promotion of verified build artifacts; no automatic merge into the live Pages source.

## Manual website operations

Run `jekyll-gh-pages.yml` on the default branch with the full source commit (including a reviewed source-sync commit). This builds only and retains `site-candidate` for 30 days. Record the run ID, source SHA and artifact.tar SHA256 from the summary. Run `site-promote.yml` separately with those exact identities to deploy the same bytes without rebuilding. Existing Pages source/environment protections remain authoritative; this change does not alter their settings. Expired or inconsistent artifacts are rejected, not silently rebuilt.

Pages promotion first reads the existing configuration and refuses to deploy unless its build type is already `workflow`. It never enables Pages, changes its source, or creates credentials.
