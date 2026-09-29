## Student AI Tooling Onboarding Handout

Welcome to the course! To streamline your development workflow, minimize environment setup troubleshooting, and provide you with industry-standard assistance, we are standardizing on a robust, free AI developer stack.

This stack is divided into two parts: Turnkey Autocomplete for passive line-by-line coding assistance, and The OpenCode Harness for active, agentic task execution and debugging.

Follow the instructions below to activate your free student benefits and configure your environment.

------------------------------

## Part 1: Turnkey Autocomplete & Inline Chat

For continuous keystroke autocompletions (ghost text) and direct file-level queries, you will use [GitHub Copilot](https://github.com/orgs/community/discussions/203821). If you are waiting on your academic verification, use [Codeium / Windsurf](https://chromewebstore.google.com/detail/windsurf-plugin-ai-code-a/hobjkcpmjhlegmobgonaagepfckjkceh) as your instant fallback.

## 🚀 Activating GitHub Copilot for Students

Verified students get GitHub Copilot for free through the GitHub Student Developer Pack.

   1. Visit the [GitHub Student Developer Pack](https://dev.to/chrisachinga/github-students-developer-pack-by-github-education-1d0d) page.
   2. Click Sign up for student benefits and log in with your primary GitHub account.
   3. Submit your official school email address (@.edu) and upload your student ID or proof of current enrollment if prompted.
   4. Once verified, open your code editor (e.g., VS Code), install the official GitHub Copilot extension, and sign in via your verified GitHub account.

## ⚡ Quick Fallback: Codeium / Windsurf

If your GitHub verification is delayed and you need immediate autocomplete capabilities for upcoming assignments:

   1. Download and install the Codeium or Windsurf extension from your IDE marketplace.
   2. Create a free individual account (no school verification required).
   3. Leave it running silently in your editor background to provide inline suggestions as you type.

------------------------------

## Part 2: Autonomous Multi-File Agents & The CLI

When you need to handle deep codebase debugging, refactor multiple files at once, run compiler test suites automatically, or execute system commands safely, you will use [OpenCode](https://ai.sulat.com/the-definitive-guide-to-opencode-from-first-install-to-production-workflows-aae1e95855fb).
OpenCode operates locally via an interactive terminal interface (TUI) or an IDE side-panel, serving as the execution harness for your high-powered model subscriptions and free API keys.

## 🔑 Setting Up Your Free Cloud Engines

## 1. Google AI Studio & Google Antigravity
Google offers student-accessible tiers powered by their latest reasoning architectures (Gemini Flash & Pro).

* For the IDE & CLI Environment: Authenticate the native Google Antigravity tool suite using your primary Google account. This gives you baseline agentic access to file structures and terminal actions.
* For Custom API Access: Visit [Google AI Studio](https://www.udemy.com/course/create-epic-movie-scenes-with-gemini-google-ai-studio-p1/), log in, and click Create API Key. This key provides up to 1,500 free requests per day and a massive 1-million-token context window—perfect for parsing heavy codebase folders or documentation packs.

## 2. Groq Cloud (The Speed King)

Groq provides completely free API keys for open-source models (like Llama and Gemma) that process data at hundreds of tokens per second.

   1. Go to the [Groq Cloud Console](https://dev.to/paweljanda/building-ai-powered-net-applications-with-groq-cloud-and-mainnet-2o6d).
   2. Create a free developer account and navigate to API Keys.
   3. Generate a new key and save it securely.
   4. Important Configuration Note: When routing an open API key to a sidebar panel, ensure automatic keystroke ghost-text is disabled to prevent hitting request-per-minute rate limits.

------------------------------

## Part 3: Configuration & Workspace Guardrails

[OpenCode](https://opencode-tutorial.com/en/faq) unifies your keys under a single interface, tracks your workspace state via a local database, and creates automated Git checkpoints before letting an AI modify files. If a model generates broken code, you can easily roll back your state.

## 🛠️ Global Configuration File

Create or update your global OpenCode configuration file (typically located at ~/.config/opencode/opencode.json or managed via your system dotfiles). Paste the structure below, substituting your environment variables or direct keys:

```JSON
{
  "providers": {
    "google_oauth": {
      "enabled": true,
      "default_model": "gemini-3.8-flash"
    },
    "google_ai_studio": {
      "api_key": "${ENV.GOOGLE_AI_STUDIO_KEY}",
      "models": ["gemini-2.5-flash"]
    },
    "groq": {
      "api_key": "${ENV.GROQ_API_KEY}",
      "models": ["llama-3.3-70b-specdec", "gemma-2-9b-it"]
    }
  }
}
```

## 💻 Essential Terminal Commands

OpenCode standardizes your development commands inside the CLI shell. Open your terminal in your project directory and use the following interaction loop:

* opencode init: Initializes OpenCode within your active project workspace directory.
* /context [filename]: Ingests specific files, directory structures, or compiler error logs into the active memory window.
* /model: Opens an interactive drop-down list to instantly swap backends (e.g., switching from a fast Groq model to a high-capacity Google AI Studio model).
* /shell [command]: Safely tests your project by allowing the agent to run your test suite or compiler with an interactive checkpoint.
* /undo: Instantly rolls back the last file-system modification executed by the agent, returning your workspace to its exact prior state.

------------------------------

If you run into any authentication hurdles or need help binding your API path variables inside your Fish or Bash shell profiles, please bring your device to office hours or post your environment logs to the class discussion board!
