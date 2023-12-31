## Services

Banchan uses the following third-party services as part of its development and deployment:

* [GitHub](https://github.com/BanchanArt) - Code hosting, project management
* [Fly.io](https://fly.io) - Platform + database hosting and clustering (requires invite by email for access)
* [Amazon S3](https://aws.amazon.com/s3/) - File/image uploads storage
* [Plausible](https://plausible.io/) - Web analytics
* [Netlify](https://netlify.com) - Landing page hosting, beta signup email form collection
* [Stripe](https://stripe.com/connect) - Stripe Connect Express with Stripe Tax for payment processing and tax management
* [Sendgrid](https://sendgrid.com/) - Sending emails (both transactional and marketing)
* [Sentry.io](https://sentry.io/) - Logging and error logging (requires invite by email for access)
* Google - OAuth login
* Discord - OAuth login
* [Oban Web](https://getoban.pro/) - Better observability into Oban queues. 
* [Freshdesk](https://www.freshdesk.com/) - Support tickets


### Services Wishlist

Stuff we don't use yet, but might be nice to afford in the future:

* Ticketing system - Debating replacing Freshdesk, but there are other things more pressing right now.


## Working with Stripe

Stripe has [a number of credit card and account numbers for testing](https://stripe.com/docs/testing).

Of note:

* `4000000000000077`: Instantly succeeds a payment, bypassing the pending period (so the amount can be immediately paid out)
* `4000000000000002`: Card declined
* `4242424242424242`: US-based transaction that immediately succeeds but is subject to the payout waiting period (7 days for an account's first payout, even in test mode)

## Environment Variables

There's a number of env vars you need to get set up to get up and running, depending on your needs/environment. See [[Environment Variables|Environment-Variables]].

## Details to Know 

- Phoenix templates are not in use due to incompatibilities with SurfaceUI.
- `router.ex` to view all URLs and their routes
- `priv/repo/migrations/` and `lib/banchan/` for database schema and migrations
- `lib/banchan/uploads/uploads.ex` contains the upload configuration except for max file size, which is set in `config/config.exs`
- `lib/banchan/workers/thumbnailer.ex` is where ImageMagick handles the images, which includes a memory usage limit to 128mb and two jobs at a time. 
  - This limit is relevant when testing on non-local dev (dev.banchan.art) as the memory limit is low, which can cause a OOM killed event on that dev server.

## Dependencies of Note

Automatically installed as part of the initial install of the repo, here are a few dependencies to be aware of that the project is built on:

- [Phoenix](https://www.phoenixframework.org/)
- [Phoenix LiveView](https://hexdocs.pm/phoenix_live_view)
- [SurfaceUI](https://surface-ui.org/)
- [TailwindCSS](https://tailwindcss.com/)
- [DaisyUI](https://daisyui.com)
