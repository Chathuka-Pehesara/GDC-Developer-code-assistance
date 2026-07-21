# Workshop ADK

Sample agents built with the [Google Agent Development Kit (ADK)](https://google.github.io/adk-docs/) for a workshop on building LLM agents.

## Prerequisites

- Python 3.13+
- [uv](https://docs.astral.sh/uv/) for dependency management
- A Google API key with access to Gemini models

## Setup

1. Install dependencies:

   ```bash
   uv sync
   ```

2. Add your API key to `.env` in the project root:

   ```bash
   GOOGLE_API_KEY=your-api-key-here
   ```

## Running an agent

Each agent lives in its own folder with an `agent.py` exposing a `root_agent`. From the project root, run:

```bash
# Interactive terminal chat with a specific agent
uv run adk run weather_agent

# Browser-based UI (http://localhost:8000) with a dropdown to pick any agent
uv run adk web
```

## Agents in this repo

- **`weather_agent/`** — a single agent with a mock `get_weather` tool. Good starting example for tools + instructions.
- **`code_agent/`** — a `SequentialAgent` pipeline (`CodeWriterAgent` → `CodeReviewerAgent` → `CodeRefactorerAgent`) that writes, reviews, and refactors Python code.

## Standalone scripts

- **`weather_agent_starter.py`** — exercise skeleton for wiring up a `Runner` + `InMemorySessionService` around `weather_agent` by hand (fill in the `TODO`s).
- **`weather_agent_completed.py`** — the completed version of the same script.

Run either directly with:

```bash
uv run python weather_agent_completed.py
```

## PR Review Bot Demo

This repository includes an AI PR Review Bot built for the buildathon. It uses the `pr_review_agent` to fetch a GitHub Pull Request diff and post a code review comment using Gemini.

### Setup

1. Copy `.env.example` to `.env`.
2. Add your `GOOGLE_API_KEY`.
3. Add a `GITHUB_TOKEN` (a Personal Access Token with repo access).

### Running the Demo

To run a review against a real GitHub PR, use the included CLI script:

```bash
uv run python review_pr.py --repo <owner/repo_name> --pr <pr_number>
```

Example:

```bash
uv run python review_pr.py --repo tsuresh/workshop_adk --pr 1
```

The script will fetch the diff, analyze it for bugs, security risks, and code smells, and post a review comment back to the PR.
