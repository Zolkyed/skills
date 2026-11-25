# CLI tools for coding agents

## Search and edit

| Tool | What it does | Replaces |
|---|---|---|
| `rg` | Fast search of file contents | `grep` |
| `fd` | Find files by name or pattern | `find` |
| `ast-grep` | Search and rewrite code by syntax structure | `grep` for refactors |
| `sd` | Find and replace in files | `sed` |

## Data

| Tool | What it does | Replaces |
|---|---|---|
| `jq` | Process JSON | n/a |
| `yq` | Process YAML like `jq` does JSON | n/a |
| `xmlstarlet` | Query, edit and validate XML files | n/a |
| `sqlite3` | Query and inspect SQLite databases | n/a |

## Files and documents

| Tool | What it does | Replaces |
|---|---|---|
| `pandoc` | Convert documents between Markdown, HTML, docx, PDF and other formats | n/a |
| `7z` | Create and extract 7z, zip, tar and other archives | n/a |

## Runtimes and build tools

| Tool | What it does | Replaces |
|---|---|---|
| `dotnet` | Build, run and test C#, F# and other .NET projects | n/a |
| `node` | Run JavaScript and build Node.js projects | n/a |
| `bun` | Run JS/TS and install packages | `node` or `npm` |
| `python` | Run Python scripts and build Python projects | n/a |
| `uv` | Run Python scripts and manage Python versions, environments and packages | `pip` |
| `go` | Build, run and test Go projects | n/a |
| `cargo` | Build, run and test Rust projects | n/a |
| `javac` | Compile Java source code | n/a |
| `gcc` | Compile C and C++ code | n/a |
| `cmake` | Generate build files for C and C++ projects | n/a |
| `ninja` | Run builds that CMake generates | `make` |

## Dev workflow

| Tool | What it does | Replaces |
|---|---|---|
| `gh` | Repos, issues, PRs and branches from the shell | n/a |
| GNU `parallel` | Run shell tasks concurrently | n/a |

## AI coding agents

| Tool | What it does | Replaces |
|---|---|---|
| `claude` | Claude Code: run Anthropic's coding agent from the terminal. `-p` runs one prompt and exits, `--model` picks the model | n/a |
| `opencode` | Run the open-source OpenCode coding agent with many model providers. `run` runs one prompt and exits, `-m provider/model` picks the model | n/a |
| `copilot` | GitHub Copilot CLI: run GitHub's coding agent from the terminal. `-p` runs one prompt and exits, `--model` picks the model | n/a |

## IDE

| Tool | What it does | Replaces |
|---|---|---|
| `code` | VS Code CLI: open files at a line with `-g`, compare two files with `-d`, manage extensions with `--install-extension` and `--list-extensions` | n/a |
| `code chat` | Send a prompt to the Copilot chat panel in VS Code. `-m` picks the mode, `-a` adds a file | n/a |

## Linting and checks

| Tool | What it does | Replaces |
|---|---|---|
| `shellcheck` | Find mistakes in shell scripts | n/a |
| `actionlint` | Find mistakes in GitHub Actions workflow files | n/a |
| `yamllint` | Find syntax errors and style problems in YAML files | n/a |
| `hadolint` | Find mistakes and bad practice in Dockerfiles | n/a |
| `pre-commit` | Run linters and formatters on staged files before each commit | n/a |

## Cloud

| Tool | What it does | Replaces |
|---|---|---|
| `az` | Manage Azure resources, identities and subscriptions from the shell | n/a |
| `aws` | Manage AWS resources, identities and services from the shell | n/a |

## Infrastructure as code

| Tool | What it does | Replaces |
|---|---|---|
| `terraform` | Plan and apply cloud infrastructure from declarative config files | n/a |
| `ansible` | Configure servers and run tasks across many hosts over SSH | n/a |

## HTTP and TLS

| Tool | What it does | Replaces |
|---|---|---|
| `curl` | Make HTTP requests and test APIs from the shell | n/a |
| `wget` | Download files and mirror sites from the shell | n/a |
| `grpcurl` | Call gRPC services and list their methods from the shell | n/a |
| `openssl` | Inspect certificates, test TLS connections, generate keys and hashes | n/a |
| `mitmproxy` | Intercept, inspect and replay HTTP and HTTPS traffic from the command line | n/a |

## Network and DNS

| Tool | What it does | Replaces |
|---|---|---|
| `socat` | Connect and relay data between sockets, ports, files and processes | `nc` |
| `ss` | List open sockets and listening ports | `netstat` |
| `dig` | Query DNS records | `nslookup` |
| `nmap` | Scan hosts for open ports and running services | n/a |

## Packet capture

| Tool | What it does | Replaces |
|---|---|---|
| `tshark` | Capture and analyze network packets, the Wireshark CLI | n/a |
| `tcpdump` | Capture packets and print them to the terminal | n/a |

## Directory and authentication

| Tool | What it does | Replaces |
|---|---|---|
| `ldapsearch` | Query LDAP and Active Directory servers | n/a |
| `ldbsearch` | Query LDB databases, such as Samba's directory files | `ldapsearch` for local LDB files |
| `kinit` | Get a Kerberos ticket for a user or service | n/a |

## Android and instrumentation

| Tool | What it does | Replaces |
|---|---|---|
| `adb` | Talk to Android devices and emulators: install apps, read logs, run shell commands, forward ports | n/a |
| `frida` | Hook running processes to trace calls and change behavior | n/a |

## Browser and media

| Tool | What it does | Replaces |
|---|---|---|
| `playwright-cli` | Drive a real browser from the terminal: the Playwright MCP commands as a CLI | n/a |
| `ffmpeg` | Convert and process audio, video and images | n/a |
| `yt-dlp` | Download video, audio and subtitles from YouTube and other sites | n/a |
