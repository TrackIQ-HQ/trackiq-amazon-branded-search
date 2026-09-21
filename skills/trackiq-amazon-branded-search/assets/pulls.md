# The pull sequence

## 0. Account and terms

`list_marketplaces` first. Never print `account_id`. If more than one
TrackIQ MCP is connected, call it on each and match on `name`.

Read the Brand terms block from account.md. If it is empty, ask for the brand
name, common misspellings and product-line names before pulling anything.

Window: a trailing 30 days.

## 1. The pulls

| # | Call | Arguments | Gives you |
|---|---|---|---|
| 1 | `get_search_terms` | `ad_type='sp'`, `sort='spend DESC'` | customer query, spend, sales, orders — SP, 7-day window |
| 2 | `get_search_terms` | `ad_type='sb'`, `sort='spend DESC'` | the same for SB, 14-day window |
| 3 | `get_targets` | `record_type='KEYWORD'`, `ad_type='all'`, `state='enabled'` | the keywords the account bids on, to spot brand keywords with no search volume |
| 4 | `get_search_query_performance` | the top 10 branded queries by spend | the brand's organic purchase share on its own name |

## 2. Why SP and SB are separate pulls

`ad_type='all'` returns one ranking with each row tagged by channel — and
one ROAS blending a 7-day and a 14-day attribution window. Summing across
the two inflates SB against SP. Keep two tables, one per channel, and a
spend-only combined view where windows do not matter.

## 3. Paginate — the limit is binding

Search terms are a long tail, and the tail is almost all generic. Page with
`offset` until a call returns fewer rows than the limit. Stopping early makes
brand look like a bigger share of spend than it is.

## 4. What the search-term report will not tell you

`get_search_terms` returns the query and its metrics — no campaign, ad group
or match type. The split is by what the shopper typed, which is the right
question here. It cannot say which keyword caught the query.

## 5. Search Query Performance

`get_search_query_performance` covers organic and paid together and is
reported weekly. Use the brand's **purchase share** on its own branded
queries — the share of all purchases on that search that went to the brand.
If it is not available for a query (SQP is sparse on small brands), say so
for that row rather than estimating it.
