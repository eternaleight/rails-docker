# Local configuration and runtime data

Environment files and their backups are local configuration. Copy the relevant
`.env.example` (or `.env.sample`) where available, then configure values locally
or through the deployment platform's secret manager. Only names and empty values
belong in templates. Browser-visible variables must never contain private keys.

Before pulling this change into an existing checkout, copy any local environment
files or database data to a private backup outside the repository. Git can remove
previously tracked files when applying their removal. Restore the private copy
after updating; the ignore rules keep it out of subsequent commits.

Removing a file from Git tracking does not remove earlier commits or invalidate
credentials. Rotate any real credentials that were shared, and coordinate any
history cleanup separately. Never use production data or reusable private keys
as sample data.

The existing Compose bind mount `./src/db/mysql_data:/var/lib/mysql` is retained
so existing development data can continue to be used. That runtime directory is
now ignored and must be provisioned locally. Do not run `docker compose down -v`
or delete the directory to apply this Git-only change.
