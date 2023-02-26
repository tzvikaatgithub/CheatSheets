AWS
:aws:s3:glacier:

[AWS Docs](https://docs.aws.amazon.com/amazonglacier/latest/dev/getting-started-download-archive.html)

# Windows Clients

* https://s3browser.com/amazon-s3-glacier-storage-class.aspx

# Cli

You'll need config somewhere say in `~/.aws`

`config` file:

```
[default]
region = us-east-1
```

`credentials` file:

```
[default]
aws_access_key_id=<bla-bla-bla>
aws_secret_access_key=<another-bla-bla>
```

# Backup file

Here is something coded by Darko to make backup and send to Glacier.

[file](~/projects/s3-backups/backup.sh)
