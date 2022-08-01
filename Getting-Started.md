## Setup

### Pre-Install Requirements
- [Elixir](https://elixir-lang.org/install.html) and Erlang (Typically auto-installs with Elixir)
  - [Check versions here.](https://github.com/digitalworkersguild/banchan/blob/main/Dockerfile#L15-L16)
- [Postgresql v13 or later](https://wiki.postgresql.org/wiki/Detailed_installation_guides)
- [ImageMagick](https://imagemagick.org/)
- [NodeJS](https://nodejs.org/en/download/)
  - [Check versions here.](https://github.com/digitalworkersguild/banchan/blob/main/Dockerfile#L27)
- [Stripe CLI](https://stripe.com/docs/stripe-cli) (only for local dev)

> Note: If postgresql installed via homebrew, make sure to run `/usr/local/opt/postgres/bin/createuser -s postgres`.

### Initial Install

- Install dependencies with `mix deps.get`
- Copy `config/dev.secret.example.exs` to `config/dev.secret.exs` and fill out the relevant fields as instructed.
- Create and migrate your database with `mix ecto.setup`.
- To make sure everything is good, run `mix quality`
- Start your local Stripe server with `mix stripe.local`
- Start Phoenix endpoint with `mix phx.server`
- [Windows Only] If you want color output for tests, [run this command in your terminal](https://hexdocs.pm/mix/1.13/Mix.Tasks.Test.html#module-coloring): `reg add HKCU\Console /v VirtualTerminalLevel /t REG_DWORD /d 1`

Now you can visit [`localhost:4000`](http://localhost:4000) from your browser.

***

## Other useful commands

### Database

- `mix ecto.migrate`: Run migrations. Remember to do this whenever you pull from git, if there's new migrations!
- `mix reset`: blow away your local database and start fresh.
- `mix ecto.gen.migration <name>`: Generate a new migration.

### Inner loop

- `mix test`: Run just the test suite.
- `mix credo`: Run the linter/static analyzer. It tends to be pretty picky. You can ignore messages about TODOs.
- `mix format`/`mix fmt`: format your code.
- `mix quality`: Runs test + credo + format together.
- `mix test test/path/here.ex`: run a specific test file. Append `:<LINE>` to execute a specific test in that file.

### Adding Static Files

- Static files go in `priv/static`.
- Images go in `priv/static/images/`.
- Example of how to link images from that location: `<img src={Routes.static_path(Endpoint, "/images/shop_card_default.png")} />`

### Troubleshooting

- If your local database has issues with migrations, then run `mix ecto.reset` instead of `mix ecto.migrate`.

## Application Notes

### Working with Stripe

In order to create studios and test transactions locally, you need to create your own Stripe account. The country _must_ be set to the United States, since that's what Banchan currently expects and it's not configurable. You'll also need to install and run the [Stripe CLI](https://stripe.com/docs/stripe-cli).

Stripe has [a number of credit card and account numbers for testing](https://stripe.com/docs/testing).

Of note:

* `4000000000000077`: Instantly succeeds a payment, bypassing the pending period (so the amount can be immediately paid out)
* `4000000000000002`: Card declined
* `4242424242424242`: US-based transaction that immediately succeeds but is subject to the payout waiting period (7 days for an account's first payout, even in test mode)

### Environment Variables

There's a number of env vars you need to get set up to get up and running, depending on your needs/environment. See [[Environment Variables|Environment-Variables]].

### Working locally 

_aka dev mode_, the following URLs are only available to admins, or when working locally:

- `/admin/sent_emails` to view confirmation emails, password resets, etc since dev mode does not send real emails
- `/admin/dashboard/` to view admin dashboard

### Details to Know 

- Phoenix templates are not in used due to incompatibilities with SurfaceUI.
- `router.ex` to view all URLs and their routes
- `priv/repo/migrations/` and `lib/banchan/` for database schema and migrations

#### Dependencies of Note

Automatically installed as part of the initial install of the repo, here are a few dependencies to be aware of that the project is built on:

- [Phoenix](https://www.phoenixframework.org/)
- [Phoenix LiveView](https://hexdocs.pm/phoenix_live_view)
- [SurfaceUI](https://surface-ui.org/)
- [TailwindCSS](https://tailwindcss.com/)
- [DaisyUI](https://daisyui.com)

##### SurfaceUI Specific Details 

- [surface slots](https://surface-ui.org/slots) go with components
- Surface contains three different kinds of links: [normal links](https://surface-ui.org/builtincomponents/Link), [live patch](https://surface-ui.org/builtincomponents/LivePatch), and [live redirects](https://surface-ui.org/builtincomponents/LiveRedirect).

#### Other Application Misc

- For email confirmations of account creation, the production site uses Twilio Sendgrid. No real emails are sent during local dev.
- [Fly.io](https://fly.io) hosts the production site.
- Images are hosted on S3 in production, and in `priv/uploads` in dev/test.