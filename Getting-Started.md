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
  - Your country MUST be set to "United States". If you have problems, try creating a new account (top left button on dashboard, choose `+ New account`) and set as required.
  - [Activate Stripe Connect](https://dashboard.stripe.com/setup/connect/activate) (if doing this in local test, enable test mode toggle first)
    - Set up your Platform Profile:
      - Select "E-commerce"
      - Select "From your platform's website or app"
      - Select "Your Platform's name"
      - Select "Your Platform"
      - Select "Yes"
      - Select "No"
      - Submit the profile
  - [Activate Stripe Tax](https://dashboard.stripe.com/setup/tax/activate) (if doing this in local test, enable test mode toggle first)
    - Use Banchan Art LLC's address as the origin address if you don't want to use your own, or you're outside the US (the account MUST be set up in the US):
      - Addr 1: 440 N BARRANCA AVE
      - Addr 2: #8687
      - City: COVINA
      - State: California
      - zip: 91723
    - Say that you're registered to collect taxes in your state
    - Start collecting immediately
  - For local dev, you don't need to provide all your details. You'll be working in test mode.
  - For local dev, your **Stripe secret key** is at https://dashboard.stripe.com/test/apikeys
- [Stripe CLI](https://stripe.com/docs/stripe-cli) (only for local dev)
- If you're using VS Code:
  - Install the [ElixirLS extension](https://marketplace.visualstudio.com/items?itemName=JakeBecker.elixir-ls)
  - Install the [Surface extension](https://marketplace.visualstudio.com/items?itemName=msaraiva.surface)

> Note: If postgresql installed via homebrew, make sure to run `/usr/local/opt/postgres/bin/createuser -s postgres`.

### Initial Install

- Fork this repository, clone it and create a new branch to make changes [(guide here)](https://docs.github.com/en/get-started/quickstart/contributing-to-projects). Follow [github flow](https://docs.github.com/en/get-started/quickstart/github-flow) when you are ready to make changes.
- Copy `config/dev.secret.example.exs` to `config/dev.secret.exs` and fill out the relevant fields as instructed.
- (If your postgres config is different from what's in `config/test.exs`): Copy `config/test.secret.example.exs` to `config/test.secret.exs` and configure postgres credentials as needed.
- Install Elixir dependencies, NPM packages, and set up/migrate the database with `mix setup`. (If you have to run setup more than once, you may need to run `mix ecto.drop` to get rid of databases, which is what setup expects)
- To make sure everything is good, run `mix quality`
- Start your local Stripe server with `mix stripe.local`
- Start Phoenix endpoint with `mix phx.server`
- If you're using VS Code, you can run the `Create terminals` task in order to start a terminal group that automatically runs the stripe and phoenix services, above (instead of having to manage them manually).
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
- `mix quality`: Runs test + credo + check format together.
- `mix test test/path/here.ex`: run a specific test file. Append `:<LINE>` to execute a specific test in that file.
- `mix phx.server`: Start the app.
  - This is generally all you need to run after every pull, although sometimes you won't even have to restart and the server will update its code automatically while running. You might need to restart when configs change, or when you need to run migrations.
- `mix ecto.migrate`: Run a migration, if needed.

### Useful data for local dev
- `seeds.exs` has admin user for local dev
- to confirm email on local user go to `/admin/sent_emails`

### Adding Static Files

- Static files go in `priv/static`.
- Images go in `priv/static/images/`.
- Example of how to link images from that location: `<img src={~p"/images/shop_card_default.png"} />`

### Troubleshooting

- If your local database has issues with migrations, then run `mix ecto.reset` instead of `mix ecto.migrate`.
- If after pulling updates, new dependencies are added, then you need to run `npm install ./assets/` or `mix deps.get`

## Next Steps

Check out [[Application Notes|Application-Notes]] for more details, such as where things are hosted, and how to work with Stripe transactions.

### Best Practices
- With resolving an issue, please mark the PR as fixing that issue, and let GitHub auto-close the issue when the PR gets merged.
  - [Keywords to close issues automatically via the PR ](https://docs.github.com/en/issues/tracking-your-work-with-issues/linking-a-pull-request-to-an-issue#linking-a-pull-request-to-an-issue-using-a-keyword)
- When performing squash/merge via a PR, please list the Fixes in the commit message (one line per fixed issue) as well
