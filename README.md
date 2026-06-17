[Facebook Group Posts Scraper](https://apify.com/crowdpull/facebook-group-posts-scraper?fpr=data)

# CrowdPull FB Group Posts Scraper

Extract posts from any **public** Facebook group — no login or cookies required.

No browser automation — just fast, lightweight HTTP requests for reliable extraction.

## Features

- **No login required** — extracts posts anonymously from public groups
- **Smart Scrape (dedup)** — skip posts already scraped in previous runs, saving up to 75% on recurring scrapes
- **Full post data** — text, author, permalink, timestamp, reactions, comments, images
- **Date filtering** — extract posts newer than a specific date (ISO or relative: `7d`, `30d`, `6m`)
- **Author filtering** — find posts from specific contributors or admins
- **Engagement filtering** — minimum comment/reaction thresholds
- **Sorting** — chronological (newest first) or algorithmic (top posts)
- **Multi-group support** — process multiple groups in a single run
- **Pagination** — automatically scrolls through the full feed
- **Comment scraper chaining** — automatically trigger the comment scraper after extraction

## Smart Scrape: How It Saves You Money

Enable **Smart Scrape** to skip posts you've already extracted. The scraper maintains a persistent cache per group that survives across runs indefinitely.

|  | Without Smart Scrape | With Smart Scrape |
| --- | --- | --- |
| **Run 1** (500 posts) | 500 × $0.004 = **$2.00** | 500 × $0.004 = **$2.00** |
| **Run 2** (125 new) | 500 × $0.004 = **$2.00** | 125 new × $0.004 + 375 skip × $0.001 = **$0.875** |
| **Run 3** (125 new) | 500 × $0.004 = **$2.00** | 125 new × $0.004 + 375 skip × $0.001 = **$0.875** |
| **Run 4** (125 new) | 500 × $0.004 = **$2.00** | 125 new × $0.004 + 375 skip × $0.001 = **$0.875** |
| **Monthly total** | **$8.02** | **$4.65** |
| **Unique posts** | 500 (+ 1,500 duplicates) | 875 (zero duplicates) |
| **Cost per unique post** | $0.016 | $0.005 |

**42% cheaper per month. 69% cheaper per unique post. Zero duplicate cleanup.**

### Refresh Window

Set `refreshWindowDays` to re-check recent posts for updated comment/reaction counts. For example, `refreshWindowDays: 7` re-scrapes posts from the last 7 days even if cached, so you always get fresh engagement data on recent content.

## What you get per post

| Field | Description |
| --- | --- |
| `postId` | Unique post identifier |
| `postUrl` | Direct permalink to the post |
| `postText` | Full post text content |
| `authorName` | Author's display name |
| `authorProfileUrl` | Link to author's profile |
| `timestamp` | ISO 8601 timestamp |
| `commentCount` | Number of comments |
| `reactionCount` | Number of reactions |
| `imageUrls` | Array of image URLs attached to the post |
| `sharedLinks` | URLs shared in the post text |
| `groupUrl` | Source group URL |

## How it works

1. Fetches the group page anonymously — no login, no cookies, no browser
2. Extracts structured post data from Facebook's response
3. Checks each post against the dedup cache (if Smart Scrape is enabled)
4. Paginates automatically until `maxPosts` reached or feed exhausted
5. Saves updated cache for next run

## Input examples

### Basic extraction

```
{
  "startUrls": [
    { "url": "https://www.facebook.com/groups/homebakeryforbeginners/" }
  ],
  "maxPosts": 25,
  "sortOrder": "CHRONOLOGICAL"
}
```

### Smart Scrape (incremental monitoring)

```
{
  "startUrls": [
    { "url": "https://www.facebook.com/groups/homebakeryforbeginners/" }
  ],
  "maxPosts": 100,
  "enableDedup": true,
  "refreshWindowDays": 7
}
```

## Output example

```
{
  "postId": "903615849189843",
  "postUrl": "https://www.facebook.com/groups/homebakeryforbeginners/posts/903615849189843/",
  "postText": "What St. Patrick's Day themed treats are you planning to make this year?",
  "authorName": "Sarah Mitchell",
  "authorProfileUrl": "https://www.facebook.com/sarah.mitchell",
  "timestamp": "2026-02-25T18:00:00.000Z",
  "commentCount": 12,
  "reactionCount": 45,
  "imageUrls": ["https://scontent.fudi1-1.fna.fbcdn.net/..."],
  "sharedLinks": [],
  "groupUrl": "https://www.facebook.com/groups/homebakeryforbeginners/"
}
```

## Pair with the Comment Scraper

Use this Actor to find high-engagement posts, then feed the `postUrl` values into **[Facebook Post Comment Scraper](https://apify.com/crowdpull/facebook-post-comment-scraper)** to extract all 30+ fields per comment — including demographics, reaction breakdowns, and moderation signals that no other scraper captures.

You can also enable automatic chaining via the `chainCommentScraperTaskId` input to trigger comment extraction automatically after the feed scrape completes.

## Cost estimate

This Actor uses **no browser** — just lightweight HTTP requests.

| Event | Cost |
| --- | --- |
| Actor start | $0.005 (one-time per run) |
| New post extracted | $0.004/post |
| Cache check (Smart Scrape skip) | $0.001/post |

Volume discounts available at Starter, Scale, and Business tiers.

## Is it legal to scrape Facebook groups?

Our scrapers are ethical and do not extract any private user data, such as email addresses, gender, or location. They only extract what the user has chosen to share publicly. We therefore believe that our scrapers, when used for ethical purposes by Apify users, are safe. However, you should be aware that your results could contain personal data. Personal data is protected by the GDPR in the European Union and by other regulations around the world. You should not scrape personal data unless you have a legitimate reason to do so. If you're unsure whether your reason is legitimate, consult your lawyers.

## Limitations

- Only works with **public** groups (private groups return 0 posts)
- Facebook may change internal APIs — report issues if extraction stops
- Facebook rate limits apply; residential proxies recommended
- Anonymous API returns `commentCount: 0` for most posts — use the comment scraper for accurate counts