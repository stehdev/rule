# Agent Guidelines for Rule Configuration Repository

## Overview

This repository is primarily a collection of proxy and routing configuration files for Mihomo, sing-box, Shadowrocket, and Zijian, plus supporting rule lists and helper scripts. Most files are templates or user-specific examples rather than application source code.

The repository is primarily in Chinese. Keep existing Chinese comments and user-facing wording unless the user explicitly asks for a rewrite.

Do not assume Python or Go tooling exists in the current working tree. Verify files and commands before referencing build or test steps.

## Repository Layout

- `config/mihomo/`: Mihomo/Clash Meta style YAML, INI, and related OpenClash/Nikki configuration files
- `config/singbox/`: sing-box JSON configs, versioned variants under `1.11.x/`, HomeProxy-style config, and helper shell scripts
- `config/shadowrocket/`: Shadowrocket `.conf` files
- `config/zijian/`: client and server YAML/JSON examples
- `proxy.list` and `direct.list`: supplemental routing rule lists
- `README.md`: short Chinese project note rather than full technical documentation

## Editing Priorities

- Preserve syntax and structure. Avoid broad reformatting unless the user asks for it.
- Preserve existing comments, placeholders, emoji labels, and quoted strings. Many policy names are referenced across multiple sections.
- When changing selectors, proxy groups, outbounds, rule-set tags, or policy names, update every matching reference consistently.
- Treat ports, LAN IPs, dashboard paths, subscription URLs, UUIDs, passwords, and API secrets as user-specific values. Do not replace them unless explicitly requested.
- If a file contains real-looking credentials or endpoints, avoid surfacing them in summaries unless necessary for the task.

## Format-Specific Guidance

### YAML and INI-style configs

- Keep indentation stable and avoid introducing anchors or advanced YAML features unless requested.
- Maintain current naming and comment style because these files are meant to be hand-edited by end users.

### JSON configs

- Preserve the existing shape and key naming when possible.
- After editing JSON, prefer a lightweight syntax check such as `python -m json.tool <file>` if validation is needed.

### UCI-style config files

- Files such as `config/mihomo/openclash`, `config/mihomo/nikki`, and `config/singbox/homeproxy` use section-and-option syntax. Preserve `config`, `option`, and `list` structure exactly.

### Rule list files

- Keep one rule per line.
- Preserve comments and the current matcher style such as `DOMAIN-SUFFIX`, `DOMAIN-KEYWORD`, and `IP-CIDR`.

## Validation Expectations

- There is no automated test suite in this repository.
- Prefer targeted syntax validation and consistency checks over runtime execution.
- For routing changes, sanity-check that referenced group names, outbounds, and rule-set labels still exist after the edit.
- Do not run service restart or reload scripts unless the user explicitly asks.

## Safety Notes

- `config/singbox/update-singbox.sh` is operational: it downloads config, kills an existing `sing-box` process, and starts it again. Treat it as a user-approved action only.
- Many files are environment-specific examples. Avoid changing local addresses, interface names, controller ports, or UI paths unless the request is explicit.
- The worktree may already contain user edits. Do not revert unrelated changes.

