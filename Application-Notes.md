## Services

Banchan uses the following third-party services as part of its development and deployment:

* GitHub - Code hosting, project management
* Fly.io - Platform + database hosting and clustering
* Amazon S3 - File/image uploads storage
* Plausible - Web analytics
* Netlify - Landing page hosting, beta signup email form collection
* Stripe - Stripe Connect Express with Stripe Tax for payment processing and tax management
* Sendgrid - Sending emails (both transactional and marketing)
* Sentry.io(?) - (planned?) Logging and error logging
* Google - OAuth login
* Discord - OAuth login
* Twitter - OAuth login

## Working with Stripe

In order to create studios and test transactions locally, you need to create your own Stripe account. The country _must_ be set to the United States, since that's what Banchan currently expects and it's not configurable. It needs to have [Stripe Tax activated](https://dashboard.stripe.com/setup/tax/activate). You'll also need to install and run the [Stripe CLI](https://stripe.com/docs/stripe-cli).

Stripe has [a number of credit card and account numbers for testing](https://stripe.com/docs/testing).

Of note:

* `4000000000000077`: Instantly succeeds a payment, bypassing the pending period (so the amount can be immediately paid out)
* `4000000000000002`: Card declined
* `4242424242424242`: US-based transaction that immediately succeeds but is subject to the payout waiting period (7 days for an account's first payout, even in test mode)

## Environment Variables

There's a number of env vars you need to get set up to get up and running, depending on your needs/environment. See [[Environment Variables|Environment-Variables]].

## Details to Know 

- Phoenix templates are not in used due to incompatibilities with SurfaceUI.
- `router.ex` to view all URLs and their routes
- `priv/repo/migrations/` and `lib/banchan/` for database schema and migrations

## Dependencies of Note

Automatically installed as part of the initial install of the repo, here are a few dependencies to be aware of that the project is built on:

- [Phoenix](https://www.phoenixframework.org/)
- [Phoenix LiveView](https://hexdocs.pm/phoenix_live_view)
- [SurfaceUI](https://surface-ui.org/)
- [TailwindCSS](https://tailwindcss.com/)
- [DaisyUI](https://daisyui.com)
