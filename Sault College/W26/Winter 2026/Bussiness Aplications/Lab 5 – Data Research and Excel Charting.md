# Data Organization in Excel

## Spreadsheet Structure

**Sheet 1: Cities** This sheet organizes geographic and demographic data to analyze market presence.

|Column|Data Type|Purpose|
|---|---|---|
|City|Text|Northern Ontario cities|
|Population|Number|Demographic baseline|
|Tim Horton's|Number|Store count per city|
|Starbucks|Number|Store count per city|
|Country Style|Number|Store count per city|

**Cities included:** Sault Ste. Marie (pop. 81,225), Sudbury (194,123), North Bay (52,662), Timmins (45,065), Thunder Bay (109,140)

**Sheet 2: Franchises** This sheet compares business costs across competitors.

|Column|Data Type|Purpose|
|---|---|---|
|Coffee Shop|Text|Company name|
|Average Cost|Currency|Typical franchise investment|
|Royalty Fees|Percentage/Currency|Ongoing payments|
|Advertising Fees|Percentage/Currency|Marketing contributions|
|# of Stores|Number|Total locations in Canada|

# Per Capita Analysis

**What it is:** [[Per Capita Analysis]] means calculating a ratio "per person" to compare across populations of different sizes.

**How it's used here:** You divide the number of Tim Hortons stores by the city's population to determine stores per person (or per capita).

# Data Visualization Types

## Column Charts (3D)

**What they are:** [[Bar Charts]] (or [[Column Charts]]) display data using vertical or horizontal bars, where bar height represents value.

**Why 3D?** Adds visual depth, though it's primarily aesthetic—2D charts are often clearer for precise comparisons.

## Pie Charts

**What they are:** [[Pie Charts]] display data as slices of a circle, where each slice represents a proportion of the whole.

> [!NOTE]
> Best for showing how parts contribute to a total (percentage distribution).

**Key insight:** Pie charts answer "what percentage of the total?" rather than "how many?"

# Formulas Used

**Per Capita Calculation:**

```
Per Capita Ratio = Number of Stores / City Population
```

**Example:**

```
Tim Hortons Per Capita (North Bay) = Tim Hortons Count / 52,662
```

This produces a decimal representing stores per person (e.g., 0.00019 = approximately 1 store per 5,263 people).

# Tags

#business-applications #excel #data-visualization #primary-research #franchises #data-analysis #spreadsheets