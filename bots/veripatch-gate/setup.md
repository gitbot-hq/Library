# VeriPatch Gate setup

Prepare the machine before reviewing a dependency fix. Do not run a scan or verification as part of setup.

## 1. Install Node.js and npm

Install Node.js 20 or newer from the official [Node.js download page](https://nodejs.org/en/download). Confirm both commands work:

```bash
node --version
npm --version
```

## 2. Install Docker

VeriPatch runs dependency verification inside a Docker sandbox. Install Docker for your operating system using the official instructions:

- [Docker Desktop for Windows](https://docs.docker.com/desktop/setup/install/windows-install/) (use the WSL 2 backend where applicable)
- [Docker Desktop for Mac](https://docs.docker.com/desktop/setup/install/mac-install/)
- [Docker Engine for Linux](https://docs.docker.com/engine/install/)

Start Docker Desktop or the Docker Engine service, then confirm the CLI can reach the daemon:

```bash
docker --version
docker info
```

If `docker info` fails, Docker is not ready yet. Resolve that first; do not try to install or modify system components without asking the user.

## 3. Install the VeriPatch CLI

This setup refers specifically to **VeriPatch**, the npm vulnerability-remediation verifier maintained at [amarjaleelbanbhan/VeriPatch](https://github.com/amarjaleelbanbhan/VeriPatch). It is not another project with a similar name.

Install the published CLI package:

```bash
npm install --global veripatch
veripatch --version
veripatch doctor
```

The doctor command checks the local environment, including Node.js, Docker, lockfile and network readiness. If the CLI is missing or a prerequisite check fails, explain the issue and ask before installing software or changing the environment.

## Setup boundary

Preparing the machine is the whole job. Do not scan a project, run verification, modify files, or produce a verdict during setup. VeriPatch verification can execute project build and test commands inside its Docker sandbox, so obtain explicit user approval before starting it.
