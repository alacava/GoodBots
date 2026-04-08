# GoodBots
Curated lists of IP addresses/whitelists of good bots and crawlers. Includes GoogleBot, BingBot, DuckDuckBot, etc.

All IP-Lists are in the [CIDR-Notation](https://en.wikipedia.org/wiki/Classless_Inter-Domain_Routing) and can be used as whitelists in your webserver's firewall or as an exception for rate-limits.

Either use the [all.ips](all.ips) list or a specific service's list of IP-Addresses found in the [iplists/](iplists/) directory.

The lists are updated daily via a scheduled GitHub Action.

## Integrations

### CloudFlare IP List

The `iplists-botsonly/` lists are automatically synced to a CloudFlare IP List daily. Configure the following GitHub secrets to enable this:

| Secret | Description |
|--------|-------------|
| `CF_ACCOUNT_ID` | CloudFlare account ID |
| `CF_LIST_ID` | CloudFlare IP list ID |
| `CLOUDFLARE_API_TOKEN` | CloudFlare API token with List write access |

### AWS WAF IP Sets

The `iplists-botsonly/` lists are also synced to AWS WAF daily. Because AWS WAF IP sets are typed, IPv4 and IPv6 addresses are written to two separate IP sets. Addresses are normalized to CIDR notation (bare IPs get `/32` or `/128`), and IPv6 is expanded to full notation (no `::` compression) as required by the WAF API.

Create two IP sets in AWS WAF — one with address version `IPV4` and one with `IPV6` — then configure the following GitHub secrets:

| Secret | Description |
|--------|-------------|
| `AWS_ACCESS_KEY_ID` | IAM access key ID |
| `AWS_SECRET_ACCESS_KEY` | IAM secret access key |
| `AWS_REGION` | AWS region (use `us-east-1` for CloudFront-scoped WAF) |
| `AWS_WAF_SCOPE` | `REGIONAL` or `CLOUDFRONT` |
| `AWS_WAF_IPV4_SET_ID` | IPv4 IP set UUID from the AWS console |
| `AWS_WAF_IPV4_SET_NAME` | IPv4 IP set name |
| `AWS_WAF_IPV6_SET_ID` | IPv6 IP set UUID from the AWS console |
| `AWS_WAF_IPV6_SET_NAME` | IPv6 IP set name |

The IAM user/role needs the following permissions:

```json
{
  "Effect": "Allow",
  "Action": [
    "wafv2:GetIPSet",
    "wafv2:UpdateIPSet"
  ],
  "Resource": "arn:aws:wafv2:REGION:ACCOUNT_ID:*/ipset/*"
}
```

<!-- TODO: Better Readme -->
  
```
.
├── all.ips 
│   Combined List of all IP addresses found in iplists/
├── all_botsonly.ips 
│   Combined List of all IP addresses found in iplists-botsonly/
|   -This list has a limited number of lists, mainly those related to bots. This list is shorter to comply with CloudFlare's IP List limit.
|   -Lists with * are included in the smaller list.  
│
└── iplists/
    │
    ├── ahrefsbot.ips
    │   IP-Addresses used by the AhrefsBot Crawler
    │   
    ├── applebot.ips*
    │   IP-Addesses used by the Apple Crawler
    │   
    ├── betteruptimebot.ips*
    │   IP-Addesses used by the BetterUptime Bot
    │   
    ├── bingbot.ips*
    │   IP-Addesses used by the Bing Crawler
    │   
    ├── bunnycdn.ips*
    │   IP-Addesses used by the bunny.net CDN
    │   
    ├── cloudflare.ips
    │   IP-Addesses used by the Cloudflare CDN
    │   
    ├── commoncrawlbot.ips*
    │   IP-Addesses used by the CommonCrawl Bot (CCBot)
    │   
    ├── duckduckbot.ips*
    │   IP-Addesses used by the DuckDuckGo Crawler
    │   
    ├── facebookbot.ips*
    │   IP-Addesses used by the Facebook Link-Preview Bot
    │   
    ├── fastly.ips*
    │   IP-Addesses used by the Fastly CDN
    │   
    ├── freshpingbot.ips*
    │   IP-Addesses used by the Freshping Bot
    │   
    ├── googlebot.ips*
    │   IP-Addesses used by the Google Crawler
    │   
    ├── imagekit.ips*
    │   IP-Addesses used by the Imagekit.io Image Proxy
    │   
    ├── imgix.ips*
    │   IP-Addesses used by the Imgix Image Proxy
    │   
    ├── internal.ips*
    │   Internal IP-Addresses
    │   
    ├── marginalia.ips*
    │   IP-Addresses used by the Marginalia Search Crawler
    │   
    ├── mojeekbot.ips*
    │   IP-Addesses used by the Mojeek Crawler
    │   
    ├── molliewebhook.ips*
    │   IP-Addesses used by Mollie to send out Webhooks
    │   
    ├── outageowl.ips*
    │   IP-Addesses used by the Outage Owl Bot
    │   
    ├── pingdombot.ips*
    │   IP-Addesses used by the Pingdom Bot
    │   
    ├── rssapi.ips*
    │   IP-Addesses used by the RSSAPI.net Feed parser
    │   
    ├── stripewebhook.ips*
    │   IP-Addesses used by Stripe to send out Webhooks
    │   
    ├── telegrambot.ips*
    │   IP-Addesses used by the Telegram Link-Preview Bot
    │   
    ├── twitterbot.ips*
    │   IP-Addesses used by the Twitter/X Link-Preview Bot
    │
    ├── uptimerobot.ips*
    │   IP-Addesses used by UptimeRobot.com
    │
    ├── webpagetestbot.ips*
    │   IP-Addesses used by Webpagetest.org
    │
    └── yandex.ips* 
        IP-Addesses used by the Yandex Crawler
        
```
