---
layout: default
title: backup_restoration.py
parent: Utilities
nav_order: 3
permalink: /utilities/backup-restoration
---

# `backup_restoration.py`

Restore the database from a backup.

`backup_restoration.py [OPTIONS] -d <path/to/database/>`

Required arguments:
- `-d`, `--database <db_dir>` Path to database directory.

Optional arguments:
- `--list_backups` List available backups to restore from
- `--restore <N>` Number of backup to restore from
- `-h`, `--help` Show this help message and exit