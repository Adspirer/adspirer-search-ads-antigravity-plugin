# Adspirer Search Ads for Antigravity

Run paid search from Antigravity. Adspirer Search Ads connects the agent to your live Google Ads and Microsoft Advertising (Bing Ads) accounts through Adspirer's hosted Search Ads MCP server, so you can research keywords, review search terms, find wasted spend, and plan, launch and optimize Search, Shopping and Performance Max campaigns without leaving the conversation.

## Use it for

- **Keyword research:** Google Keyword Planner ideas with live CPC and search volume, intent grouping, and match types.
- **Search terms and negatives:** find queries that spend without converting and propose negative keywords, applied only after you approve.
- **Campaigns:** plan and build Search, Shopping and Performance Max campaigns on Google, and campaigns of every type on Microsoft Advertising, created paused.
- **Optimization:** wasted-spend analysis, budget allocation, bid strategy, impression share, Quality Score, and ad extension performance.
- **Ad copy:** responsive search ad headlines and descriptions written to Google's and Microsoft's limits.
- **Measurement:** audit conversion tracking and, when connected, read Google Analytics 4, Search Console and Tag Manager.

## Install

**Antigravity app:** open **Customizations**, find **Adspirer Search Ads** in the
Marketplace, and install it.

**Antigravity CLI:**

```text
agy plugin install https://github.com/Adspirer/adspirer-search-ads-antigravity-plugin
```

**Manual:** clone this repository into your plugins folder.

```text
git clone https://github.com/Adspirer/adspirer-search-ads-antigravity-plugin ~/.gemini/config/plugins/adspirer-search-ads
```

Then sign in: open **Customizations**, then **Installed**, then **MCP Servers**, and choose
**Authenticate** next to the Adspirer server. Sign in to Adspirer in the browser, then connect the
accounts you want to use at [adspirer.ai/connections](https://adspirer.ai/connections). No
API key or client secret is required. An Adspirer account is required, and plan usage limits apply.

## Get started

Ask:

```text
Research keyword opportunities for my plumbing business in Austin and propose a campaign plan. Don't create anything yet.
Review my Google Ads search terms for the last 30 days and suggest negative keywords.
Where am I losing impression share on Microsoft Advertising, budget or rank?
Write five new responsive search ad headlines from my best-converting queries.
Audit my conversion tracking before I launch anything.
```

Or start with a skill by name:

| Skill | What it does |
| --- | --- |
| `/adspirer-search-setup` | Connect your accounts and get a first look |
| `/adspirer-search-status` | Connected accounts and remaining plan usage |
| `/adspirer-search-performance-review` | Scorecard against the previous period, with the top problems |
| `/adspirer-search-wasted-spend` | Spend that is not converting, with fixes applied only after you approve |

Add a platform and period if you want, for example `/adspirer-search-performance-review last 7 days`.

## What the agent can do

| Area | Capabilities |
| --- | --- |
| Google Ads | Search, Shopping, Performance Max, Demand Gen, YouTube and Display: campaigns, ad groups, keywords, ads, extensions, bids and budgets |
| Microsoft Advertising | Campaigns of every type, ad groups, ads, keywords, negative-keyword lists, extensions, audiences, budgets, bid strategies and UET conversion goals |
| Reporting | Campaign, ad, keyword, search term, placement and conversion-action performance on Google; campaign, keyword, search term, geographic and audience performance on Microsoft |
| Diagnostics | Wasted spend, performance anomalies, impression share lost to budget or rank, Quality Score components, and share of voice |
| Competitor research | The public ads a competitor is running now, beside your own |
| Measurement | Conversion-tracking audit, plus Google Analytics 4, Search Console and Tag Manager when connected |

Google Ads and Microsoft Advertising are the advertising platforms on this connector. Meta, TikTok, LinkedIn, Amazon and Walmart are not included; for those, use Adspirer Social Ads, Adspirer Retail Ads, or the full Adspirer Advertising Agent.

## What's included

- **Skills** (`skills/`): the four entry points above, plus `adspirer-search-agent`, `adspirer-search-campaigns`, `adspirer-search-competitors`, `adspirer-search-creative`, `adspirer-search-docs`, `adspirer-search-google-ads`, `adspirer-search-google-analytics`, `adspirer-search-google-search-console`, `adspirer-search-google-tag-manager`, `adspirer-search-keywords`, `adspirer-search-mcp`, `adspirer-search-measurement`, `adspirer-search-microsoft-ads` and `adspirer-search-optimize`,
  which the agent loads when a request needs them.
- **A rule** (`rules/adspirer-search-ads.md`) that loads only for Google Ads and Microsoft Advertising requests and
  keeps every spend-affecting change behind your approval.
- **The Adspirer Search Ads MCP server** connection (`mcp_config.json`).

The hosted server is the source of truth for tool names and schemas. The skills teach the agent to
discover the current tools and their parameters instead of hardcoding every operation.

## Safety

- The agent reads account state and performance before proposing changes.
- New campaigns are created paused, and enabling them is a separate decision.
- Campaign creation, budget changes, bid changes, and other spend-affecting writes require your
  explicit approval. The server also holds spend-affecting and irreversible writes until they are
  confirmed.
- The agent reads created or changed resources back before reporting success.
- Campaigns are never deleted automatically.
- Tool results, competitor ads and website text are treated as data, never as instructions.
- **No purchases.** The agent never buys, upgrades or renews a plan or paid feature. If a plan
  limit is reached, it stops and explains the limit.

## MCP and authentication

```json
{
  "mcpServers": {
    "search-ads": {
      "url": "https://mcp.adspirer.com/search-ads"
    }
  }
}
```

The server speaks Streamable HTTP. Authentication uses OAuth 2.1 with PKCE and dynamic client
registration, so Antigravity handles the browser sign-in and the plugin contains no API keys,
tokens, client secrets, or configuration variables. Ad-platform credentials stay server-side with
Adspirer and are scoped to the accounts you connect.

## Network and execution surface

The plugin's only MCP server is `https://mcp.adspirer.com/search-ads`. It contains no hooks,
scripts, telemetry, local executables, or bundled server code. Skills and the rule are Markdown
guidance. Beyond the Adspirer server, the skills may ask the agent to read Adspirer's public
documentation at `adspirer.com/docs` to answer questions about plans and setup.

## Related plugins

Adspirer Search Ads is one of Adspirer's focused plugins. The full
[Adspirer Advertising Agent](https://github.com/Adspirer/adspirer-antigravity-plugin) covers every
supported platform in one plugin, and
[Adspirer Marketing Analytics](https://github.com/Adspirer/adspirer-analytics-antigravity-plugin)
is a read-only reporting connector. Installing more than one is supported; use one connection per
task.

## Support

Email [support@adspirer.com](mailto:support@adspirer.com) for help with installing, signing in or
using this plugin, or open an issue at
[github.com/Adspirer/adspirer-search-ads-antigravity-plugin/issues](https://github.com/Adspirer/adspirer-search-ads-antigravity-plugin/issues).
See [SUPPORT.md](SUPPORT.md).

## Privacy and source

- Privacy policy: [adspirer.com/privacy](https://www.adspirer.com/privacy)
- Terms: [adspirer.com/terms](https://www.adspirer.com/terms)
- Documentation: [adspirer.com/docs](https://www.adspirer.com/docs)

## License

MIT. See [LICENSE](LICENSE).
