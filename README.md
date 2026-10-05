# Versionlane runner releases

Reviewed customer-runner distributions only. The main source repository and control service remain private. Wheels contain the Python customer runner, shared contracts and reviewed Deepgram catalogue. No signing private key, credentials or customer artifacts are distributed.

## v0.1.0 — engineering preview

Supported: Python 3.11 on macOS/Linux, Git, Docker, one root requirements.txt with exact public PyPI pins, offline pytest tests. The only migration is the Versionlane-curated Deepgram Python SDK 6.1.1 → 7.0.0 three generated-type mappings. Deepgram is not a partner. There is no live provider pilot or customer-adoption claim.

Installation was checked in a fresh Linux arm64 container. GitHub-hosted amd64 onboarding and live authentication/campaign acceptance are pending. Installations do not grant reporting consent or GitHub access.

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
