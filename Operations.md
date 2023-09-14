Our setup is basically fly.io + GitHub Actions + S3. Sentry is used for monitoring and logging errors on production. Additional third party services are listed in \[[Application Notes|Application-Notes]].

## Automated Deployment
1.  Deploying to main on Github triggers CI testing. After CI testing, Github Actions automatically deploys to staging/dev.
2.  Run `mix bump <major|minor|patch>` on main, which will bump the Banchan Art version accordinly.
    -  That will trigger a new run, which will deploy to staging again; it also generates a GitHub Release with automatically-generated release notes based on merged pull requests.
    -  That Github Release then triggers a release to production.

## Connecting to Servers

> [!IMPORTANT]
> Requires [Flyctl](https://fly.io/docs/hands-on/install-flyctl/) and access to our Fly.io servers.<sup>[1](#footnote1)</sup>

1.  Login via Flyctl `fly auth login`
2.  Verify access to servers `flyctl apps list`
3.  Connect to relevant server, ie `fly ssh console -a banchan-dev --pty -C "/app/bin/banchan remote"`
    -   after connecting to the server for the first time, you'll be able to connect with this shorter command `fly ssh console -a banchan-dev`

## Manual Deployment
> [!WARNING]
> This process is only for use if Github Actions breaks again. 

Requires: 
- Oban Setup locally
- Logged in via [Flyctl](https://fly.io/docs/hands-on/install-flyctl/) and access to our Fly.io servers.<sup>[1](#footnote1)</sup>

1.  Go to local repo.
2.  Ensure local repo is up to date.
3.  `mix deploy.dev` or  `mix deploy.prod` 

## Restarting and checking Servers

From the CLI
- For status: Run `flyctl machine status -a` plus the app name
- For restart: Run `flyctl machine restart -a` plus the app name

> [!NOTE]
> This restarts every server involved with the app name. Alternatively, you can restart individual machines via machine id.

See [Flyctl Reference Guide](https://fly.io/docs/reference/) for more commands to run.

## Monitoring
-   [Dev Server Logs on Fly.io](https://fly.io/apps/banchan-dev/monitoring)<sup>[1](#footnote1)</sup>
-   [Production Server Logs on Fly.io](https://fly.io/apps/banchan-prod/monitoring)<sup>[1](#footnote1)</sup>
-   [Error Logs on Sentry.io](https://sentry.io/organizations/banchan-art/issues/)<sup>[2](#footnote2)</sup>
-   [Oban Web](https://banchan.art/admin/oban)<sup>[2](#footnote2)</sup>
-   [Phoenix Live Dashboard](https://banchan.art/admin/dashboard/home)<sup>[3](#footnote2)</sup>

## Other Notes
- Deployment settings exist in `fly.toml`, `mix.exs`, and `Dockerfile` (not to be confused the one in `.devcontainer`, which is for local dev).

---

<sup>Footnotes</sup> <br />
<sup><a name="footnote1">1:</a></sup> Requires invite to Fly.io <br/>
<sup><a name="footnote1">2:</a></sup> Requires invite to Sentry.io <br/>
<sup><a name="footnote2">3:</a></sup> Requires user with dev permissions on production




