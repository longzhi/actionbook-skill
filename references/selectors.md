# Common CSS Selectors for Popular Sites

Quick reference for frequently-scraped websites.

## Twitter / X (x.com)

### Tweet Content

```css
[data-testid="tweetText"]              /* Tweet text content */
[data-testid="User-Name"]              /* Username display */
[data-testid="tweet"]                  /* Individual tweet container */
article[data-testid="tweet"]           /* Tweet article wrapper */
```

### Timeline & Feed

```css
[data-testid="primaryColumn"]          /* Main timeline column */
[data-testid="cellInnerDiv"]           /* Timeline item cells */
[aria-label="Timeline: Your Home Timeline"]  /* Home timeline */
```

### User Profile

```css
[data-testid="UserName"]               /* Profile display name */
[data-testid="UserProfileHeader_Items"]  /* Profile stats bar */
[data-testid="UserDescription"]        /* Bio text */
```

### Interactions

```css
[data-testid="like"]                   /* Like button */
[data-testid="retweet"]                /* Retweet button */
[data-testid="reply"]                  /* Reply button */
[data-testid="tweetButtonInline"]      /* Compose tweet button */
```

## Reddit (reddit.com)

### Post Content

```css
[data-testid="post-container"]         /* Post wrapper */
h1[slot="title"]                       /* Post title */
[slot="text-body"]                     /* Post body text */
[data-testid="comment"]                /* Comment container */
```

### Voting & Engagement

```css
[aria-label*="upvote"]                 /* Upvote button */
[aria-label*="downvote"]               /* Downvote button */
[data-testid="comment-submission-form-richtext"]  /* Comment box */
```

## LinkedIn (linkedin.com)

### Feed Posts

```css
.feed-shared-update-v2                 /* Post container */
.feed-shared-text                      /* Post text content */
.feed-shared-actor__name               /* Post author name */
.feed-shared-social-counts             /* Engagement counts */
```

### Profile

```css
.pv-text-details__left-panel          /* Profile name/headline */
.pv-top-card-profile-picture          /* Profile photo */
.pvs-list__outer-container            /* Experience/education sections */
```

## GitHub (github.com)

### Repository

```css
.repository-content                    /* Main repo content area */
.markdown-body                         /* README / Markdown content */
[data-testid="latest-commit"]          /* Latest commit info */
.file-navigation                       /* File browser */
```

### Issues & PRs

```css
.js-issue-title                        /* Issue/PR title */
.comment-body                          /* Comment text */
[data-testid="issue-status-badge"]     /* Status badge */
```

## Medium (medium.com)

```css
article                                /* Article container */
h1[class*="title"]                     /* Article title */
[data-testid="storyReadTime"]          /* Read time estimate */
section[data-field="body"]             /* Article body */
```

## YouTube (youtube.com)

```css
#video-title                           /* Video title */
#description                           /* Video description */
#comment-content                       /* Comment text */
ytd-video-renderer                     /* Video result item */
```

## Amazon (amazon.com)

```css
#productTitle                          /* Product name */
.a-price-whole                         /* Price (dollars) */
#averageCustomerReviews                /* Rating section */
#feature-bullets                       /* Product features list */
```

## eBay (ebay.com)

```css
.x-item-title                          /* Item title */
.x-price-primary                       /* Current price */
.ux-seller-section__item               /* Seller info */
```

## Generic Selectors

### Common Patterns

```css
/* Navigation */
nav, header, [role="navigation"]
.navbar, .header, .menu

/* Main content */
main, [role="main"], article
.content, .main, .container

/* Forms */
form, input, textarea, select, button
[type="text"], [type="email"], [type="submit"]

/* Lists */
ul, ol, li
.list, .items, [role="list"]

/* Buttons */
button, [type="button"], [type="submit"]
.btn, .button, a[role="button"]

/* Modals & Popups */
[role="dialog"], .modal, .popup
.overlay, [aria-modal="true"]

/* Loading indicators */
.loading, .spinner, [aria-busy="true"]
```

### Data Attributes (common patterns)

```css
[data-testid="..."]                    /* Test IDs (React Testing Library) */
[data-cy="..."]                        /* Cypress test selectors */
[data-test="..."]                      /* Generic test attributes */
[data-id="..."]                        /* Custom ID attributes */
```

## Tips for Finding Selectors

### 1. Use Browser DevTools

Right-click element → Inspect → Copy Selector

### 2. Prefer Stable Selectors

**Good (stable):**
```css
[data-testid="submit-button"]
#user-profile
.product-card
```

**Bad (fragile):**
```css
div > div > div:nth-child(3)
.css-1x2y3z4
```

### 3. Test with `actionbook browser eval`

```bash
# Check if selector exists
actionbook browser eval 'document.querySelector("[data-testid=\"tweet\"]") !== null'

# Count matching elements
actionbook browser eval 'document.querySelectorAll("article").length'

# Extract all text from matches
actionbook browser eval 'Array.from(document.querySelectorAll(".post")).map(p => p.innerText)'
```

### 4. Use Multiple Selectors as Fallback

```javascript
const selectors = [
  '[data-testid="tweetText"]',
  '.tweet-text',
  'article p'
];

for (const sel of selectors) {
  const el = document.querySelector(sel);
  if (el) return el.innerText;
}
```

## Common Pitfalls

### Shadow DOM

Some sites use Shadow DOM (custom elements). Regular selectors won't work:

```javascript
// ❌ Won't work
document.querySelector('my-component .inner-element')

// ✅ Need to pierce shadow root
document.querySelector('my-component').shadowRoot.querySelector('.inner-element')
```

### Dynamic Content

Wait for elements to appear:

```bash
actionbook browser wait '[data-testid="content-loaded"]'
actionbook browser eval 'document.querySelector("[data-testid=\"content-loaded\"]").innerText'
```

### Infinite Scroll

Scroll to load more content:

```javascript
window.scrollTo(0, document.body.scrollHeight);
// Wait, then extract
```

### iframes

Content inside iframes requires switching context:

```javascript
const iframe = document.querySelector('iframe').contentWindow.document;
iframe.querySelector('.inner-content').innerText;
```
