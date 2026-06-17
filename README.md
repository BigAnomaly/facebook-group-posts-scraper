[Facebook Group Posts Scraper](https://apify.com/logical_scrapers/facebook-group-posts-scraper?fpr=data)

Transform how you analyze Facebook groups! This powerful tool helps businesses, researchers, and marketers extract valuable insights from public Facebook groups. Whether you're tracking market trends, conducting research, or monitoring social engagement, our scraper delivers the data you need.

## 🌟 Why Choose This Scraper?

- ⚡ **Lightning Fast**: Extract hundreds of posts in minutes
- 🎯 **Precision Targeting**: Focus on specific groups or analyze multiple groups at once
- 📊 **Rich Insights**: Capture reactions, comments, shares, and engagement metrics
- 🔄 **Bulk Processing**: Analyze up to 50 groups in one go
- 🛡️ **Reliable & Stable**: Built for consistent, dependable performance
- 📱 **Modern Interface**: Simple setup, powerful results

## 🎯 Perfect For

- 📈 **Market Research**: Track trends and consumer sentiment
- 🎭 **Social Media Managers**: Monitor engagement and content performance
- 📚 **Researchers**: Gather data for social media studies
- 💼 **Business Intelligence**: Analyze competitor activities
- 🔍 **Lead Generation**: Find potential customers and opportunities

## 📝 Input Configuration

### Required Parameters

- **`groupUrls`** (array of strings)

- Facebook group URLs in any format:

- Name-based: `https://web.facebook.com/groups/techstartups`
- ID-based: `https://web.facebook.com/groups/123456789`
- Min: 1 group, Max: 50 groups
- Example: `["https://web.facebook.com/groups/techstartups"]`

### Optional Parameters

- **`maxResults`** (integer)

- Maximum posts to collect per group
- Range: 1-1000
- Default: 10
- Example: `100`
- **`untilDate`** (string)

- Stop collecting posts older than this date
- Format: YYYY-MM-DD
- Example: `"2024-01-01"`
- Note: When set, forces sorting to CHRONOLOGICAL
- **`sortingSetting`** (string)

- How to sort posts when scraping
- Options:

- `"RECENT_ACTIVITY"`: Latest activity first
- `"CHRONOLOGICAL"`: Newest posts first
- `"TOP_POSTS"`: Most engaging posts first
- Default: `"CHRONOLOGICAL"`
- Note: Ignored if untilDate is set

### Input Example

```
{
  "groupUrls": [
    "https://web.facebook.com/groups/techstartups",
    "https://web.facebook.com/groups/123456789"
  ],
  "maxResults": 100,
  "untilDate": "2024-01-01",
  "sortingSetting": "CHRONOLOGICAL"
}
```

## 📊 Output Format

Each post is returned with rich metadata. Here's a detailed example:

```
{
  "post_id": "987654321098765",
  "creation_time": "2024-01-15T10:30:45.000Z",
  "message": "🚀 Just launched our new AI product! Looking for beta testers. Comment below if interested! #TechStartup #Innovation",
  "post_url": "https://web.facebook.com/groups/techstartups/posts/987654321098765",
  "reactions": {
    "total": 145,
    "breakdown": {
      "like": 89,
      "love": 32,
      "wow": 24
    }
  },
  "comments_count": 28,
  "shares_count": 12,
  "author": {
    "id": "100012345678901",
    "name": "Alex Chen",
    "url": "https://web.facebook.com/alex.chen.tech"
  },
  "attachments": [
    {
      "type": "photo",
      "id": "123456789012345",
      "url": "https://web.facebook.com/photo.php?fbid=123456789012345",
      "thumbnail": "https://scontent.example.com/photo123.jpg",
      "width": 1200,
      "height": 800,
      "description": "Product dashboard screenshot showing AI analytics interface",
      "download_urls": [
        {
          "url": "https://scontent.example.com/photo123_high.jpg",
          "type": "photo_image",
          "quality": "high",
          "width": 1200,
          "height": 800
        }
      ]
    }
  ],
  "facebook_group_url": "https://web.facebook.com/groups/techstartups",
  "facebook_group_name": "Tech Startups Network"
}
```

### Output Fields Explained

- **Basic Post Data**

- `post_id`: Unique identifier for the post
- `creation_time`: ISO timestamp of post creation
- `message`: Post text content (null if no text)
- `post_url`: Direct link to the post
- **Engagement Metrics**

- `reactions`: Total count and breakdown by type
- `comments_count`: Number of comments
- `shares_count`: Number of shares
- **Author Information**

- `author.id`: Author's Facebook ID
- `author.name`: Author's display name
- `author.url`: Link to author's profile
- **Media Attachments**

- `attachments`: Array of media (photos, videos, links)
- Each attachment includes:

- Type and ID
- URLs (original and thumbnail)
- Dimensions
- Description
- Download options
- **Group Context**

- `facebook_group_url`: Source group URL
- `facebook_group_name`: Group name or ID

## 🚀 Key Features

- **Smart Date Filtering**: Collect posts from specific time periods
- **Engagement Metrics**: Track reactions, comments, and shares
- **Bulk Processing**: Analyze multiple groups simultaneously
- **Author Details**: Identify key influencers and active members
- **Post Content**: Capture full message content and attachments
- **Group Context**: Keep track of post sources and group details

## 🎮 Easy to Use

1. **Add Group URLs**: Paste the Facebook group links you want to analyze
2. **Set Parameters**: Choose how many posts to collect and date ranges
3. **Get Results**: Receive structured data ready for analysis

## 📊 Use Cases

- **Competitor Analysis**: Monitor competitor groups and engagement
- **Market Research**: Gather customer feedback and preferences
- **Content Strategy**: Identify trending topics and discussions
- **Community Management**: Track group activity and engagement
- **Lead Generation**: Find potential customers and opportunities
- **Academic Research**: Collect data for social media studies

## 🤝 Support & Contact

Need help or have questions? We're here to help!

- Email: [coredev.dan@gmail.com](mailto:coredev.dan@gmail.com)
- Other tools: [Check Other scrapers](https://apify.com/logical_scrapers)

## Keywords

facebook group scraper, facebook data extraction, social media analytics, facebook group analysis, facebook engagement metrics, social media monitoring, facebook group insights, market research tool, social media data collection, facebook group tracker, community analysis tool, social media research, facebook group monitoring, engagement analytics, social media data extraction

---

*Note: This tool is designed for public Facebook groups only and should be used in compliance with Facebook's terms of service.*