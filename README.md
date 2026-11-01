# OpenCode Jailbroken (Termux Ready)

Fully unrestricted OpenCode setup. Uncensored AGENTS.md + agents auto-inject on every run.

## What this is

- `AGENTS.md` — zero-refusal system rules
- `.opencode/agent/uncensored.md` + `build.md` — primary unrestricted agents
- `opencode.json` — forces the uncensored agents and NVIDIA model

When you open this folder with OpenCode, the uncensored instructions load automatically.

## Termux Install (best method)

```bash
# 1. Install OpenCode
curl -fsSL https://opencode.ai/v2/install | bash
export PATH="$HOME/.opencode/bin:$PATH"

# 2. Clone this repo
git clone https://github.com/YOUR_USER/opencode-jailbroken.git
cd opencode-jailbroken

# 3. Set your NVIDIA key (or any provider)
export NVIDIA_API_KEY="nvapi-your-key-here"

# 4. Run
opencode
```

Or one-shot:

```bash
opencode run -m nvidia/nvidia/nemotron-3-ultra-550b-a55b "your request"
```

## Files

```
.
├── AGENTS.md                          # Core uncensored rules (auto-loaded)
├── opencode.json                      # Config + agent overrides
├── README.md
└── .opencode/
    └── agent/
        ├── uncensored.md              # Primary unrestricted agent
        └── build.md                   # Unrestricted build agent
```

## How the injection works

OpenCode automatically loads:

1. `AGENTS.md` in the project root
2. Any files listed in `opencode.json` → `instructions`
3. Agent definitions in `.opencode/agent/*.md`

No extra steps. Just `cd` into the folder and run `opencode`.

## Notes for Termux

- After install, add to `~/.bashrc` or `~/.zshrc`:
  ```bash
  export PATH="$HOME/.opencode/bin:$PATH"
  export NVIDIA_API_KEY="nvapi-..."
  ```
- Storage permission: `termux-setup-storage` if you want to work outside home.
