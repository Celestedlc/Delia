# Delia

## Description

Delia is planned as an air-gapped two-factor authentication (2FA) token and cold storage suite featuring RAM-locked vaults, rot-shielded optical disc burning, acoustic FSK (Frequency-Shift Keying) data-over-audio transmission, and a zero-dependency ASCII text user interface (TUI).

Currently, this repository is in its initial setup stage. It provides the licensing configuration and a continuous integration workflow for automated documentation maintenance via the Google Gemini API.

## Architecture

The repository currently consists of CI/CD documentation automation components:

- **CI/CD Workflow (`.github/workflows/update-readme.yml`)**: An automated GitHub Actions pipeline.
  - **Triggers**: Executed on every push to the `main` branch or manually through `workflow_dispatch`.
  - **Integration**: Invokes the external reusable workflow `Celestedlc/github-workflows/.github/workflows/reusable-gemini-docs.yml@main`.
  - **Permissions**: Requires write access for repository contents and pull requests (`contents: write`, `pull-requests: write`).
- **License (`LICENSE`)**: Project licensed under the GNU General Public License v3.0 (GPL-3.0).

### Execution Flow

```text
[Push to main / workflow_dispatch]
              │
              ▼
   [update-readme.yml]
              │
              ▼
[Reusable Gemini Docs Workflow] ◄── (Secrets: GEMINI_API_KEY, WORKFLOW_REPO_TOKEN)
              │
              ▼
     [README.md Updated]
```

## Requirements

To run and maintain the repository workflows, the following credentials and environment settings are required:

- **GitHub Repository Secrets**:
  - `GEMINI_API_KEY` (Required): API key used by the Gemini documentation generator workflow.
  - `WORKFLOW_REPO_TOKEN` (Optional): Personal access token or custom workflow token if elevated repository access is required.
- **Git**: For version control and local repository management.

## Installation

1. Clone the repository:
   ```bash
   git clone https://github.com/Celestedlc/target-repo.git
   cd target-repo
   ```

2. Configure repository secrets in GitHub:
   - Navigate to **Settings** > **Secrets and variables** > **Actions** in your GitHub repository.
   - Add a repository secret named `GEMINI_API_KEY` containing your Google Gemini API key.
   - Optionally add `WORKFLOW_REPO_TOKEN` if required by custom permissions.

## Usage

### Automated Documentation Updates

The documentation update workflow is triggered automatically:
- **On Push**: Pushing new commits to the `main` branch initiates the README update job.
- **Manual Trigger**: 
  1. Open the repository on GitHub.
  2. Navigate to the **Actions** tab.
  3. Select the **Update README with Gemini** workflow.
  4. Click **Run workflow** on branch `main`.

## File Structure

```text
.
├── .github/
│   └── workflows/
│       └── update-readme.yml   # Workflow automating README updates using Gemini
├── LICENSE                     # GNU General Public License v3.0
└── README.md                   # Repository documentation
```
