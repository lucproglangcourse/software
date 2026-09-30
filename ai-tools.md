# Student AI Tooling Onboarding Handout

Welcome to the course! Modern software engineering increasingly means working *alongside* AI assistants. Rather than a single all-in-one tool, we use a **three-tiered stack** that layers tools by the depth and autonomy of the task at hand. Each tier builds on the one before it, and you will use all three throughout the semester.

| Tier | Tool | Best For |
|------|------|----------|
| 1 | **GitHub Copilot** | Passive autocomplete and inline chat as you type |
| 2 | **Antigravity (`agy`)** | Conversational agentic sessions with deep codebase context |
| 3 | **Cline** | Autonomous multi-file execution with full human-in-the-loop control |

> **Quick mental model:** Copilot whispers suggestions in your ear; `agy` is a pair programmer you can have a conversation with; Cline is a junior developer you assign a complete task to and supervise.

---

## Part 1 — Tier 1: GitHub Copilot (Passive Autocomplete & Inline Chat)

GitHub Copilot is your always-on coding companion. It generates ghost-text completions as you type and answers targeted questions about the code in your current file. Because it operates inline and never touches your file system autonomously, it is the safest and lowest-friction tier.

### 1.1 Free Student Access

Verified students receive GitHub Copilot at no cost through the **GitHub Student Developer Pack**.

1. Visit [github.com/settings/education/benefits](https://github.com/settings/education/benefits) and click **Start an application**.
2. Sign in with your primary GitHub account and submit your `.edu` email address. Upload a student ID or enrollment letter if prompted.
3. Approval typically takes a few minutes to a few days.
4. Once approved, go to [github.com/education/benefits](https://github.com/education/benefits), scroll to **All offers → GitHub Copilot**, and click **Claim offer**.
   > If you had a prior trial or subscription, cancel it first to avoid billing conflicts.

### 1.2 VS Code Setup

1. Open VS Code and press `Ctrl+Shift+X` (or `Cmd+Shift+X` on macOS) to open the Extensions view.
2. Search for **GitHub Copilot** (publisher: GitHub) and install it. Also install **GitHub Copilot Chat**.
3. A sign-in prompt appears — sign in with the **same GitHub account** you used for the Student Developer Pack.
4. Restart VS Code to ensure the extension fully syncs with your student entitlement.

> **Status check:** Look for the Copilot icon in the VS Code status bar (bottom right). A check mark means it is active. If it shows a warning, wait 24–48 hours for GitHub's systems to sync, then sign out and back in.

### 1.3 Other IDEs

Copilot extensions are also available for **JetBrains IDEs** (IntelliJ, PyCharm, CLion, etc.) via the JetBrains marketplace, and for **Neovim**, **Vim**, and **Azure Data Studio**. The authentication flow is identical — sign in with your verified GitHub account.

### 1.4 Key Interactions

| Action | How |
|--------|-----|
| Accept ghost-text suggestion | `Tab` |
| Dismiss suggestion | `Esc` |
| Accept word by word | `Ctrl+→` / `Cmd+→` |
| Cycle through alternative suggestions | `Alt+]` / `Alt+[` |
| Open inline chat | `Ctrl+I` / `Cmd+I` |
| Open Copilot Chat panel | Click the chat icon in the activity bar |

### 1.5 Effective Prompting Tips

- **Write a comment first.** A comment like `// Parse ISO 8601 date string and return a Python datetime object` gives Copilot a clear target before it generates code.
- **Keep related code visible.** Copilot uses open editor tabs as context. Split-screen the file you are implementing and the interface or test it must satisfy.
- **Use inline chat for localized edits.** Select a block, press `Ctrl+I`, and type "add error handling" or "convert to list comprehension." This is faster than rewriting manually.
- **Use Copilot Chat for explanations.** Ask `/explain` on an unfamiliar function or `/fix` on a compiler error in the Chat panel.

### 1.6 Instant Fallback: Codeium / Windsurf

If your GitHub student verification is delayed, install the **Codeium** or **Windsurf** extension from the VS Code marketplace. Create a free individual account (no school verification needed) and you get immediate inline suggestions while you wait for Copilot to activate. Remove it once Copilot is running to avoid conflicts.

---

## Part 2 — Tier 2: Google Antigravity / `agy` (Conversational Agentic Sessions)

**Google Antigravity** (brand name) runs on the same underlying engine as Gemini. It is available as:

- **Antigravity IDE** — a standalone VS Code-based editor with deep AI integration built in.
- **`agy` CLI** — a terminal-based interactive agent (TUI) you can run anywhere.
- **VS Code Extension** — installs the Antigravity side panel inside your existing VS Code.

Unlike Copilot, `agy` can read your entire project tree, run terminal commands, search the web, and iterate on multi-step plans — but it still works *conversationally* and asks for your approval before making changes. It is free with a Google account (generous daily limits on Gemini Flash and Pro).

### 2.1 VS Code Extension Setup (Recommended Starting Point)

1. In VS Code, open the Extensions view (`Ctrl+Shift+X` / `Cmd+Shift+X`).
2. Search for **Google Antigravity** (publisher: Google) and click **Install**.
3. An Antigravity icon appears in the Activity Bar. Click it.
4. Follow the sign-in prompts using your **Google account**. The extension handles the local backend setup automatically on first launch.

The side panel gives you:

- **Sidebar Chat** — conversational Q&A and planning with your codebase in context.
- **Agent Mode** — the agent reads/writes files, runs build/test commands, and searches the web, showing you a plan before executing.
- **Planning Mode** — review and refine a step-by-step plan before the agent touches anything.
- **Inline Code Lenses** — clickable "Refactor / Write Tests / Explain" buttons that appear directly above your classes and functions.
- **Visual Diff Overlays** — inline red/green diffs let you accept or reject each proposed edit in place.
- **Diagnostic Auto-Fix** — click a compiler error or lint warning in the Problems pane and the agent generates and applies a fix.

> **Autocomplete inside Antigravity IDE:** If you use the standalone Antigravity IDE instead of VS Code, the **Antigravity Tab** feature provides context-aware ghost-text completions (including supercomplete for larger diffs), Tab-to-Jump for cursor navigation, and Tab-to-Import for automatic import management.

### 2.2 `agy` CLI Setup

The CLI is ideal for terminal-first workflows, SSH sessions, and scripting. It shares the same agent harness as the IDE extension.

**Install (macOS / Linux):**
```bash
curl -fsSL https://antigravity.google/cli/install.sh | bash
```

**Install (Windows PowerShell):**
```powershell
irm https://antigravity.google/cli/install.ps1 | iex
```

After installation, make sure `agy` is on your `PATH` (the installer usually handles this; restart your shell if needed). Then:

```bash
agy          # start an interactive session in the current directory
agy --help   # list all flags and subcommands
```

**First run:** `agy` walks you through a one-time Google account authentication. After that, launching `agy` in any project directory immediately gives the agent full context of your workspace.

### 2.3 Essential `agy` CLI Interactions

Once inside the `agy` TUI session:

| Command | What it does |
|---------|--------------|
| `/help` | List all available slash commands |
| `/model` | Switch the active model (e.g., Gemini Flash → Gemini Pro) |
| `/context <file>` | Explicitly add a file or directory to the active context window |
| `/plan` | Ask the agent to produce a numbered plan before acting |
| `/clear` | Clear conversation history and reset context |
| `/exit` or `Ctrl+D Ctrl+D` | End the session |

**Configuration file:** `~/.gemini/antigravity-cli/settings.json` — edit this to set your default model, preferred behaviors, and MCP tool integrations.

### 2.4 Using `agy` Inside the VS Code Terminal

You do not need a separate window. Open the integrated terminal in VS Code (`Ctrl+\`` / `Cmd+\``), `cd` into your project, and run `agy`. The TUI runs inside VS Code just like any other CLI tool, letting you keep your editor and agent session side by side.

### 2.5 Other IDEs

The `agy` CLI works identically in any IDE's integrated terminal (JetBrains, Zed, Neovim). The Antigravity IDE extension is currently VS Code-based; for JetBrains users, the CLI is the primary path.

### 2.6 Effective Prompting Tips

- **Start with context.** Open a session and say "here is the project structure" and paste or `/context` the relevant directories before asking a question.
- **Use planning mode.** For any task touching more than one file, ask `agy` to plan first: "Before changing anything, give me a numbered plan." Review it, then say "proceed."
- **Be specific about scope.** "Refactor the authentication module to use bcrypt" is better than "make the login more secure."
- **Iterate in the same session.** `agy` maintains conversation history. Follow up with "now add unit tests for that" or "the build is still failing — here is the new error."

---

## Part 3 — Tier 3: Cline (Autonomous Multi-File Agent with Checkpoints)

**Cline** (originally "Claude Dev") is an open-source autonomous coding agent. Unlike `agy`, which is conversational, Cline executes complete multi-step tasks — creating files, editing code across your entire project, running test suites, and even driving a headless browser — and only pauses at each action to ask for your **explicit approval**. This human-in-the-loop checkpoint model makes it powerful but safe.

Cline uses a **Bring Your Own Key (BYOK)** model: you connect it to whichever AI provider you prefer (Anthropic Claude, Google Gemini, OpenAI, etc.), and you pay inference costs directly. Many providers offer free tiers sufficient for coursework.

### 3.1 VS Code Extension Setup

1. In VS Code, open the Extensions view.
2. Search for **Cline** (publisher: Cline) and click **Install**.
3. A Cline icon appears in the Activity Bar. Click it to open the Cline side panel.
4. Click the **gear / settings icon** inside the Cline panel to open API settings.
5. Select your preferred **AI Provider** from the dropdown (Anthropic, Google Gemini, OpenAI, Ollama for local models, etc.).
6. Paste your API key for that provider.
7. Choose your default model (e.g., `claude-sonnet-4-5`, `gemini-2.5-flash`).

> **Free API option:** Google's Gemini API via [Google AI Studio](https://aistudio.google.com) provides free daily quotas (1,500 requests/day for Gemini Flash) and a massive context window — enough for most assignments. Generate a free key at AI Studio, then select **Google Gemini** as your Cline provider.

### 3.2 Other IDEs and Platforms

Cline runs in:
- **JetBrains IDEs** (IntelliJ, PyCharm, etc.) — via the JetBrains Marketplace.
- **Cursor** and **Windsurf** — native integrations.
- **Zed** and **Neovim** — community plugins.

### 3.3 Cline CLI Setup

For terminal-only environments or scripting, install the Cline SDK via npm:

```bash
npm install -g @cline/sdk
cline --help
```

This gives you the same autonomous agent runtime in scripts, cron jobs, and CI/CD pipelines. Configuration (API keys, model preferences) are shared with the VS Code extension via a common config file.

### 3.4 Key Concepts and Modes

#### Plan Mode vs. Act Mode

Cline separates strategy from execution:

- **Plan Mode** — Cline thinks through the task, researches the codebase, and produces a detailed plan. No files are touched. Review and approve the plan.
- **Act Mode** — Cline executes the plan step by step. Before every significant action (writing a file, running a shell command, making a network request), it shows you a diff or command and waits for your **Approve** or **Reject**.

Always run Plan Mode first on any complex task.

#### Checkpoints

Cline automatically creates **workspace checkpoints** (backed by Git snapshots) before making changes. If generated code breaks your build:

1. Open the Cline panel.
2. Click **Checkpoints** and select the snapshot to restore.
3. Cline resets your workspace to that exact state.

> This makes it safe to let Cline attempt ambitious refactors — you can always roll back to a known-good state.

#### `.clinerules`

Create a `.clinerules` file in your project root to give Cline standing instructions it must follow in every session:

```
- All Python functions must have type annotations and docstrings.
- Never modify files in the tests/ directory without asking first.
- Always run `pytest` after making code changes.
- Keep line length to 88 characters (Black formatter standard).
```

This is especially useful for enforcing course coding standards automatically.

### 3.5 Essential Cline Interactions (VS Code)

| Action | How |
|--------|-----|
| Start a new task | Type in the Cline chat panel and press Enter |
| Approve a proposed file change | Click **Approve** in the diff view |
| Reject a proposed change | Click **Reject** (Cline will try an alternative) |
| Pause mid-task | Click **Pause** |
| Restore a checkpoint | Click **Checkpoints** → select snapshot |
| Switch models mid-task | Click the model name in the Cline header |

### 3.6 Effective Task Descriptions for Cline

Cline works best when you give it a **complete, unambiguous task description** upfront:

- ❌ "Fix the bug."
- ✅ "The function `parse_date()` in `src/utils.py` raises a `ValueError` when the input string is `None`. Add a guard clause that returns `None` instead, and add a test case for this in `tests/test_utils.py`. Run `pytest` to confirm everything passes."

Include:
- **Which file(s)** are involved.
- **What the current behavior is** and **what the correct behavior should be**.
- **How success should be verified** (e.g., tests pass, the app runs, a specific output appears).

### 3.7 Model Selection and Cost Tips

| Provider | Free Tier | Notes |
|----------|-----------|-------|
| Google Gemini (via AI Studio) | 1,500 req/day (Flash) | Best free option; huge context window |
| Anthropic Claude | Limited free trial | Strong code quality on Claude Sonnet |
| OpenAI | Paid only (no free tier) | GPT-4o available if you have credits |
| Ollama (local) | Unlimited, free | Requires a GPU; latency varies |

For coursework, **Gemini Flash via AI Studio** covers the vast majority of tasks for free. Switch to a stronger model (Gemini Pro, Claude Sonnet) when you need deeper reasoning on a hard problem.

---

## Putting It All Together: The Daily Workflow

Here is how the three tiers work together in a typical coding session:

```
1. Write new code       →  Copilot ghost-text completes line-by-line as you type.
2. Understand a module  →  Ask agy: "Explain how the auth flow works in this codebase."
3. Plan a feature       →  Ask agy to produce a numbered plan; review it with you.
4. Implement a feature  →  Hand the approved plan to Cline in Act Mode; approve each step.
5. Hit a tricky bug     →  Ask Copilot Chat /fix, or bring agy in for a deeper conversation.
6. Refactor a subsystem →  Assign to Cline with a .clinerules constraint and checkpoints on.
```

| Situation | Reach for |
|-----------|-----------|
| Completing a line or small block | Copilot (ghost-text) |
| Explaining an error message | Copilot Chat or `agy` |
| "How does X work in this codebase?" | `agy` |
| Writing tests for an existing function | `agy` or Cline |
| Implementing a full feature across multiple files | Cline (Plan then Act) |
| Refactoring with rollback safety | Cline (with Checkpoints) |
| Working over SSH / no GUI | `agy` CLI or `cline` CLI |

---

## Quick-Reference: CLIs Side by Side

For students who prefer terminal-first workflows or are working on a remote server, both Tier 2 and Tier 3 have full CLI support:

| | `agy` (Antigravity CLI) | `cline` (Cline CLI) |
|--|------------------------|---------------------|
| **Install** | `curl -fsSL https://antigravity.google/cli/install.sh \| bash` | `npm install -g @cline/sdk` |
| **Launch** | `agy` | `cline` |
| **Auth** | Google account (prompted on first run) | API key in config or env var |
| **Style** | Conversational TUI (chat-based) | Task-oriented (plan → approve → execute) |
| **Config** | `~/.gemini/antigravity-cli/settings.json` | Shared with VS Code extension config |
| **Get help** | `agy --help` / `/help` inside TUI | `cline --help` |
| **Exit** | `/exit` or `Ctrl+D Ctrl+D` | `Ctrl+C` |

Both CLIs work in any terminal: your laptop shell, VS Code's integrated terminal, a JetBrains terminal, an SSH session, or a CI runner.

---

## Troubleshooting & Support

| Problem | Fix |
|---------|-----|
| Copilot not activating after claim | Wait 24–48 h; sign out and back in in VS Code |
| `agy` not found after install | Restart your shell; check that `~/.local/bin` is on your `PATH` |
| Cline API errors | Verify the key is pasted correctly; check your provider's dashboard for quota |
| Cline broke my code | Use **Checkpoints** in the Cline panel to restore the last known-good state |
| `agy` gives outdated information | Run `/clear` to reset context; provide fresh file excerpts |

If you run into authentication issues or environment configuration problems (PATH variables, shell profiles), bring your device to **office hours** or post your error output to the **class discussion board**.

---

*Handout prepared for CS 371 — subject to revision as tools evolve.*
