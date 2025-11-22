# RNS FileSync

P2P file synchronization with delta sync over Reticulum. Only changed blocks are transmitted making it bandwidth efficient.

## Installation

```bash
pip install rns --break-system-packages
# or 
pipx install rns
```

```bash
git clone https://github.com/Sudo-Ivan/RNS-Filesync.git
cd RNS-Filesync
```

## Usage

Start syncing:

```bash
python rns_filesync.py -d ~/shared # or whatever directory you want to sync
```

Connect to peer:

```bash
python rns_filesync.py -d ~/shared -p <peer_destination_hash>
```

## Options

```
-d PATH              Directory to sync (required)
-i NAME              Identity name
-p HASH              Peer to connect (multiple allowed)
-n                   No monitoring (one-time sync)
--permissions-file   Permissions file path
--allow HASH         Allow peer
--perms LIST         Permissions (read,write,delete)
--no-tui             Disable TUI
-v, -vv, -vvv        Verbosity
```

## Commands

```
status           Show file and peer count
peers            List peers
connect <hash>   Connect to peer
browse <peer>    Browse peer files
download <file>  Download file
download_all     Download all from peer
logs             View logs
quit             Exit
```

## Permissions

Create `permissions.conf`:
```
# Full access
a1b2c3d4e5f6g7h8 read,write,delete

# Read-only
9876543210fedcba read

# Public read
* read
```

Use:
```bash
python rns_filesync.py -d ~/shared --permissions-file permissions.conf
```

## How It Works

- Files divided into 4KB blocks, each hashed
- Only changed blocks transmitted (delta sync)
- SHA-256 ensures integrity
- Scans directory every 5 seconds
- Mesh distribution (peers relay files)
- Last write wins (no conflict resolution)
