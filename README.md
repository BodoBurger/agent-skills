# Agent Skills

Reusable skills for Codex that provide focused instructions for software-engineering work.

## Installation

For skills that should be available in every repository, clone this repository into your user-level skills directory.

### Windows (PowerShell)

```powershell
New-Item -ItemType Directory -Force "$HOME\.agents" | Out-Null
git clone https://github.com/BodoBurger/agent-skills.git "$HOME\.agents\skills"
```

This normally resolves to `C:\Users\<username>\.agents\skills`.

### Linux

```bash
mkdir -p "$HOME/.agents"
git clone https://github.com/BodoBurger/agent-skills.git "$HOME/.agents/skills"
```

This normally resolves to `/home/<username>/.agents/skills`.

If the repository is already installed, update it with:

```bash
git -C "$HOME/.agents/skills" pull
```

Codex detects installed skills automatically. If newly installed or updated skills do not appear, restart Codex.

## Usage

Codex can use a skill in two ways:

- **Explicitly:** mention it in your prompt with `$skill-name`, for example `$disciplined-coding`. In the Codex CLI or IDE extension, `/skills` shows the available skills.
- **Implicitly:** describe a task that matches the skill's purpose. Codex may select the relevant skill automatically unless the skill disables implicit invocation.

Example prompts:

```text
$disciplined-coding fix the failing validation test with the smallest reasonable change.
```

```text
$hard-cut replace the legacy configuration format and remove the old runtime fallback.
```

## Included skills

| Skill | Description |
| --- | --- |
| [`creative-coding`](./creative-coding/) | Builds and evolves software with creative autonomy, sensible assumptions, and useful complementary features. Runs only when explicitly invoked with `$creative-coding`. |
| [`disciplined-coding`](./disciplined-coding/) | Keeps implementation and review work simple, surgical, assumption-aware, and tied to verifiable success criteria. |
| [`hard-cut`](./hard-cut/) | Enforces one canonical implementation when new behavior replaces old behavior, removing obsolete compatibility and fallback paths unless a verified contract requires them. Runs only when explicitly invoked with `$hard-cut`. |
