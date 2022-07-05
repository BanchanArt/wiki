## Setup

### Pre-Install Requirements
- [Elixir](https://elixir-lang.org/install.html) and Erlang (Typically auto-installs with Elixir)
  - [Check versions here.](https://github.com/digitalworkersguild/banchan/blob/main/.tool-versions)
- [Postgresql v13 or later](https://wiki.postgresql.org/wiki/Detailed_installation_guides)
- [ImageMagick](https://imagemagick.org/)
- [NodeJS](https://nodejs.org/en/download/)
  - [Check versions here.](https://github.com/digitalworkersguild/banchan/blob/main/phoenix_static_buildpack.config)
- [Stripe CLI](https://stripe.com/docs/stripe-cli) (only for local dev)

> Note: If postgresql installed via homebrew, make sure to run `/usr/local/opt/postgres/bin/createuser -s postgres`.

### Initial Install

- Install dependencies with `mix deps.get`
- Copy `config/dev.secret.example.exs` to `config/dev.secret.exs` and fill out the relevant fields as instructed.
- Create and migrate your database with `mix ecto.setup`.
- To make sure everything is good, run `mix quality`
- Start your local Stripe server with `mix stripe.local`
- Start Phoenix endpoint with `mix phx.server`

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

Stripe has [a number of credit card and account numbers for testing](https://stripe.com/docs/testing).

Of note:

* `4000000000000077`: Instantly succeeds a payment, bypassing the pending period (so the amount can be immediately paid out)
* `4000000000000002`: Card declined
* `4242424242424242`: US-based transaction that immediately succeeds but is subject to the payout waiting period (7 days for an account's first payout, even in test mode)

### Environment Variables

These are the env vars that Banchan uses to configure various systems **in production**:

#### AWS Configuration

* `AWS_ACCESS_KEY_ID` - Get this from the AWS console
* `AWS_SECRET_ACCESS_KEY` - Get this from the AWS console
* `S3_BUCKET_NAME` - Set this to whatever your S3 bucket name is. It can be anything.
* `AWS_REGION` - We usually use `us-west-1`, since that's where Gigalixir is hosted but you can test against whatever you want.

#### Stripe

* `STRIPE_SECRET`: regular Stripe API secret key ([test](https://dashboard.stripe.com/test/apikeys), [production](https://dashboard.stripe.com/apikeys))
* `STRIPE_ENDPOINT_SECRET`: Stripe secret for [webhooks endpoints](https://dashboard.stripe.com/webhooks). When using the stripe CLI for local dev, this is displayed when you do `mix stripe.local`.

#### Sendgrid

This is for sending emails. Only works in prod.

* `SENDGRID_DOMAIN`
* `SENDGRID_API_KEY`

#### Database stuff

* `POOL_SIZE`
* `DATABASE_URL`

#### OAuth

Various env vars for getting OAuth ("Log in with...") working. You don't need these locally if you don't plan to use OAuth in dev, but they're required for prod.

##### Discord

You can get these from https://discordapp.com/developers/applications, while logged in as your desired account owner.

* `DISCORD_CLIENT_ID`
* `DISCORD_CLIENT_SECRET`

##### Twitter

You can get these from https://developer.twitter.com/en/portal/dashboard. Note that you need an Elevated account (it's free, but you need to get the app manually approved). Note that these are NOT the OAuth client id/client secret as with the others.

* `TWITTER_CONSUMER_KEY`
* `TWITTER_CONSUMER_SECRET`

##### Google

You can get these from https://console.developers.google.com/apis/credentials

* `GOOGLE_CLIENT_ID`
* `GOOGLE_CLIENT_SECRET`

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
- Gigalixir hosts the production site, which utilizes AWS.