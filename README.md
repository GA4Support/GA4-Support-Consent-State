# GA4 Support Consent State — Google Tag Manager variable template

A variable template for Google Tag Manager that exposes the website visitor's
cookie choice, as made in the [GA4 Support Cookie
Banner](https://github.com/GA4Support/gtm-template-cookie-banner), to your other
tags. Use it to block or configure a tag per consent category.

Published in the Google Tag Manager Community Template Gallery.

## What it returns

Pick one of two shapes in the variable's settings:

| Setting | Returns |
|---|---|
| Every allowed category, pipe-delimited | `\|necessary\|analytics\|` — only the categories the visitor allowed |
| A single category | `granted` or `denied` |

The categories are `necessary`, `functional`, `analytics`, `marketing` and
`uncategorized`.

The pipe-delimited shape is meant for a *contains* condition — a trigger
exception on `|marketing|`, for example, blocks a tag for every visitor who did
not allow marketing cookies. The single-category shape is for a tag parameter or
a lookup table.

## Requirements

The GA4 Support Cookie Banner must be on the page: this variable reads the choice
that the banner stores. A GA4 Support account is needed for the banner, which is
included in every plan.

## Why it reads the cookie, not the dataLayer

A variable is read at the moment a tag fires. For a returning visitor the stored
choice is already present on the very first hit, while the banner's dataLayer
events only arrive once the banner script has booted — so reading the stored
choice also answers for tags that fire early.

If you want to *trigger* on a consent change rather than read a value, you do not
need this template at all. The banner pushes `consent_update_analytics`,
`consent_update_marketing`, `consent_update_functional` and
`consent_update_complete` to the dataLayer, and a standard Custom Event trigger
picks those up.

## A note on refused consent

Anything that is not an explicit yes is treated as a no. A stored choice that
holds something other than a real boolean — from an older version, another script,
or a tampered browser — never grants permission. This is deliberate: in
JavaScript every non-empty string is truthy, so a lenient check would hand out
permissions the visitor never gave.

## Documentation and support

- Installation guide: <https://cmp.ga4support.nl/gtm-template>
- Support: <support@ga4support.nl>

## Licence

Apache License 2.0 — see [LICENSE](LICENSE).
