# Coffee data dictionary

All data are synthetic teaching observations, not published research data.
Historical observations solve a stable competitive market with varying buyer and growing conditions. They are independent selling periods, not calendar months, geographic markets or individual farms. No missing values are introduced. Files use commas, headers, and decimal points.

## coffee_market.csv — Sections 1–3
300 rows. `period_id`: string key; `period_index`: display index; `price_usd_kg`: wholesale USD/kg; `quantity_kt`: thousand tonnes per selling period; `growing_conditions`: local growing-window index (-1.5 unfavorable, 0 normal, 1.5 favorable); `buyer_activity`: centered foreign activity index, zero at reference conditions. Indices have no currency units. Weather relates to the crop sold, not contemporaneous consumer weather.

## coffee_episodes.csv — Section 4
40 rows: two episodes × two phases × ten observations. Key is (`episode`, `phase`, `observation`). `episode`: A or B; `phase`: Before or During; `observation`: observation number within cell, not a matched pair ID. The other four columns have the historical meanings/units. Do not add these rows to the demand estimation sample.

## coffee_forecast_scenarios.csv — first part of Section 5
Two rows: `scenario`, `release_kt`, `buyer_activity`, `explanation`. Each release is harvested, graded and committed to sale within a shorter window. No storage or replacement supply is available. Buyer activity is zero. Use the estimated demand relation to predict its clearing price, conditional on that horizon and stable demand.

## coffee_forecast_reveal.csv — open AFTER recording predictions
80 rows: 40 independent realizations per scenario. Key is (`scenario`, `observation`). `quantity_kt` is the scenario's committed volume; `buyer_activity` is zero; `price_usd_kg` is its realized clearing price. Observations in different scenarios are NOT matched pairs. Do not estimate or recalibrate demand with this file.

## Unit conversion and accounting
One thousand tonnes is one million kilograms. Consequently price_usd_kg × quantity_kt gives **million USD** of gross market sales revenue. Calculate period revenue first, then average. E[PQ] need not equal E[P]E[Q]. There are no production costs, farmer-specific quantities, or consumer utility data. Market revenue does not measure profit or welfare.
