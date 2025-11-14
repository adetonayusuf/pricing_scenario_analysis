# pricing_scenario_analysis

# Dynamic Discounting Scenario Modeling - Power BI | Advanced DAX | Business Impact Analysis

## Overview

This project delivers a Dynamic Discounting Scenario Dashboard that models how various discount rates and demand changes affect total profits, revenue, and margins. It enables executive teams to simulate financial outcomes before implementing pricing strategies.

## Purpose

To visually communicate how your data model supports scenario-based decision-making, showing the relationships between fact and dimension tables and their role in DAX calculations.

## Diagram Layout(Data Modelling)

![Modelling](https://github.com/adetonayusuf/pricing_scenario_analysis/blob/main/Scenario%20Data%20Modeeling%20modelling.png)


## Business Use-Case

Organizations often make discounting decisions without quantifying revenue vs. margin trade-offs. This dashboard fills that gap by providing:

- Profit simulations
- Cumulative scenario vs. forecast analysis
- Dynamic demand modelling
- Product-level segmentation
- High-level KPI performance indicators

## Dashboard Capabilities

- Discount parameter (-X%)
- Demand uplift parameter (+Y%)
- Cumulative profit & revenue calculations
- Full forecast vs scenario variance engine
- Executive-friendly visualization design

  ![scenarios](https://github.com/adetonayusuf/pricing_scenario_analysis/blob/main/Product%20Sales%20Scenarios%20Dashbaord(Discount).png)

## Key DAX Measures Included in This Repository
### CUMULATIVE PROFIT ENGINE
    Cumulative 2017 Profits =
      CALCULATE(
      [All 2017 Forecast Profits],
      FILTER(
        ALLSELECTED(Dates),
        Dates[Date] <= MAX(Dates[Date])
    )
    )

    Cumulative 2017 Scenario Profits =
    CALCULATE(
      [2017 Scenario Profits],
      FILTER(
        ALLSELECTED(Dates),
        Dates[Date] <= MAX(Dates[Date])
      )
    )

    Cumulative Performance =
    [Cumulative 2017 Scenario Profits] - [Cumulative 2017 Profits]

## DISCOUNTING & DEMAND IMPACT
    2017 Discounted Sales =
      CALCULATE(
        SUMX(
          Sales,
          (Sales[Quantity] * (1 + [Demand Change Value])) *
          (RELATED(Products[Current Price]) * (1 + [Discounting Change Value]))
        ),
          DATEADD(Dates[Date], -1, YEAR)
    )

    2017 Non Discounted Sales =
      CALCULATE(
        SUMX(
          Sales,
          (Sales[Quantity] * (1 + [Demand Change Value])) *
          RELATED(Products[Current Price])
      ),
      EXCEPT(ALL(Products[Product Name]), VALUES(Products[Product Name])),
        DATEADD(Dates[Date], -1, YEAR)
    )

## SCENARIO ENGINE
    2017 Scenario Sales = 
      [2017 Discounted Sales] + [2017 Non Discounted Sales]

    2017 Scenario Profits = 
    [2017 Scenario Sales] - [All 2017 Forecast Costs]

    Scenario Profit Margins =
      DIVIDE([2017 Scenario Profits], [2017 Scenario Sales], 0)

## FORECAST ENGINE
    All 2017 Forecast Costs =
      CALCULATE(
        [Total Costs],
        DATEADD(Dates[Date], -1, YEAR),
          ALL(Products)
    )

    All 2017 Forecast Profits =
    CALCULATE(
      [Total Profit],
      DATEADD(Dates[Date], -1, YEAR),
      ALL(Products)
    )

    Forecast Profit Margins =
    DIVIDE([All 2017 Forecast Profits], [All 2017 Forecast Sales], 0)

## Outcomes & Executive Impact

This solution enables leaders to:

- Identify the optimal discount level
- Protect and grow margins
- Forecast profit changes before launching pricing campaigns
- Understand product sensitivity to pricing
- Make data-driven pricing decisions

It transforms pricing strategy from guesswork into a repeatable, data-backed decision framework.
