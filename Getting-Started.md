## Setup

### Pre-Install Requirements
- [Elixir 1.6+](https://elixir-lang.org/install.html)
- Erlang 20+ (Typically auto-installs with Elixir)
- [Phoenix](https://hexdocs.pm/phoenix/installation.html)
- [Postgresql](https://wiki.postgresql.org/wiki/Detailed_installation_guides)

> Note: If postgresql installed via homebrew, make sure to run `/usr/local/opt/postgres/bin/createuser -s postgres`.

### Initial Install
- Install dependencies with `mix deps.get`
- Create and migrate your database with `mix ecto.setup`
- Install Node.js dependencies with `npm install` inside the `assets` directory
- To make sure everything is good, run `mix quality`
- Start Phoenix endpoint with `mix phx.server`

Now you can visit [`localhost:4000`](http://localhost:4000) from your browser.

### Ater Installing Updates
Pull updates with git and then:
- run `npm install` inside the `assets` directory
- run `mix quality`
- then you can start the server again `mix phx.server`

### Useful Phoenix Commands Reference

- Stop Phoenix server: type Ctrl+C twice.
- Start Phoenix server: `mix phx.server`

#### Adding static files

- Static files go in `assets/static/`.
- Images go in `assets/static/images/`.
- Location of images after compiling for live site: `/priv/static/images/`. 
- Example of how to link images from that location: `<img src={Routes.static_path(Endpoint, "/images/shop_card_default.png")} />`

Compilation Steps for static files
- `npm run deploy --prefix ./assets`
- `mix phx.digest`

## Application Notes

### Working locally 
_aka dev mode_, the following commands will not work on production without an admin user
- `/admin/sent_emails` to view confirmation emails, password resets, etc since dev mode does not send real emails
- `/admin/dashboard/` to view admin dashboard (currently broken as of 8/6/21)

### Other Repo Notes
- `assets/css/bulma.scss` for theme customization (overrides Bulma defaults)
- `lib/banchan/accounts/user.ex` for user account setting defaults
- `banchan_view.ex` is utilities
- `router.ex` to view all URLs and their routes
- 

#### Dependencies of Note
Automatically installed as part of the initial install of the repo, here are a few dependencies to be aware of that the project is built on:
- [Bulma](https://bulma.io/)
- [AlpineJS](https://alpinejs.dev/)
- [SurfaceUI](https://surface-ui.org/)