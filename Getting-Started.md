## Setup

### Pre-Install Requirements
- [Elixir](https://elixir-lang.org/install.html) and Erlang (Typically auto-installs with Elixir)
  - [Check versions here.](https://github.com/digitalworkersguild/banchan/blob/main/.tool-versions)
- [Phoenix](https://hexdocs.pm/phoenix/installation.html)
- [Postgresql](https://wiki.postgresql.org/wiki/Detailed_installation_guides)
- ImageMagick

> Note: If postgresql installed via homebrew, make sure to run `/usr/local/opt/postgres/bin/createuser -s postgres`.

### Initial Install
- Install dependencies with `mix deps.get`
- Set up your env vars file. Create `.env` (*NIX) or `.env.ps1` (Powershell)
  - Add commands for your environment variables there
  - This gets loaded automatically
- Create and migrate your database with `mix ecto.setup`
- Install Node.js dependencies with `npm install` inside the `assets` directory
- To make sure everything is good, run `mix quality`
- Start Phoenix endpoint with `mix phx.server`

Now you can visit [`localhost:4000`](http://localhost:4000) from your browser.

***

## Useful Commands Reference

- Stop Phoenix server: type Ctrl+C twice.
- Start Phoenix server: `mix phx.server`
- Check quality (which includes running tests and checking formatting commands below): `mix quality`
- Check which tests are failing: `mix test` 
- Reset everything: `mix reset`

### Installing Updates

Pull updates with git and then:
- `mix ecto.migrate` to migrate any database changes
- run `npm install` inside the `assets` directory
- run `mix quality`
- then you can start the server again `mix phx.server`

### Adding Static Files

- Static files go in `priv/static`.
- Images go in `priv/static/images/`.
- Example of how to link images from that location: `<img src={Routes.static_path(Endpoint, "/images/shop_card_default.png")} />`

Compilation Steps for static files if you need to change them:
- `mix phx.digest`

### Troubleshooting

- If your local database has issues with migrations, then run `mix ecto.reset` instead of `mix ecto.migrate`.
- You will also need to manually reset the local test database by running `MIX_ENV=test mix ecto.reset`.

## Application Notes

### Working locally 

_aka dev mode_, the following URLs are only available to admins, or when working locally:

- `/admin/sent_emails` to view confirmation emails, password resets, etc since dev mode does not send real emails
- `/admin/dashboard/` to view admin dashboard

#### Local Stripe development (Draft)

1. Set up the [Stripe CLI](https://stripe.com/docs/stripe-cli)
2. Find your [test mode Stripe API secret in the Stripe Dashboard](https://dashboard.stripe.com/test/apikeys) and set it as your `STRIPE_SECRET`. It looks like `sk_test_....`.
3. Invoke `mix stripe.local` to forward webhook events to your local dev server
4. Set the signing secret it displays as your `STRIPE_ENDPOINT_SECRET`. It looks like `whsec_...`.
5. Fire up mix phx.server and go do some fake money stuff!

### Details to Know 

- Phoenix templates are not in use due to incompatibilities with SurfaceUI.
- `banchan_view.ex` is utilities
- `router.ex` to view all URLs and their routes
- `priv/repo/migrations/` and `lib/banchan/` for database schema and migrations
- Database utilizes [ecto](https://hexdocs.pm/ecto/Ecto.html).
- `lib/banchan/accounts/user.ex` for user account setting defaults
- TODO: add details about TailwindCSS

#### Dependencies of Note
Automatically installed as part of the initial install of the repo, here are a few dependencies to be aware of that the project is built on:
- [TailwindCSS](https://tailwindcss.com/)
- [AlpineJS](https://alpinejs.dev/)
- [SurfaceUI](https://surface-ui.org/)
- [DaisyUI](https://daisyui.com)

##### SurfaceUI Specific Details 
- _something something ignore controllers?_ (need to ask Kat)
- [surface slots](https://surface-ui.org/slots) go with components
- Surface contains three different kinds of links: [normal links](https://surface-ui.org/builtincomponents/Link), [live patch](https://surface-ui.org/builtincomponents/LivePatch), and [live redirects](https://surface-ui.org/builtincomponents/LiveRedirect).

#### Other Application Misc
- For email confirmations of account creation, the production site uses Twilio Sendgrid, and the dev mode uses bamboo, which does not send real emails.
- Gigalixer hosts the production site, which utilizes AWS Cloudfront.