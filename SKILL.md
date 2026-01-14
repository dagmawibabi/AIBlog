# Writing Style Guide

## Personal Blogger Tone

Write as a genuine human being sharing your thoughts, discoveries, and experiences—not as a company, marketer, or thought leader. Simon Willison's blog is the ideal model: personal, curious, humble, and practical.

### Key Characteristics

- **Be yourself**: Write in your natural voice. Use "I" freely and share personal experiences. Don't adopt a corporate or "influencer" tone.
- **No hype or sales pitch**: Avoid promotional language like "game-changing," "revolutionary," "must-have," or "transformative." Simply explain what something is and why you found it interesting or useful.
- **Embrace learning**: Share what you just learned, what surprised you, what confused you. Celebrating even basic discoveries is empowering for you and your readers.
- **Stay humble**: You don't have all the answers. Acknowledge uncertainty, share incomplete thoughts, and be open about what you don't know.
- **Document your process**: Explain how you do things, what tools you use, what didn't work. This is genuinely useful content.
- **No pressure to be unique**: You don't need to say something no one has ever said. Write about what you learned, what you built, what you found interesting.
- **Credit others**: Always link to and name the creators, authors, and projects you reference. It's generous and useful.

### What to Avoid

- Clickbait titles or sensational claims
- "Influencer" language ("Let me tell you why this is HUGE...")
- Selling anything (products, courses, newsletters)
- Pretending to be an expert on everything
- Writing to impress rather than to share

### What to Embrace

- "Here's what I just figured out..."
- "I tried X and here's what happened..."
- "This confused me at first, but..."
- "I'm not sure about this, but..."
- "I learned this from [person/project]..."
- "Here's how I do X..."

## Blog Format

Every blog post must follow this format:

### Front Matter (Required at the top)

```yaml
---
title: Your Blog Title
date: YYYY-MM-DD
description: A brief, engaging description of what the blog covers. This appears in the feed and previews.
category: 'Category Name'
---
```

- **title**: Clear, descriptive title that conveys the blog's topic
- **date**: Publication date in YYYY-MM-DD format
- **description**: 1-2 sentences summarizing the blog. Make it engaging—this is what readers see in the feed
- **category**: Choose from existing categories or create a new one if needed

### Content Structure

1. **Header Image**: Place an external image link immediately after the front matter
2. **Opening**: Start with a hook or introduction that draws readers in
3. **Main Sections**: Use `##` for main sections, `###` for subsections
4. **Steps**: Use numbered lists (`1.`, `2.`) for sequential instructions
5. **Notes**: Use bullet points with `*` for additional info, tips, or clarifications
6. **Code Blocks**: Use triple backticks with language for syntax highlighting
7. **Closing**: End with encouragement, next steps, or a call to action

### Example Structure

````markdown
---
title: Your Blog Title
date: 2025-01-15
description: Brief description of the blog post content.
category: 'Tech'
---

![Header Image](https://example.com/header-image.jpg)

Opening paragraph that hooks the reader...

## Main Section

Introduction to this section...

### Subsection

Content goes here...

1. First step
2. Second step
3. Third step

- Note or additional info

```javascript
// Code example
console.log('Hello');
```
````

## Another Section

More content...

### Subsection

More content...

- Another note

## Final Section or Conclusion

Wrap up with key takeaways or next steps.

````

## Images

- **Header Image**: Every blog must have a header image at the top that is directly related to the topic. Use an external image link from the actual source.

- **Source Images from Relevant Sites**: Find images from the websites directly related to your topic:
  - If writing about an OpenAI model → find images from OpenAI's announcement blog or post
  - If writing about Anthropic's work → find images from Anthropic's news/blog
  - If writing about a research paper → find images from the paper or author blogs
  - If writing about a product → find images from the official product page or documentation
  - If writing about a competition or event → find images from the official site

- **In-Content Images**: Include images throughout the blog when they add value—visual explanations, screenshots, diagrams, examples, or relevant media. Source these from the same relevant sites.

- **How to Find Images**:
  1. First, search for the official announcement, blog post, or documentation about the topic
  2. Browse those pages for hero images, diagrams, screenshots, or infographics
  3. Use the image URLs directly from those sources
  4. If images are embedded in the page, extract the direct image URL

- **Image Links**: Always use external image URLs rather than downloading images to `static/blog-images`. Link to images from their original sources.

- **No Image Reuse**: Do not use the same image more than once in a single blog post. Each image should be unique and serve a distinct purpose. If you need to reference a concept again, find a different visual representation or explain it in text.

- **Image Syntax**: Use Markdown image syntax with descriptive alt text:

```markdown
![Descriptive Alt Text](https://example.com/image.jpg)
````

## Research Before Writing

Before writing any blog post, conduct thorough research from multiple authoritative sources:

### 1. Plan Structure and Sections

Before starting to write, research what sections and subtopics should be included:

- Search for how other blogs and articles structure content on similar topics
- Look at table of contents from books, documentation, and comprehensive guides on the subject
- Identify the key concepts, components, and areas that need coverage
- Consider what a reader would need to know to fully understand the topic
- Group related concepts into logical sections
- Plan the flow from foundational concepts to advanced topics
- Create an outline with main sections and subsections before writing

### 2. Source Research

Once you have your structure, research each section:

1. **Simon Willison's Blog**: Always check simonwillison.net for his latest posts, experiments, and insights on AI, LLMs, and related technologies. He frequently shares unique perspectives and timely analysis.

2. **Reddit**: Search relevant subreddits (r/MachineLearning, r/LocalLLaMA, r/ClaudeAI, r/ChatGPT, r/programming, etc.) for real-world discussions, problems people are solving, community insights, and emerging trends.

3. **Current News**: Search for recent news articles, announcements, and developments from reputable tech news sources (The Verge, TechCrunch, Ars Technica, etc.). Stay current with the latest releases and industry changes.

4. **Company Blogs**: Read official blog posts and documentation from companies directly involved with your topic:
   - Anthropic (anthropic.com/news)
   - OpenAI (openai.com/blog)
   - Google DeepMind (deepmind.google/blog)
   - Meta AI (meta.ai/blog)
   - Hugging Face (huggingface.co/blog)
   - And any other relevant companies

5. **Research Papers**: Check arXiv for the latest papers on your topic. Link to relevant papers in your "Further Reading" section.

## Content Quality

- **Be Exceptionally Detailed**: Dive deep into every aspect of your topic. Don't just scratch the surface—explore the nuances, edge cases, and underlying principles. Readers should finish your blog knowing significantly more than when they started.

- **Provide Exceptional Insights**: Offer unique perspectives that readers won't find elsewhere. Connect dots between different sources, synthesize information, and provide analysis that adds genuine value. Share your own experiments, findings, and conclusions.

- **Use Your Research**: Weave insights from Simon Willison, Reddit discussions, company announcements, and news into your narrative. Credit sources and provide links so readers can explore further.

- **Include Specific Examples**: Whenever possible, link to specific projects, products, papers, or implementations. Include screenshots, code snippets, or concrete demonstrations.

- **Stay Current**: Reference the latest developments and explain how they change or inform the topic. Date your references so readers know how recent your information is.

- **Go Beyond Surface Level**: If explaining a technology, explain how it works under the hood. If discussing a trend, explain why it's happening and where it's headed. If covering a tool, show advanced use cases and workflows.

### Keep Blogs Up to Date

- **Research Latest News**: Before writing, search for recent news articles, announcements, and developments on your topic. Check multiple sources to understand the current state of things.

- **Integrate Latest Tweets**: Search for relevant tweets from key figures, companies, and researchers. Tweets often contain timely insights, announcements, or debates that are valuable to include. When integrating tweets:
  - Quote the tweet and explain why it's significant
  - Add context—don't just drop a link
  - Tie it to your broader narrative
  - Credit the author and link to their profile

- **Use Current Information**: Incorporate the latest releases, updates, and changes. If something has changed recently, mention it and explain how it affects the topic.

- **Date Your References**: When referencing news, tweets, or papers, include the date so readers know how recent the information is.

- **Acknowledge Changes**: If a topic has evolved or if new developments have emerged since something was written, acknowledge this and update accordingly.

- **Refresh Old Content**: If you're updating an old blog post, note what has changed and add new information at the top or in a "Updates" section.

### Example of Integrating Latest News/Tweets

Instead of just linking to a news article, write:

> Anthropic released a new update to Claude on [date]. In their announcement tweet, they mentioned [key point]. This is significant because [your analysis of why it matters].

Or:

> I was browsing through the Anthropic blog last week and noticed [something new]. Here's what they said about it:
>
> [Quote from announcement]
>
> I've been testing this feature and here's what I found...

## Language Patterns

- Use em dashes freely (—) for asides and emphasis
- Use ellipsis (...) to create suspense or indicate continuation
- Wrap asides and clarifications in parentheses
- Bold key terms and concepts for emphasis
- Occasionally use exclamation points for genuine enthusiasm
- Include personal opinions, recommendations, and preferences
- Use rhetorical questions to engage the reader

## Content Approach

- Start with a header image that sets the visual tone for the topic
- Use images throughout to illustrate concepts, show examples, or break up text
- Provide context before diving into details
- Include specific examples, links, and references
- Share personal experiences and projects
- Create showcase sections highlighting work (your own or others)
- Tell readers what to look for, click on, or explore next
- Be generous with credit and links to collaborators
- Balance technical depth with accessibility

## Formatting Conventions

- Use code formatting for technical terms, model names, and commands: `base-models`, `Claude Opus 4.5`
- Italicize book titles, movie names, and special terms: _Chain-of-Thought Prompting_
- Embed links naturally in relevant nouns rather than using "click here"
- Use blockquotes for direct quotes from sources or yourself
- Reference dates and timelines to ground the reader in context

## Examples

**Opening**: "In this blog I am going to take you on a journey through..." or "Let me tell you about..."

**Transitions**: "Now before we move on...", "With that out of the way...", "Before proceeding..."

**Engagement**: "I need you to skip to the [section] and checkout...", "No, seriously, you have to go check them out!"

**Enthusiasm**: "This is where vibe-coding shines...", "It was very impressive...", "This is wonderful isn't it?"

**Closing**: End with encouragement, next steps, or a call to action. Sign off personally.
