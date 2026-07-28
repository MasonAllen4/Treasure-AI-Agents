# Media Re-Engagement - Campaign Plan

## Campaign Overview
- **Goal:** Re-engage lapsed users
- **KPI:** Reactivation rate (% of at-risk subscribers who play content within 14 days of email)
- **Target:** 14% reactivation rate

## Industry Context
- **Industry:** Media
- **Data Source:** Default data
- **Key considerations:** Media subscribers churn fastest when content consumption drops - re-engagement windows are narrow and personalized content recommendations dramatically outperform generic win-back messages. First-party behavioral data (watch history, genre preferences, subscription status) is the critical differentiator for this campaign type.

## Campaign Direction
This campaign targets Media subscribers whose subscription expires within 14 days and who have had no content plays in 30+ days - the highest-intent window for re-engagement. The strategy leads with AI-personalized content picks surfaced from each subscriber's own viewing history, paired with a low-friction "Resume Watching" CTA rather than a renewal prompt. The tone is value-focused ("here's what you're missing") rather than urgency-first, which reduces churn defensiveness.

## Audience

### Parent Segment
- **Type:** Full audience profile
- **Data foundation:** Combined consumption + subscription + engagement data
- **Tables used:** `subscriber_profiles`, `content_consumption`, `subscription_billing`, `email_engagement`
- **Key attributes:** `first_name`, `subscription_tier`, `subscription_expiry_date`, `last_content_play_date`, `genre_preferences`, `last_content_played`

### Target Segments
- **At-risk subscribers:**
  - Rule: `subscription_expiry_date <= NOW() + 14 days AND last_content_play_date < NOW() - 30 days`
  - Description: Active subscribers approaching renewal who have gone quiet on content consumption - highest re-engagement leverage before churn

## Email Template
- **Subject line:** *Still subscribed? Your top picks are waiting*
- **Preview text:** *Based on what you loved watching*
- **Personalization variables:**
  - `{{profile.first_name}}` - greeting personalization (default: "there")
  - `{{profile.subscription_tier}}` - plan-level messaging (default: "Subscriber")
  - `{{profile.days_until_expiry}}` - urgency signal in hero and CTA (default: "soon")
  - `{{profile.last_content_played}}` - content recommendation anchor
- **Layout sections:** Header with logo → Hero image + headline → Content recommendations grid (3 titles) → CTA button → Footer
- **Conditional content:** None - single version for all recipients
- **HTML file:** `./media-reengagement-template.html`

## Campaign Settings
- **UTM Parameters:**
  - utm_source: `treasure_data`
  - utm_medium: `email`
  - utm_campaign: `media-reengagement-at-risk`
  - utm_content: `reengagement-v1`

## Optimization Suggestions
- **A/B test:** Subject line A (*Expires soon + what you're missing*) vs. B (*Top picks are waiting*) - test urgency-led vs. content-led framing; measure open rate + click-to-reactivation
- **Suppression rules:** Exclude subscribers emailed in last 7 days, unsubscribed users, hard-bounced addresses, and already-renewed accounts
- **Preheader optimization:** *"Based on what you loved watching"* - keep under 85 characters; avoid repeating subject line words
- **Dynamic content (next iteration):** Add genre-based content recommendations using `{{profile.genre_preferences}}` for drama, documentary, sport variants
- **Follow-up campaign:** Re-send to non-openers at Day 3 with Subject A (urgency variant); send a final renewal reminder at Day 7 to non-clickers with a plan discount offer

---
*Campaign plan finalized during guided planning flow. This is for demo purposes only - no changes have been made to any data or environment.*
