# **Rektor: Software Supply Chain Security Toolkit**

[![CD](https://github.com/jackhax/supply-chain-security/actions/workflows/cd.yml/badge.svg)](https://github.com/jackhax/supply-chain-security/actions/workflows/cd.yml)
[![Scorecard OSSF](https://github.com/jackhax/supply-chain-security/actions/workflows/scorecard.yml/badge.svg)](https://github.com/jackhax/supply-chain-security/actions/workflows/scorecard.yml)
[![OpenSSF Best Practices](https://www.bestpractices.dev/projects/9778/badge)](https://www.bestpractices.dev/projects/9778)

---

## Overview
Rektor is a comprehensive toolkit designed to enhance the security and integrity of your software supply chain. It provides automated solutions for artifact signing, verification, dependency management, code quality enforcement, SBOM generation, and CI/CD integration. Rektor helps organizations meet modern software security standards and best practices with minimal friction.

---

## Key Features
- **Artifact Signing & Verification**: Sign artifacts with Sigstore's `cosign` and verify signatures using Rekor transparency logs.
- **Transparency & Auditability**: Fetch and verify inclusion and consistency proofs from transparency logs for full traceability.
- **Code Quality & Security**: Enforce code formatting, linting, type checking, and static application security testing using industry-standard tools.
- **Dependency Management**: Manage Python dependencies and project configuration with Poetry.
- **SBOM Generation & Attestation**: Automatically generate CycloneDX SBOMs and create cryptographic attestations for your releases.
- **Automated CI/CD**: Integrate with GitHub Actions for continuous integration, deployment, and security checks.
- **Secret Scanning**: Prevent and detect secrets leakage with pre-commit hooks and automated scanning.
- **Comprehensive Testing**: Ensure high code quality and coverage with pytest and coverage reporting.

---

## Getting Started
1. **Install Rektor**
   - Install from PyPI:
     ```sh
     pip install rektor
     ```
   - Or clone and install locally:
     ```sh
     git clone https://github.com/jackhax/supply-chain-security.git
     cd supply-chain-security
     poetry install
     ```

2. **Sign and Verify Artifacts**
   - Use `cosign` to sign your artifacts and upload signatures to Rekor.
   - Use Rektor's Python API to fetch and verify signatures, certificates, and inclusion proofs.

3. **Generate and Attest SBOMs**
   - Generate a CycloneDX SBOM with `cyclonedx-py`:
     ```sh
     cyclonedx-py -o cyclonedx-sbom.json
     ```
   - Attest the SBOM using `cosign`:
     ```sh
     cosign attest --predicate cyclonedx-sbom.json --type cyclonedx rektor-*.whl
     ```

4. **Automate with CI/CD**
   - Integrate the provided GitHub Actions workflows for automated testing, security checks, SBOM generation, and artifact attestation.

---

## Usage

### Command-Line Interface (CLI)

You can run Rektor directly from the command line:

```sh
python -m rektor.main [OPTIONS]
```

**Examples:**
- Verify artifact inclusion in Rekor log:
  ```sh
  python -m rektor.main --inclusion <log_index> --artifact <artifact_filepath>
  ```
- Fetch the latest checkpoint:
  ```sh
  python -m rektor.main --checkpoint
  ```
- Verify consistency between checkpoints:
  ```sh
  python -m rektor.main --consistency --tree-id <tree_id> --tree-size <tree_size> --root-hash <root_hash>
  ```
- Enable debug mode:
  ```sh
  python -m rektor.main --debug ...
  ```

### Python API Usage

You can import and use Rektor's functions in your own Python scripts:

```python
from rektor.main import inclusion, consistency, get_latest_checkpoint

# Example: Verify inclusion
inclusion(log_index=12345, artifact_filepath="artifact.md")
```

### As a Package Entry Point

If installed as a package, you can also run:

```sh
python -m rektor
```
This will invoke the CLI defined in `rektor/__main__.py`.

---

## Project Structure
```
rektor/
├── __init__.py
├── __main__.py
├── main.py
├── merkle_proof.py
├── util.py

tests/
├── test_main.py
├── ...

pyproject.toml
README.md
LICENSE
```

---

## Tools and Technologies
- **Programming Language**: Python
- **Version Control**: Git (GitHub)
- **Signing Tool**: Sigstore (`cosign`)
- **Transparency Log**: Rekor
- **Static Analysis**: Black, Ruff, Flake8, Pylint, mypy, Bandit
- **Dependency Management**: Poetry
- **SBOM**: CycloneDX (`cyclonedx-py`)
- **Testing**: pytest, pytest-cov
- **Secret Scanning**: trufflehog, pre-commit

---

## Security and Best Practices
- All code changes require pull requests and branch protection.
- Automated secret scanning and static analysis in CI.
- High test coverage and code quality enforced.
- Security policies and contribution guidelines included.

---

## Badges
- Build status, OpenSSF Scorecard, and Best Practices badges are displayed above to reflect the security and reliability of this project.

---

## License
This project is licensed under the terms of the LICENSE file in this repository.

---

## Contact & Support
For questions, issues, or contributions, please open an issue or pull request on GitHub.

