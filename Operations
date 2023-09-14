## About Operations
Our setup is basically fly.io + GitHub Actions + S3. Sentry is used for monitoring and logging errors on production. Additional third party serives are listed in \[[Application Notes|Application-Notes]].

## Automated Deployment
1.  When you deploy to main, we do our regular CI testing and then we deploy to staging/dev, automatically.
2.  If you do `mix bump <major|minor|patch>` on main, it'll bump the Banchan Art version accordinly.
    -  That will trigger a new run, which will deploy to staging again; it also generates a GitHub Release with automatically-generated release notes based on merged pull requests.
    -  That Github Release then triggers a release to prod.

## Connecting to Servers

Requires [Flyctl](https://fly.io/docs/hands-on/install-flyctl/) and access to our Fly.io servers.

1.  Login via Flyctl `fly auth login`
2.  Verify access to servers `flyctl apps list`
3.  Connect to relevant server, ie `fly ssh console -a banchan-dev --pty -C "/app/bin/banchan remote"`
    -   after connecting to the server for the first time, you'll be able to connect with this shorter command `fly ssh console -a banchan-dev`

## Manual Deployment
This process is only for use if Github Actions breaks again. 

Requires 
- Oban Setup locally
- Logged in via [Flyctl](https://fly.io/docs/hands-on/install-flyctl/) and access to our Fly.io servers.

1.  Go to local repo.
2.  Ensure local repo is up to date.
3.  `mix deploy.dev` or  `mix deploy.prod` 

## Restarting and checking Servers

From the CLI
- For status: Run `flyctl machine status -a` plus the app name
- For restart: Run `flyctl machine restart -a` plus the app name
  - Note: this restarts every server involved with the app name. Alternatively, you can restart individual machines via machine id.

See [Flyctl Reference Guide](https://fly.io/docs/reference/) for more commands to run.

## Monitoring
-   [Dev Server Logs on Fly.io](https://fly.io/apps/banchan-dev/monitoring)
-   [Production Server Logs on Fly.io](https://fly.io/apps/banchan-prod/monitoring)
-   [Error Logs on Sentry.io](https://sentry.io/organizations/banchan-art/issues/) (Requires invite to Sentry.io)
-   [Oban Web](https://banchan.art/admin/oban) (Requires user with dev permissions on production)
-   [Phoenix Live Dashboard](https://banchan.art/admin/dashboard/home) (Requires user with dev permissions on production)

## Other Notes
- Deployment settings exist in `fly.toml`, `mix.exs`, and `Dockerfile` (not to be confused the one in `.devcontainer`, which is for local dev)


