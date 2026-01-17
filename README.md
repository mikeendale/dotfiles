# dotfiles

Personal configuration files for development environments.

## Contents

| File | Description |
|------|-------------|
| `.vimrc` | Vim configuration with Vundle plugin management |
| `.claude/settings.json` | Claude Code permission settings |

## Installation

### Vim

1. Clone this repository:
   ```bash
   git clone https://github.com/mikeendale/dotfiles.git ~/dotfiles
   ```

2. Symlink the vim configuration:
   ```bash
   ln -s ~/dotfiles/.vimrc ~/.vimrc
   ```

3. Install Vundle (plugin manager):
   ```bash
   git clone https://github.com/VundleVim/Vundle.vim.git ~/.vim/bundle/Vundle.vim
   ```

4. Install plugins:
   ```bash
   vim +PluginInstall +qall
   ```

### Claude Code

Copy or symlink the Claude Code settings:

```bash
# Option 1: Use as project-level settings (recommended)
cp -r ~/dotfiles/.claude /path/to/your/project/

# Option 2: Use as user-level settings (applies globally)
mkdir -p ~/.claude
ln -s ~/dotfiles/.claude/settings.json ~/.claude/settings.json
```

## Vim Configuration

### Plugins (via Vundle)

- **[NERDTree](https://github.com/scrooloose/nerdtree)** - File system explorer
- **[vim-markdown](https://github.com/plasticboy/vim-markdown)** - Markdown syntax and features
- **[vim-javascript](https://github.com/pangloss/vim-javascript)** - JavaScript syntax
- **[vim-jsx](https://github.com/mxw/vim-jsx)** - JSX syntax support
- **[typescript-vim](https://github.com/leafgarland/typescript-vim)** - TypeScript syntax
- **[python-syntax](https://github.com/hdima/python-syntax)** - Enhanced Python syntax
- **[vim-twig](https://github.com/evidens/vim-twig)** - Twig template syntax
- **[Tabular](https://github.com/godlygeek/tabular)** - Text alignment
- **[vim-abolish](https://github.com/tpope/vim-abolish)** - Case-preserving substitution
- **[MatchTag](https://github.com/gregsexton/MatchTag)** - HTML tag matching
- **[Jenkinsfile-vim-syntax](https://github.com/martinda/Jenkinsfile-vim-syntax)** - Jenkinsfile syntax

### Key Mappings

| Key | Action |
|-----|--------|
| `F5` | Enable paste mode |
| `F6` | Disable paste mode |
| `,,` | Remove trailing whitespace |

### Settings

- 2-space indentation (spaces, not tabs)
- Dark background color scheme
- Case-insensitive search
- Natural split behavior (below and right)
- Drupal file type detection (`.module`, `.theme`, `.install`, etc.)

## Claude Code Settings

The `.claude/settings.json` provides fine-tuned permissions for [Claude Code](https://docs.anthropic.com/en/docs/claude-code).

### Philosophy

- **Permissive by default** - Standard mode prompts on first use
- **Explicit deny list** - Dangerous commands are blocked outright
- **Ask for risky ops** - Destructive but sometimes-needed commands require confirmation

### Blocked Commands (deny)

| Category | Examples |
|----------|----------|
| Destructive deletion | `rm -rf`, `rm -r`, `shred` |
| Git dangerous ops | `git reset --hard`, `git push --force`, `git rebase` |
| Privilege escalation | `sudo`, `su`, `doas` |
| System/disk ops | `dd`, `mkfs`, `fdisk`, `mount` |
| Cloud CLI | `aws`, `gcloud`, `az`, `terraform destroy` |
| Package publishing | `npm publish`, `pip upload`, `cargo publish` |
| Secrets access | `.env*`, `~/.aws/**`, `~/.ssh/id_*`, `*.pem` |

### Auto-Approved Commands (allow)

| Category | Examples |
|----------|----------|
| Node.js | `npm run`, `npm test`, `npx`, `yarn`, `pnpm` |
| Python | `python`, `pytest`, `poetry`, `ruff`, `black` |
| Git (safe) | `status`, `diff`, `log`, `add`, `commit`, `branch` |
| Shell utilities | `ls`, `cat`, `grep`, `find`, `sed`, `awk`, `jq` |
| Build tools | `make`, `cargo`, `go`, `tsc`, `vite` |

### Commands Requiring Confirmation (ask)

- File operations: `rm` (single), `mv`, `cp -r`
- Network: `curl`, `wget`, `ssh`, `scp`, `rsync`
- Git push operations
- Docker runtime commands
- Config file edits (`package.json`, `Dockerfile`, etc.)

## License

MIT
