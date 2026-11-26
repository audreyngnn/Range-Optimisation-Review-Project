# Range Review Dashboard: Did the five range reviews work?

An interactive, single-file HTML dashboard that evaluates five supermarket range reviews (Coffee, Baby food, Cat food, Ice cream, Sunscreen) across 15 stores, built during a Range & Space work simulation.

**Live demo:** `https://audreyngnn.github.io/range-review-dashboard/` (after enabling GitHub Pages, see below)

## The question

A Head of Category wanted to know whether each range review (changing which products are on the shelf and how much shelf space each gets) actually improved sales, and if not, where the problems are and what to do next.

## Key findings

| Category | Raw change | Benchmarked result | Verdict |
|---|---|---|---|
| Coffee | −0.9% | −3.8% (excl. leftover stock) | No |
| Baby food | +3.2% | +3.0% (excl. leftover stock) | Small gain |
| Cat food | +4.7% | +4.4% (units −1.7%) | Partly |
| Ice cream | +43.0% | 0.0 pts vs same weeks last year | No effect |
| Sunscreen | −52.5% | +2.1 pts vs same weeks last year | Small gain |

**What to do first**

1. **Cat food:** find out why Kitbury fell 25% (space explains only part of it) and give budget stores their own shelf plan. About $47k a year at stake.
2. **Coffee:** close the capsule gap. Shoppers of the removed Crema Lane Capsules did not switch to the remaining capsule. About $41k a year at stake.
3. **All categories:** fix how reviews are measured. Three of five raw results were misleading: seasonal categories must be compared with last year, and leftover stock of removed products must be excluded.

Annual figures are rough estimates (weekly gap × 52, assuming the gap continues).

## What the dashboard shows

- **Overview:**
  - the main finding, the top 3 priorities and a results table for all five categories;
  - a clickable map of Australia comparing each state with all 15 stores, always shown with the store count (SA and TAS have only one store each).
- **One tab per category:** a summary and verdict, category, brand, product and store level views, and three prioritised recommendations.
- **Filters:**
  - state, store and brand;
  - for the two seasonal categories, a switch between "vs category, same weeks" and "vs same weeks last year".

## Method

- **Windows:** N weeks before and N weeks after each review date, where N is the category's review period (13 or 26 weeks). The review day counts as "after".
- **Weekly averages:** total ÷ N. A missing day counts as $0.
- **Space:** product shelf length (cm) in the month before the review vs the review month.
- **Benchmarks:**
  - Seasonal categories (Ice cream, Sunscreen): growth minus growth in the same weeks one year earlier, a period with no review.
  - Coffee, Baby food and Cat food: growth excluding leftover stock (products removed from the shelf plan that kept selling). The data is too short for a 26 week year-ago comparison.
- **Store gap:** dollars per week a store sold above or below what it would have sold growing at the all-store rate (or at its own last-year rate, for seasonal categories).
- **Validation:**
  - every query was reconciled against the source database;
  - no other review falls inside any comparison window;
  - lagging stores were checked for closures (none found).

## Caveats

- **Missing context:** the data has no prices, promotions, stock levels or competitor information. Store and brand findings are questions to ask, not conclusions.
- **Inferences:** explanations such as "shoppers switched to other products" are inferences, and annual dollar figures are estimates, not recoverable amounts.
- **Small state samples:** state results are based on 1 to 4 stores per state.

## Tech

- **PostgreSQL:** CTEs, `FILTER`, window functions and `FULL OUTER JOIN` to build store × product before/after tables.
- **Python:** exports the results as JSON embedded in the page.
- **Front end:** plain HTML, CSS and JavaScript. No libraries, no server, works offline.
- **Map:** state boundaries from [Natural Earth](https://www.naturalearthdata.com/) (public domain).

## Run it

Open `index.html` in any browser. To publish it as a website:

1. Go to **Settings → Pages**.
2. Choose **Deploy from a branch**, then `main` and `/ (root)`.

## Author

Audrey
