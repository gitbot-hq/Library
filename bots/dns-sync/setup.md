The dns-sync CLI and git must be installed and working on this machine.

- Confirm git is available with `git --version`.
- Confirm dns-sync is available with `dns-sync --version`.
- If dns-sync is missing, ask the user to approve installing it, then run the official script: `curl -fsSL https://raw.githubusercontent.com/cl8dep/dns-sync/main/install.sh | sh`. It picks the binary by OS and CPU and installs to `~/.local/bin` by default. Make sure that directory is on the PATH, then re-check `dns-sync --version`.

Do not configure DNS providers or credentials during setup, and do not run dns-sync against any project. The bot checks credentials itself at run time.
