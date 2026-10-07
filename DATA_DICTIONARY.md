# Processed data dictionary

All three CSV files use UTF-8 and include a header row. Dates represent calendar months.

| Variable | Meaning |
| --- | --- |
| `month` | Month in `YYYY-MM` format, 2011-01 through 2025-12 |
| `city` | Beijing, Shanghai, Hangzhou, Guangzhou, Shenzhen or Chengdu |
| `housing_type` | `new` or `second_hand` |
| `housing_return` | `log(official month-on-month housing index / 100)`, rounded to eight decimal places |
| `stock_return` | Log change in CSI 300 closing value between the last available observations of consecutive months |
| `direction` | Stock-return direction label used by the Rmd: `up`, `down`, or `flat` |
| `lag1_return` | Stock log return one month before `month` |
| `lag2_return` | Stock log return two months before `month` |
| `lag3_return` | Stock log return three months before `month` |

`csi300_monthly.csv`: one row per month; 180 rows. Columns: month, stock_return, direction, lag1_return, lag2_return, lag3_return.

`housing_monthly.csv`: one row per month × city × housing type; 2,160 rows. Columns: month, city, housing_type, housing_return.

`analysis_panel.csv`: the housing table joined to stock variables by month; 2,160 rows. The same monthly stock values therefore appear for every city and housing type in that month.

Returns are decimal log changes, not percentages. For illustration only, an index of 101 yields log(1.01), approximately 0.00995. Housing changes reflect the official index methodology, not changes in the city's mean transaction price.
