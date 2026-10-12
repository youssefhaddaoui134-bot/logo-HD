# Render deployment

## Shared design settings

Design editor settings are stored in the server-side SQLite database. To keep
them across deploys on Render:

1. Add a Render Persistent Disk mounted at `/var/data`.
2. Set `DESIGN_SETTINGS_DB_PATH=/var/data/design-settings.sqlite`.
3. Keep the service at one instance while it uses SQLite. Render disks attach
   to one service instance; multiple instances need a shared database service.

If the configured database does not exist but `data/design-settings.sqlite`
does, the server copies that database to the configured path before opening it.

## GoalAPI logos

Team badges and league logos are read from the `badge` and `logo` fields in
GoalAPI responses. The server accepts image URLs hosted at
`media.goal-api.com/badges/`; no separate logo provider, API key, or lookup
quota is needed. The site's default logo is used if GoalAPI does not provide
a valid logo. GoalAPI remains the source for all match and football data.
