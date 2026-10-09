Prepare this machine to run grackle, the scanner this bot drives. grackle is a single binary; it needs nothing else at runtime.

- `git` is installed and on PATH, so a GitHub URL can be cloned for auditing. Confirm with `git --version`.
- `grackle` is installed and on PATH. Install it one of these ways, then confirm with `grackle --version`:
  - Homebrew, on macOS or Linux: `brew install cpeoples/tap/grackle`.
  - With the Rust toolchain, on any OS: `cargo install --git https://github.com/cpeoples/grackle.git`, which places the binary on the cargo path.
  - Or download the archive for this platform from the project's releases page, extract it, and put `grackle` on PATH.
- grackle classifies its own rules correctly. Confirm with `grackle --self-test`, which should report that the rules pass.

Do not audit anything during setup. Preparing the machine is the whole job.
