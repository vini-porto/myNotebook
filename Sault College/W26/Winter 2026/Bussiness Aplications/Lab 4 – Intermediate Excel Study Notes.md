## Overview

This lab focuses on intermediate [[spreadsheet]] techniques that move beyond basic data entry. You'll learn to automate decisions using logic, perform financial calculations, visualize data, and use optimization tools. These skills are fundamental for business analysis, financial modeling, and data-driven decision-making.

---

## Main Concepts

### The IF Function

**What it is:** The [[IF function]] is a **logical function** that makes decisions based on conditions. It evaluates whether something is true or false, then returns different values accordingly.

**Why it matters:** Real-world data often requires conditional logic. For example, assigning letter grades based on percentages, determining scholarship eligibility, or categorizing temperatures as hot or cold. The IF function automates these decisions.

**Structure:** The IF function follows this pattern: check a condition, if true do one thing, if false do another thing.

**How it's used in this lab:**

- Converting percentage grades to letter grades (A+, A, B, C, D, F)
- Determining scholarship amounts based on performance thresholds
- Categorizing weather temperatures (Hot, Warm, Comfortable, Cold)

**Key principle:** You can **nest** IF functions inside each other to handle multiple conditions. This creates a decision tree where each condition is checked in sequence.

---

### Cross-Sheet References

**What it is:** [[Cross-sheet references]] allow one worksheet to pull data from another worksheet within the same workbook. Instead of duplicating information, you create links between sheets.

**Why it matters:** This keeps your workbook organized and maintains a single source of truth. If you update data in one location, all references automatically update. It's essential for creating organized, professional spreadsheets.

**How it's used in this lab:** The Grades sheet references data stored in the Legend sheet. When displaying scholarship information, the formula looks up text stored in specific cells on the Legend sheet, keeping the main grade sheet clean and the reference data separate.

**Syntax concept:** To reference another sheet, you use the format: `SheetName!CellAddress`

---

### The AVERAGE Function

**What it is:** The [[AVERAGE function]] is a [[statistical function]] that calculates the arithmetic mean of a set of numbers. It adds all values and divides by the count.

**Why it matters:** Averages are fundamental to data analysis. Whether calculating student grades, temperature trends, or business metrics, averages provide a central tendency that summarizes data.

**How it's used in this lab:**

- Computing a student's overall grade average across multiple courses
- Finding the average temperature over a 10-day forecast

**Important note:** The AVERAGE function automatically ignores text and empty cells, counting only numeric values.

---

### The PMT Function

**What it is:** The [[PMT function]] is a **financial function** that calculates periodic payment amounts for loans or investments. It considers the principal amount, interest rate, and number of payment periods.

**Why it matters:** This is essential for financial planning. Whether you're buying a car, calculating mortgage payments, or planning business financing, the PMT function shows exactly how much you'll pay each period.

**How it's used in this lab:** Calculating monthly car payments based on:

- Loan amount (purchase price)
- Interest rate (annual percentage rate)
- Term length (number of months)

**Real-world application:** Banks and financial institutions use this exact calculation to determine loan payments. Understanding it helps you make informed financial decisions.

---

### Goal Seek Tool

**What it is:** [[Goal Seek]] is an **optimization tool** that works backward. You specify a desired result, and Excel automatically adjusts an input value to achieve that result.

**Why it matters:** Often you know what outcome you want but need to determine what input will get you there. Goal Seek automates trial-and-error, finding the precise value needed.

**How it's used in this lab:** You want a car payment of exactly $200 per month. Goal Seek adjusts the loan term (number of months) until the payment matches your target. Instead of manually trying different values, Goal Seek finds the answer instantly.

**The process:**

1. Set up your formula with the desired outcome cell
2. Tell Goal Seek what value you want that cell to show
3. Specify which input cell should be changed
4. Let Excel calculate the required input value

---

### Conditional Formatting

**What it is:** [[Conditional formatting]] automatically applies visual formatting (colors, fonts, borders) to cells based on their values. The formatting changes dynamically as data changes.

**Why it matters:** Visual cues make patterns and outliers immediately apparent. Instead of reading through numbers, you can see hot temperatures in red and cold ones in blue at a glance. This accelerates data analysis and decision-making.

**How it's used in this lab:** The weather forecast uses conditional formatting to visually distinguish between cold and warm temperatures for January, making temperature trends easy to spot.

**Common uses:**

- Highlighting values above or below thresholds
- Color scales showing high to low values
- Data bars providing visual magnitude comparison
- Icon sets (arrows, traffic lights) indicating performance

---

### Charts and Data Visualization

**What it is:** [[Charts]] transform numerical data into visual representations like lines, bars, or pies. They reveal trends, comparisons, and patterns that aren't obvious in raw numbers.

**Why it matters:** Humans process visual information faster than tables of numbers. Charts make data accessible to non-technical audiences and support data-driven storytelling.

**How it's used in this lab:** Creating a **line chart** to visualize temperature trends over the 10-day forecast period. Line charts are ideal for showing change over time.

**Chart elements:**

- **Axis labels** identify what each axis represents
- **Data series** are the actual lines or bars showing values
- **Legend** identifies different data series
- **Title** describes what the chart shows

---

### Absolute References

**What it is:** [[Absolute references]] lock a cell reference so it doesn't change when you copy a formula. They use dollar signs ($) to fix the row, column, or both.

**Why it matters:** When applying the same calculation to multiple rows, you often need one value (like a tax rate or growth percentage) to remain constant while other references adjust. Absolute references make this possible.

**How it's used in this lab:** Calculating 2026 rent increases using a single 4% rate stored in one cell. When the formula is copied down for multiple properties, the reference to the 4% rate stays locked while the 2025 rent amounts change.

**Syntax:**

- `$A$1` – locks both row and column (fully absolute)
- `$A1` – locks column only
- `A$1` – locks row only
- `A1` – no locks (relative reference)

---

### Sorting Data

**What it is:** [[Sorting]] rearranges rows of data based on values in one or more columns. You can sort alphabetically, numerically, by date, or by custom orders.

**Why it matters:** Sorted data is easier to analyze, search, and present. Whether organizing student names alphabetically or financial data by amount, sorting creates order from chaos.

**Common applications:**

- Ranking students by grades
- Organizing transactions by date
- Listing products by price
- Alphabetizing customer lists

---

### Worksheet Organization

**What it is:** [[Worksheet organization]] involves structuring workbooks with multiple sheets, each serving a specific purpose. Sheets are renamed with meaningful labels, and data is logically separated.

**Why it matters:** Well-organized workbooks are easier to navigate, understand, and maintain. Separating raw data, calculations, and reference tables prevents errors and improves clarity.

**How it's used in this lab:**

- **Grades sheet** – contains student course grades and calculations
- **Legend sheet** – stores reference data like grading scales and scholarship criteria
- **Weather sheet** – holds forecast data and visualizations
- **Vehicle sheet** – contains loan payment calculations
- **Rent sheet** – manages rent increase calculations

**Best practice:** Use descriptive sheet names that immediately communicate each sheet's purpose.

---

## General Lab Workflow

This lab involves creating multiple related spreadsheets within one workbook:

1. **Student Grading System** – Build formulas that convert percentage grades to letters, calculate averages, and determine scholarship eligibility using nested IF functions and cross-sheet references
    
2. **Weather Forecast Analysis** – Research current weather data, apply conditional formatting to visualize temperature ranges, calculate averages, and create line charts to show temperature trends
    
3. **Vehicle Loan Calculator** – Use the PMT function to calculate payments, then apply Goal Seek to determine the loan term needed to achieve a target monthly payment
    
4. **Rent Increase Calculator** – Use absolute references to apply a consistent percentage increase across multiple properties
    

Throughout the lab, you'll practice renaming sheets, merging cells for formatting, creating formulas with multiple functions, and presenting data visually.

---

## Key Skills Developed

**Logical Decision-Making:** Using IF functions to automate decisions based on criteria eliminates manual categorization and reduces errors.

**Financial Modeling:** The PMT function and Goal Seek tool provide practical skills for real-world financial planning and "what-if" analysis.

**Data Visualization:** Charts and conditional formatting transform numbers into insights, making data accessible and actionable.

**Formula Design:** Combining functions, using absolute and relative references, and creating cross-sheet formulas builds sophisticated calculation systems.

**Professional Presentation:** Organized worksheets with clear formatting, merged titles, and visual elements create polished, professional deliverables.

---

## Formulas Used

### IF Function (Basic)

```
=IF(condition, value_if_true, value_if_false)
```

### IF Function (Nested for Multiple Conditions)

```
=IF(condition1, result1, IF(condition2, result2, IF(condition3, result3, default_result)))
```

### Average Function

```
=AVERAGE(range)
```

Example: `=AVERAGE(B2:B11)` calculates the mean of values in cells B2 through B11

### PMT Function

```
=PMT(rate, nper, pv, [fv], [type])
```

Where:

- **rate** = interest rate per period
- **nper** = total number of payment periods
- **pv** = present value (loan amount)
- **fv** = future value (optional, usually 0 for loans)
- **type** = when payments are due (optional, 0 = end of period)

### Cross-Sheet Reference

```
=SheetName!CellAddress
```

Example: `=Legend!A1` pulls the value from cell A1 on the Legend sheet

### Absolute Reference

```
=$A$1
```

The dollar signs lock the reference when copying formulas

### Percentage Calculation with Absolute Reference

```
=value * $reference
```

Example: `=B2 * $B$10` multiplies B2 by the locked cell B10 (which contains 4%)

To calculate a value increased by a percentage:

```
=value * (1 + $rate)
```

Example: `=B2 * (1 + $B$10)` increases B2 by the rate in B10

---

#excel #business-applications #spreadsheets #if-function #financial-functions #data-visualization #conditional-formatting #formulas #goal-seek #data-analysis