# Versionlane reviewed runner distributions

[Current early engineering release: v0.2.0](https://github.com/1xollie/versionlane-releases/releases/tag/v0.2.0).

# Versionlane runner 0.2.0 — early engineering release

Customer migration software for reviewed, bounded Python SDK upgrades. This release
is supported by controlled engineering tests, including fresh hosted Linux
installation and restricted Docker verification of the exact candidate. These
tests are not customer adoption, provider endorsement or a production availability
commitment.

Supported migrations:

- Deepgram Python **6.1.1 → 7.0.0**: three reviewed generated-type import/binding mappings.
- Stripe Python **12.5.1 → 13.0.0**: four reviewed exception imports only. Other
  Stripe SDK client, resource and payment/API usage blocks the whole upgrade.
  Exception checks do not verify payment behavior or the changed default API version.

Both examples are Versionlane-curated. Neither provider is a claimed partner.

Requirements: Python 3.11; one root `requirements.txt` with the exact baseline SDK
pin; configured Python source paths; bounded offline pytest; supported restricted
Docker execution. No lockfiles, monorepos, additional languages or arbitrary plugins.
Dependency acquisition is separate from secret-free, network-free test execution.

`assess` reports eligibility without running customer code. `run --authorize`
produces review artifacts without changing the checkout; `--verify` separately
authorizes baseline and candidate tests. Unsupported usages, failing tests,
incompatible packages and stale evidence stop safely. Verification is bounded,
not general behavioral equivalence or a production guarantee.

Execution and detailed artifacts remain customer-owned. PR publication is explicit,
creates a draft, preserves stale-base/human-edit protections and requires maintainer
review. Ordinary repository CI is separate and may need explicit maintainer dispatch.
There is no automatic merge. Reporting remains optional with separate link consent;
provider receipts are bounded customer-reported metadata, not independent attestation.

Install into a fresh environment using the included installer and the separately
reviewed wheel/requirements SHA-256 pins. The installer validates HTTPS downloads
and hashes before binary-only dependency installation. Historical v0.1.0 assets and
schema-one signed packages remain unchanged. Schema-two Stripe requires runner 0.2.0;
v0.1.0 rejects it. This release contains no control-service source or customer data.

## Install current release

```sh
curl --fail --location --proto '=https' --proto-redir '=https' 'https://github.com/1xollie/versionlane-releases/releases/download/v0.2.0/install_runner.py' --output install_runner.py
python3.11 -I -c "import hashlib,pathlib; assert hashlib.sha256(pathlib.Path('install_runner.py').read_bytes()).hexdigest() == 'f8d34e2fb95353531da9bba5d36be024fac5c4dde0b3809937f27456ceac2b30'"
python3.11 -I install_runner.py \
  --wheel-url 'https://github.com/1xollie/versionlane-releases/releases/download/v0.2.0/versionlane_runner-0.2.0-py3-none-any.whl' \
  --wheel-sha '09c5a8defcc42ab13972d83e1ad4b485716e05c56d63aa6531f7c250c3ebbeff' \
  --requirements-url 'https://github.com/1xollie/versionlane-releases/releases/download/v0.2.0/runner-requirements.txt' \
  --requirements-sha 'c5cd40659d70665166f97f5f3e35f9e63d7a038e47cbeeaa0ea5be231ad3405c' \
  --destination ./versionlane-0.2.0
./versionlane-0.2.0/bin/python -I -m versionlane --help
```

Fresh public installation passed on macOS and GitHub-hosted Ubuntu 24.04/Python 3.11.13. Both supported migrations passed restricted Docker verification; deliberately blocked and failed cases stopped safely. These are controlled engineering tests. No independent onboarding or adoption is claimed.

## Historical v0.1.0 documentation (retained)

The following text records the original release state. Its pending live gates are historical, not a statement of current application status. v0.1.0 asset bytes are unchanged.

# Versionlane runner releases

Reviewed customer-runner distributions only. The main source repository and control service remain private. Wheels contain the Python customer runner, shared contracts and reviewed Deepgram catalogue. No signing private key, credentials or customer artifacts are distributed.

## v0.1.0 — engineering preview

Supported: Python 3.11 on macOS/Linux, Git, Docker, one root requirements.txt with exact public PyPI pins, offline pytest tests. The only migration is the Versionlane-curated Deepgram Python SDK 6.1.1 → 7.0.0 three generated-type mappings. Deepgram is not a partner. There is no live provider pilot or customer-adoption claim.

Fresh installation passed on macOS arm64, Linux arm64 and GitHub-hosted Ubuntu 24.04 amd64. The GitHub run also passed restricted Docker verification (seven independent SDK checks and one customer test in each baseline/candidate environment). This was builder-performed controlled development verification; live authentication, campaign-to-PR acceptance and independent customer onboarding remain pending. Installations do not grant reporting consent or GitHub access.

## Verify and install

Use an empty directory outside your customer repository. Review the installer before running it. Python 3.11, Git and a working Docker daemon are prerequisites; the installer does not install system tools.

```sh
curl --fail --location --proto '=https' --proto-redir '=https' 'https://github.com/1xollie/versionlane-releases/releases/download/v0.1.0/install_runner.py' --output install_runner.py
python3.11 -I -c "import hashlib,pathlib; assert hashlib.sha256(pathlib.Path('install_runner.py').read_bytes()).hexdigest() == 'f8d34e2fb95353531da9bba5d36be024fac5c4dde0b3809937f27456ceac2b30'"
python3.11 -I install_runner.py \
  --wheel-url 'https://github.com/1xollie/versionlane-releases/releases/download/v0.1.0/versionlane_runner-0.1.0-py3-none-any.whl' \
  --wheel-sha '11be7da53c9659f728531a18307c50a10e9b34b5f2dfe2e1c52d5dcf6eabf3ee' \
  --requirements-url 'https://github.com/1xollie/versionlane-releases/releases/download/v0.1.0/runner-requirements.txt' \
  --requirements-sha 'c5cd40659d70665166f97f5f3e35f9e63d7a038e47cbeeaa0ea5be231ad3405c' \
  --destination ./versionlane-0.1.0
./versionlane-0.1.0/bin/python -I -m versionlane --help
```

The installer validates both downloaded assets before creating a virtual environment; dependencies require exact hashes and binary wheels. Existing environments are never overwritten. Pin these hashes in reviewed customer instructions; downloading hashes from the same location alone is not an independent trust decision.

For a published campaign, accept its invitation, choose reporting/link permissions, save the one-time token outside Git, and commit its exact versionlane.toml. Set VERSIONLANE_BASE_URL to the real HTTPS campaign service. Preview with inspect, explicitly run verify, review changes.patch and separate fixture/customer test results, then opt into apply or publish-pr. Never provide reporting or GitHub write credentials to verification jobs. No staging service URL is advertised until deployed and verified.

No autonomous merge, customer-code hosting, arbitrary provider plugins, lockfile support or general coding-agent behavior. A provider receipt contains aggregate customer-reported metadata only. A draft PR does not prove downstream CI ran.

The immutable v0.1.0 release.json contains `published: false` because it records the build before upload. Publication is established by the GitHub release record; existing asset bytes and checksums are preserved. Future manifests distinguish build metadata from publication state.
