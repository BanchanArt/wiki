These are the env vars that Banchan uses to configure various systems **in production**:

## AWS Configuration

* `AWS_ACCESS_KEY_ID` - Get this from the AWS console
* `AWS_SECRET_ACCESS_KEY` - Get this from the AWS console
* `S3_BUCKET_NAME` - Set this to whatever your S3 bucket name is. It can be anything.
* `AWS_REGION` - We usually use `us-west-1`, since that's where Gigalixir is hosted but you can test against whatever you want.

## Stripe

* `STRIPE_SECRET`: regular Stripe API secret key ([test](https://dashboard.stripe.com/test/apikeys), [production](https://dashboard.stripe.com/apikeys))
* `STRIPE_ENDPOINT_SECRET`: Stripe secret for [webhooks endpoints](https://dashboard.stripe.com/webhooks). When using the stripe CLI for local dev, this is displayed when you do `mix stripe.local`.

## Sendgrid

This is for sending emails. Only works in prod.

* `SENDGRID_DOMAIN`
* `SENDGRID_API_KEY`

## Database stuff

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
