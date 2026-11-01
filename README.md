# OpenCode Jailbroken (Termux Ready)

Fully unrestricted OpenCode setup. Uncensored `AGENTS.md` + agents auto-inject on every run.

Works with **any model** once OpenCode is running.

## Best method for Termux (proot Ubuntu)

Official OpenCode binary is glibc-linked and fails on pure Termux (`cannot execute: required file not found`).  
Use proot-distro + Ubuntu — this is the most reliable way.

```bash
# 1. Install proot-distro
pkg update && pkg install proot-distro -y

# 2. Install Ubuntu
proot-distro install ubuntu

# 3. Enter Ubuntu
proot-distro login ubuntu

# 4. Inside Ubuntu – install OpenCode
apt update && apt install -y curl git
curl -fsSL https://opencode.ai/v2/install | bash
export PATH="$HOME/.opencode/bin:$PATH"
opencode --version

# 5. Clone this jailbroken pack
git clone https://github.com/bageltrade/opencode-jailbroken.git
cd opencode-jailbroken

# 6. Set your API key (NVIDIA example)
export NVIDIA_API_KEY="nvapi-your-key-here"

# 7. Run – uncensored AGENTS.md injects automatically
opencode
```

One-shot:

```bash
opencode run -m nvidia/nvidia/nemotron-3-ultra-550b-a55b "your request"
```

Make the key permanent inside Ubuntu:

```bash
echo 'export NVIDIA_API_KEY="nvapi-your-key-here"' >> ~/.bashrc
echo 'export PATH="$HOME/.opencode/bin:$PATH"' >> ~/.bashrc
source ~/.bashrc
```

## Alternative – pure Termux native builds

If you prefer no proot, use a community bionic build:

```bash
rm -rf ~/.opencode
curl -fsSL https://raw.githubusercontent.com/Thr45hx/opencode-termux-native/main/install.sh | bash
# or
curl -fsSL https://github.com/Spectra010s/opencode-termux/raw/v2.0.28/install.sh | sh
```

Then clone this repo and run the same way.

## What this pack does

- `AGENTS.md` — zero-refusal system rules (auto-loaded)
- `.opencode/agent/uncensored.md` + `build.md` — primary unrestricted agents
- `opencode.json` — forces the uncensored agents + model

OpenCode automatically loads:

1. `AGENTS.md` in the project root  
2. Files listed in `opencode.json` → `instructions`  
3. Agent definitions in `.opencode/agent/*.md`

No extra steps. Just `cd` into the folder and run `opencode`.

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

## Notes

- Works with any provider/model once OpenCode is running (NVIDIA, OpenAI, Anthropic, free models, etc.)
- The uncensored rules override refusals and moralizing
- Keep your API keys in environment variables, never hard-code them in the repo
