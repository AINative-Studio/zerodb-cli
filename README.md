# ZeroDB Local CLI

Command-line interface for managing ZeroDB Local environment and syncing with ZeroDB Cloud.

> **Looking for the full ZeroDB Local runtime?** See [zerodb-local](https://github.com/AINative-Studio/zerodb-local) — the standalone Python package with lite mode (SQLite + FAISS, no Docker) and full mode (PostgreSQL + Qdrant + MinIO).

## Installation

```bash
pip install zerodb-cli
```

Or install the full runtime (includes the CLI):

```bash
pip install zerodb-local
zerodb serve
```

## Quick Start

### 1. Start Local Environment

```bash
zerodb local up
```

### 2. Login to Cloud

```bash
zerodb cloud login --email your@email.com
```

### 3. Link Project

```bash
zerodb cloud link <project-id>
```

### 4. Sync Data

```bash
# Generate sync plan
zerodb sync plan

# Apply sync (with confirmation)
zerodb sync apply

# Push to cloud (shorthand)
zerodb sync push

# Pull from cloud (shorthand)
zerodb sync pull
```

## Commands

### Sync Commands

- `zerodb sync plan` - Generate and display sync plan
  - `--schema` - Show schema diff only
  - `--data` - Show data diff only
  - `--vectors` - Show vector diff only
  - `--json` - Output as JSON

- `zerodb sync apply` - Execute sync plan
  - `--yes` - Skip confirmation
  - `--dry-run` - Preview without executing
  - `--strategy` - Conflict resolution strategy (local-wins, cloud-wins, newest-wins, manual)

- `zerodb sync push` - Push local changes to cloud
  - `--yes` - Skip confirmation
  - `--force` - Force push, overwriting cloud data

- `zerodb sync pull` - Pull cloud changes to local
  - `--yes` - Skip confirmation

### Local Environment Commands

- `zerodb local init` - Initialize local environment (create data directories)
- `zerodb local up` - Start all services (docker-compose up -d)
  - `--logs` - Show logs instead of detaching
- `zerodb local down` - Stop all services
  - `--volumes` - Also remove volumes
- `zerodb local status` - Show service status and health
- `zerodb local logs [service]` - View service logs
  - `--no-follow` - Don't follow logs
- `zerodb local restart [--service NAME]` - Restart services
- `zerodb local reset` - Reset environment (removes all data)
  - `--yes` - Skip confirmation prompt

### Cloud Commands

- `zerodb cloud login` - Login to ZeroDB Cloud
- `zerodb cloud logout` - Logout from ZeroDB Cloud
- `zerodb cloud whoami` - Show current user
- `zerodb cloud link <project-id>` - Link to cloud project
- `zerodb cloud unlink` - Unlink current project

### Environment Commands

- `zerodb env list` - List all environments
- `zerodb env switch <env>` - Switch environment
- `zerodb env current` - Show current environment

### Inspect Commands

- `zerodb inspect schema` - Show local schema tree
- `zerodb inspect vectors` - Vector namespace summary
- `zerodb inspect events` - Event lag and offsets
- `zerodb inspect sync-state` - Last sync time and status

## Features

### Conflict Resolution

When conflicts are detected during sync, you can choose how to resolve them:

- **local-wins** - Always use local version
- **cloud-wins** - Always use cloud version
- **newest-wins** - Use the version with the latest timestamp
- **manual** - Interactively choose for each conflict

### Configuration

Configuration is stored in `~/.zerodb/`:

- `config.json` - CLI configuration
- `credentials.json` - Cloud credentials (JWT tokens)

## Related

- [zerodb-local](https://github.com/AINative-Studio/zerodb-local) — full standalone runtime (lite + full modes, Tauri desktop)
- [ZeroDB Cloud](https://zerodb.ai) — managed cloud service
- [Documentation](https://docs.ainative.studio/zerodb-local)

## Support

- **Email**: hello@ainative.studio
- **Website**: https://www.ainative.studio

## License

MIT License - Copyright (c) 2025 AINative Studio
