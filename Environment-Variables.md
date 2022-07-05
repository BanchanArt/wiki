These are the env vars that Banchan uses to configure various systems **in production**:

## AWS Configuration

These are not required for local development. Uploads are managed locally if no S3 config stuff is present.

* `AWS_ACCESS_KEY_ID` - Get this from the AWS console
* `AWS_SECRET_ACCESS_KEY` - Get this from the AWS console
* `S3_BUCKET_NAME` - Set this to whatever your S3 bucket name is. It can be anything.
* `AWS_REGION` - We usually use `us-west-1`, since that's where Gigalixir is hosted but you can test against whatever you want.

## Stripe

You'll need to set up Stripe if you want to do anything having to do with Studio setup, commissions, transactions, etc, even locally. Fortunately, accounts are relatively easy to make. Note that you'll also want the Stripe CLI (See [[Getting Started|Getting-Started]] for details).

* `STRIPE_SECRET`: regular Stripe API secret key ([test](https://dashboard.stripe.com/test/apikeys), [production](https://dashboard.stripe.com/apikeys))
* `STRIPE_ENDPOINT_SECRET`: Stripe secret for [webhooks endpoints](https://dashboard.stripe.com/webhooks). When using the stripe CLI for local dev, this is displayed when you do `mix stripe.local`.

## Sendgrid

This is for sending emails. Only works in prod. Won't be used at all in dev even if you want to.

* `SENDGRID_DOMAIN`
* `SENDGRID_API_KEY`

## Database stuff

These are **only used for production**. If you want to configure how the database gets accessed in dev, use dev.secrets.exs instead.

* `POOL_SIZE`
* `DATABASE_URL`

## OAuth

Various env vars for getting OAuth ("Log in with...") working. You don't need these locally if you don't plan to use OAuth in dev, but they're required for prod.

### Discord

You can get these from https://discordapp.com/developers/applications, while logged in as your desired account owner.

* `DISCORD_CLIENT_ID`
* `DISCORD_CLIENT_SECRET`

### Twitter

You can get these from https://developer.twitter.com/en/portal/dashboard. Note that you need an Elevated account (it's free, but you need to get the app manually approved). Note that these are NOT the OAuth client id/client secret as with the others.

* `TWITTER_CONSUMER_KEY`
* `TWITTER_CONSUMER_SECRET`

### Google

You can get these from https://console.developers.google.com/apis/credentials

* `GOOGLE_CLIENT_ID`
* `GOOGLE_CLIENT_SECRET`
