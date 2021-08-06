## Setup

### Requirements
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

To stop the Phoenix server:
- Stop by typing Ctrl+C twice.

To start the Phoenix server:
- `mix phx.server`

### Installing Updates


## Application Notes

### Working locally 
_aka dev mode_
- `/admin/sent-emails` to view confirmation emails, password resets, etc since dev mode does not send real emails

Other:
- `assets/css/bulma.scss` for theme customization (overrides Bulma defaults)
- `lib/banchan/accounts/user.ex` for user account setting defaults

### Adding static files

- Static files go in `assets/static/`.
- Images go in `assets/static/images/`.

Compilation Steps for static files
- `npm run deploy --prefix ./assets`
- `mix phx.digest`

Location of images after compiling for live site: `/priv/static/images/`.
Example of how to link images from that location: `<img src={Routes.static_path(Endpoint, "/images/shop_card_default.png")} />`


