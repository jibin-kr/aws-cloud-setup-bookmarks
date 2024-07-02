# Resolving Database Collation Issues during MySQL Backup Restore

## The Problem

When restoring a MySQL database backup from a newer version to an older version, you may encounter issues due to differences in database collation.

## The Cause

The MySQL server running on the destination is an older version than the source, which means it doesn't contain the required database collation.

## The Solution

To resolve this issue, you need to make a small tweak to the backup file. Follow these steps:

### Edit the Backup File

1. Open the database backup file in a text editor.
2. Replace the following strings:
	* `utf8mb4_0900_ai_ci` with `utf8mb4_general_ci`
	* `CHARSET=utf8mb4` with `CHARSET=utf8`

### Update the ENGINE Statement

Replace the following line:
```sql
ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci;
```
With
```sql
ENGINE=InnoDB DEFAULT CHARSET=utf8 COLLATE=utf8_general_ci;
```
