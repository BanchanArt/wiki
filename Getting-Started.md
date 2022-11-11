## Setup

### Pre-Install Requirements
- [Elixir](https://elixir-lang.org/install.html) and Erlang (Typically auto-installs with Elixir)
  - [Check versions here.](https://github.com/BanchanArt/banchan/blob/main/Dockerfile#L15-L16)
- [Postgresql v13 or later](https://wiki.postgresql.org/wiki/Detailed_installation_guides) ATM the tests require a postgres/postgres user/password to run. Check [this doc](https://academind.com/tutorials/postgresql-start-stop-uninstall-upgrade-server#resetting-the-root-user-password  ) for info on how to reset your postgres password. 
- [ImageMagick](https://imagemagick.org/)
- [FFmpeg](https://ffmpeg.org/download.html)
- [NodeJS](https://nodejs.org/en/download/)
  - [Check versions here.](https://github.com/BanchanArt/banchan/blob/main/Dockerfile#L27)
- [Stripe Account](https://stripe.com)
  - Your country MUST be set to "United States". If you don't know how to do this, or you get an error like "You cannot request the \`transfers\` capability without the \`card_payments\` capability for accounts in US." during setup step, try creating a new account by going to the top left drop down and choosing `+ New account` and create a new account set to US, with all the settings you need.
  - [Activate Stripe Tax](https://dashboard.stripe.com/setup/tax/activate) and add an origin address (if local dev, do it in test mode).
  - For local dev, you don't need to provide all your details. You'll be working in test mode.
- [Stripe CLI](https://stripe.com/docs/stripe-cli) (only for local dev)

> Note: If postgresql installed via homebrew, make sure to run `/usr/local/opt/postgres/bin/createuser -s postgres`.

### Initial Install

- Copy `config/dev.secret.example.exs` to `config/dev.secret.exs` and fill out the relevant fields as instructed.
- Install Elixir dependencies, NPM packages, and set up/migrate the database with `mix setup`.
- To make sure everything is good, run `mix quality`
- Start your local Stripe server with `mix stripe.local`
- Start Phoenix endpoint with `mix phx.server`
- [Windows Only] If you want color output for tests, [run this command in your terminal](https://hexdocs.pm/mix/1.13/Mix.Tasks.Test.html#module-coloring): `reg add HKCU\Console /v VirtualTerminalLevel /t REG_DWORD /d 1`

Now you can visit [`localhost:4000`](http://localhost:4000) from your browser.

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

## Next Steps

Check out [[Application Notes|Application-Notes]] for more details, such as where things are hosted, and how to work with Stripe transactions.