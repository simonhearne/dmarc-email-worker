# dmarc-email-worker

A Cloudflare worker script to process incoming DMARC reports and store them in Cloudflare analytics and/or an Elasticsearch datastream.

It makes use of:

- [Cloudflare Workers](https://workers.cloudflare.com/)
- [Email Workers](https://developers.cloudflare.com/email-routing/email-workers/)
- [R2](https://developers.cloudflare.com/r2/)
- [Worker Analytics](https://developers.cloudflare.com/workers/analytics/)
- [Elasticsearch](https://elastic.co/)

**NB: not production ready!!**

## Install instructions

1. Clone this repo
1. Install dependencies with `npm install`
1. Login to your Cloudflare account with `npx wrangler login`
1. Ensure that the names of the R2 buckets used and Worker Analytics dataset are correct in `wrangler.toml`
1. Update `ESindex` in `wrangler.toml` to point to an elastic datastream
1. Set environment variables `EShost`, `username` and `password` for an elasticsearch instance and user who has write privileges on the `ESindex`
1. Run `npx wrangler publish` to publish the worker
1. Configure an Email Routing rule to forward the email from a destinattion address to this worker `dmarc-email-worker`
1. Add this address as RUA to your domain's DMARC record

## Testing

The simplest method for testing is to forward a DMARC email to the email address routed to the worker, use `wrangler tail` to watch the logs and discover in Elastic to view the new records.

## TODO

- [] Add ES index template
- [] Add tests
