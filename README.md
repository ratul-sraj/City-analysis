# International Air Freight Analysis — Australian Ports

**Python · Pandas · Matplotlib**

Cleaned and analysed **89,320 monthly records (1985–2025)** of international
traffic across **19 Australian ports**: date conversion, missing-value and
duplicate checks.

Aggregated freight, mail and passenger volumes by port and year to chart
long-term trends and identify each port's top trading partner — **Singapore for
6 of 19 ports**.

## Data

`city_pairs.csv` — 89,320 rows × 15 columns, one row per month per
Australian-port / foreign-port pair.

| | |
|---|---|
| Records | 89,320 |
| Period | January 1985 – 2025 (41 years) |
| Australian ports | 19 |
| Foreign ports | 200 |
| Countries | 78 |
| Missing values | 0 |
| Duplicate rows | 0 |

Columns: `Month`, `AustralianPort`, `ForeignPort`, `Country`, and in/out/total
measures for `Passengers`, `Freight_(tonnes)` and `Mail_(tonnes)`, plus `Year`
and `Month_num`.

Source: Kaggle — *International Airlines Traffic by City Pairs*.

## What the analysis does

1. **Load** the raw CSV and inspect its shape and structure.
2. **Convert dates** — `Month` arrives as a string (`Jan-85`); parsed with
   `pd.to_datetime(..., format="%b-%y")`.
3. **Check data quality** — no missing values and no duplicate rows, so no rows
   are dropped or imputed.
4. **Aggregate** freight and passenger volumes by port and year.
5. **Chart long-term trends** — freight by year for the seven largest ports, with
   a marker at 2020 to show the COVID-19 impact.
6. **Chart mail** — monthly mail-in volume for the highest-mail port, with a
   marker at March 2020.
7. **Identify top trading partners** — the foreign port with the greatest total
   freight for each Australian port.

## Findings

**Top trading partner per Australian port** (by total freight, 1985–2025):

| Foreign port | Australian ports for which it ranks first |
|---|---|
| **Singapore** | **6** |
| Auckland | 5 |
| Hong Kong | 3 |
| Denpasar | 2 |
| Jakarta, Kuala Lumpur, Osaka | 1 each |

Singapore is the largest single partner overall, ranking first for Adelaide,
Brisbane, Canberra, Darwin, Melbourne and Perth.

The seven largest ports by outward freight are Sydney (5,775,543 t), Melbourne
(3,874,944 t), Brisbane (1,683,571 t), Perth (1,349,917 t), Adelaide (337,273 t),
Cairns (181,250 t) and Darwin (20,405 t).

## Running it

```bash
pip install -r requirements.txt
jupyter notebook AustaraliaPorts.ipynb
```

The notebook reads `city_pairs.csv` by relative path — the dataset is committed
in this repo, so it runs from a fresh clone with no download step.

## Layout

```
AustaraliaPorts.ipynb   the analysis, executed with outputs and charts saved
city_pairs.csv          the dataset
requirements.txt
```

## Notes

- **Mail volumes are tiny for most ports.** 6 of the 19 ports received no mail
  freight at all across 41 years (Broome, Gold Coast/Coolangatta, Newcastle,
  Port Hedland, Toowoomba Wellcamp, Townsville), and 8 total under one tonne
  for the whole period. Sydney alone accounts for 417,989 t — 63% of the
  664,785 t total — so "top mail port" is a far weaker statement than "top
  freight port".
- **Volumes span five orders of magnitude** — from 5.78 million tonnes for Sydney
  down to 0.17 tonnes for Broome. Charts show the largest ports; ports at the
  bottom of that range are effectively invisible on a shared linear axis.
- The top-partner comparison uses `Freight_Total_(tonnes)`. Ranking by passenger
  volume gives the same answer — Singapore first for 6 of 19 — but ranking by
  mail gives Singapore only 3, since mail follows different routes.
