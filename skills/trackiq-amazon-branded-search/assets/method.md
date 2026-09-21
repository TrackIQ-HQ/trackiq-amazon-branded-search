# Method

## 1. Normalise

Lowercase the query, collapse whitespace, strip punctuation except hyphens.
Normalise the brand and competitor terms the same way.

## 2. Classify, in this order

1. **Product targeting** — the query matches `^b0[a-z0-9]{8}$`.
2. **Branded** — the query contains any brand term or misspelling as a whole
   word or whole phrase. Product-line names count as branded.
3. **Competitor** — the query contains any competitor brand term.
4. **Generic** — everything else.

A query containing both a brand and a competitor term is **branded** — the
shopper named the brand.

Whole-word matching matters. A brand called "Glow" must not claim
"glow in the dark stickers"; check the ten largest branded queries by eye
and add exclusions to account.md when it misfires.

## 3. Per bucket, per channel

Spend, sales, orders, ROAS, ACOS, share of channel spend, share of channel
sales. Then a combined **spend-only** view across SP and SB.

- **Generic ROAS** is the headline.
- **Blended ROAS** is shown beside it, labelled, for reference.
- **The brand lift**: blended ROAS minus generic ROAS. This is how much brand
  search is flattering the account average.

## 4. Is the brand spend defence?

For the ten branded queries with the most spend, read the brand's organic
purchase share from Search Query Performance.

| Organic purchase share on its own name | Reading |
|---|---|
| 80% or more, no competitor in the branded queries | Mostly harvesting. Recommend a two-week test at reduced bids on exact brand terms, measuring total brand sales, not ad sales. |
| 50–80% | Mixed. Keep it and watch. |
| Under 50%, or a competitor appears in the branded queries | Defence. Keep it. |

Never recommend a cut. Recommend a test with a stated success measure.

## 5. Competitor conquesting

Competitor-bucket ROAS against generic ROAS. Conquesting usually converts
worse; the question is whether it recruits new customers. If
`trackiq-amazon-amc-ntb-campaigns` has been run, cite the new-to-brand share
of the conquest campaigns. Otherwise say it is unknown.

## 6. Brand keywords with no search volume

From `get_targets`: enabled keywords that contain a brand term but match no
query in the window. Usually harmless, sometimes a sign the brand name is
spelled a way shoppers do not use.
