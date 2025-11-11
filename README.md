The Lyrical Master Protocol (LMP) — Release Package

This document bundles everything needed to publish the LMP as an open, auditable, deterministic, and free standard. It contains:

README.md (formal spec + quick start)

lmp_reference.py (deterministic reference engine)

Dockerfile (reproducible environment)

.github/workflows/ci.yml (CI to run unit tests and publish artifact)

leaderboard-schema.json (public leaderboard schema)

SIGNED_SAMPLE_OUTPUT.json (example signed score output template)

README.md (compact release-ready)

# The Lyrical Master Protocol (LMP) **Canonical Final Draft — Architect's Mandate** **Purpose.** A free public standard to objectively quantify lyrical & musical craft across genres, designed to surface literary lyricists and to be reproducible, auditable, and network-effect friendly. **License.** MIT (free for all artists, researchers, and platforms). This keeps the program free and public by design. ## Quick formula (human summary) Let T, P, I ∈ [0,100] and B ∈ [1, B_max]. S = B * (0.5*T + 0.4*P + 0.1*I) Phenom: S ≥ 95.0 ## How to run (quick start) 1. Clone this repo. 2. Build the Docker image: `docker build -t lmp:canonical .` 3. Run sample scoring: `docker run --rm lmp:canonical python lmp_reference.py` ## Governance & Reproducibility - All official runs publish: raw input, tokens, feature vectors, T/P/I breakdown, B, S, git commit, docker digest. - Changes to primitive definitions require a new major version. ## Contact & adoption - Public leaderboard and sample submissions are encouraged. Use `leaderboard-schema.json` for standard submission/response format. 

Dockerfile (minimal reproducible environment)

# Dockerfile FROM python:3.10-slim WORKDIR /app COPY lmp_reference.py /app/lmp_reference.py # pin any future deps here CMD ["python","lmp_reference.py"] 

.github/workflows/ci.yml (CI pipeline)

name: LMP CI on: push: branches: [ main, master ] pull_request: branches: [ main, master ] jobs: test-and-publish: runs-on: ubuntu-latest steps: - uses: actions/checkout@v4 - name: Set up Python uses: actions/setup-python@v4 with: python-version: '3.10' - name: Install dependencies run: | python -m pip install --upgrade pip - name: Run unit tests run: | python lmp_reference.py - name: Build Docker image run: | docker build -t lmp:canonical . - name: Publish artifact run: | echo "Publish step (optional): attach signed artifacts to release or run a reproducibility job." 

leaderboard-schema.json (public schema)

{ "$schema": "http://json-schema.org/draft-07/schema#", "title": "LMP Score Submission", "type": "object", "properties": { "submission_id": {"type": "string"}, "artist_name": {"type": "string"}, "city_of_origin": {"type": "string"}, "lyrics_excerpt": {"type": "string"}, "T": {"type": "number"}, "P": {"type": "number"}, "I": {"type": "number"}, "B": {"type": "number"}, "S": {"type": "number"}, "status": {"type": "string"}, "commit_hash": {"type": "string"}, "docker_digest": {"type": "string"}, "signed_by": {"type": "string"}, "signature": {"type": "string"} }, "required": ["submission_id","artist_name","lyrics_excerpt","T","P","I","B","S","commit_hash","docker_digest"] } 

SIGNED_SAMPLE_OUTPUT.json (example)

{ "submission_id": "0001", "artist_name": "The Architect", "city_of_origin": "Philadelphia, PA", "lyrics_excerpt": "The Architect builds the standard...", "T": 97.8, "P": 95.6, "I": 96.2, "B": 1.03, "S": 97.8, "status": "Certified Phenom", "commit_hash": "<git-commit-hash>", "docker_digest": "<docker-image-sha256>", "signed_by": "LMP Executive Node", "signature": "<digital-signature>" } 

Next recommended actions

Create repo (if not already) and paste these files.

Add MIT LICENSE (keeps it free for all).

Run CI and publish Docker digest with every release.

Publish a simple web page with an "Analyze your verse" form that calls the canonical engine (signed results + leaderboard ingestion).

End of release package.
