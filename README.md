# Windows Server Automation

Windows Server backups were stored locally on a dedicated drive, but there was no offsite copy. If the server's backup drive failed, the backups went with it. We needed a simple, scheduled way to sync those backups to S3.

## What This Script Does

**Upload-BackupsToS3.bat** syncs the local backup drive to an S3 bucket, organized by date. It builds a date-stamped folder path using WMIC and runs `aws s3 sync` to push only new or changed files. Designed to run as a daily scheduled task on the Windows Server.

## Usage

```batch
:: Run manually
Upload-BackupsToS3.bat

:: Or schedule via Task Scheduler to run daily
```

The script syncs from the `X:\` drive (the backup volume) to an S3 bucket with date-based folder structure: `s3://bucket-name/YYYY-MM-DD/`.

## Requirements

- AWS CLI installed and configured with appropriate credentials
- IAM permissions for `s3:PutObject`, `s3:ListBucket` on the target bucket
- Backup volume mounted at the expected drive letter
- Scheduled task configured to run daily (typically after the backup window completes)

## Blog Post

[Automating Windows Server Backups to S3 with a BAT File](https://blog.soarsystems.cc/windows-server-automation)
