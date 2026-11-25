---
name: adspirer-search-performance-review
description: "Read-only Google Ads and Microsoft Advertising reporting, scorecards, conversion checks, and evidence-backed recommendations. Use when the user asks how their search campaigns are performing or wants a weekly or monthly report."
---

# Performance review

Load adspirer-search-mcp. This skill never changes campaigns.
Check get_connections_status and select the intended account before reading data.

## Sources

Google: get_campaign_performance if advertised, plus discovered google_ads_read reports. Microsoft: discover bing_ads_read operations such as get_microsoft_campaign_performance and the analyze_microsoft_* insights; its metrics and attribution are not identical to Google's.
Use raw_data only if the actual schema accepts it; do not assume widget rendering.

## Trust the numbers

Confirm dates, timezone, currency, conversion definition, and attribution window. Distinguish
partial days, conversion lag, missing permissions, and tracking failures from real declines.
Run audit_conversion_tracking where relevant and supported. A tracking gap limits affected
conversion claims; it does not automatically invalidate independently measured spend.
Do not combine incompatible currencies or double-count cross-platform attributed conversions.

## Scorecard and interpretation

Show spend, pacing, conversions, CPA, ROAS when revenue exists, CTR/CPC, and comparison with
an equivalent prior window. Compute blended CPA from comparable totals, not average platform CPAs.
Lead with the largest supported problem and opportunity, with evidence and caveats.
Discover available anomaly tools, but treat their explanations as hypotheses unless supported.
Recommend actions; hand approved changes to adspirer-search-optimize.

## Repeating reviews

Offer a host schedule only when supported and authorized, explaining quota usage.
This endpoint does not imply access to a server-side monitoring router. Do not claim that a
report is scheduled until an actual scheduler confirms it. No fabricated figures or trends.

## Default review

Use the platform and period the user gave. With none given, cover every connected ad platform for
the last 30 complete days, compared with the 30 days before.

1. Call get_connections_status. Work only on connected platforms and their active accounts. If
   more than one account could be meant, ask which one.
2. Google Ads: call get_campaign_performance. For the reason behind a change, run
   explain_performance_anomaly through google_ads_read.
3. Microsoft Advertising: through bing_ads_read, run get_microsoft_campaign_performance, and
   analyze_microsoft_impression_share when impression share is part of the story.
4. Show one scorecard per platform: spend, impressions, clicks, CTR, average CPC, conversions,
   cost per conversion, ROAS where revenue is tracked, and the change against the previous period.
   Keep currencies separate. Compute ratios from totals, not from averages of rows.
5. List the three findings that matter most, each with the campaign and the numbers behind it,
   then at most three recommended actions.
6. Say what limits the numbers: partial days, conversion lag, or tracking gaps. If conversions
   look wrong, suggest audit_conversion_tracking.

A review changes nothing. If the user wants to act on a recommendation, describe the exact
change, wait for their approval, and follow adspirer-search-optimize.
