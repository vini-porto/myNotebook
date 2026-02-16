# Main Concepts

## The IF Function

The [[IF function]] is a **logical function** that makes decisions based on conditions. It evaluates whether something is true or false, then returns different values accordingly.

**Key principle:** You can **nest** IF functions inside each other to handle multiple conditions. This creates a decision tree where each condition is checked in sequence.

## Cross-Sheet References

[[Cross-sheet references]] allow one worksheet to pull data from another worksheet within the same workbook. Instead of duplicating information, you create links between sheets.

**Why it matters:** This keeps your workbook organized and maintains a single source of truth. If you update data in one location, all references automatically update. It's essential for creating organized, professional spreadsheets.

> [!NOTE] Syntax concept
> To reference another sheet, you use the format: `SheetName!CellAddress`

## The AVERAGE Function

**What it is:** The [[AVERAGE function]] is a [[statistical function]] that calculates the arithmetic mean of a set of numbers. It adds all values and divides by the count.

> [!NOTE] Important Note
> The AVERAGE function automatically ignores text and empty cells, counting only numeric values.

## The PMT Function

The [[PMT function]] is a **financial function** that calculates periodic payment amounts for loans or investments. It considers the principal amount, interest rate, and number of payment periods.

**Why it matters:** This is essential for financial planning. Whether you're buying a car, calculating mortgage payments, or planning business financing, the PMT function shows exactly how much you'll pay each period.

**How it's used in this lab:** Calculating monthly car payments based on:

- Loan amount (purchase price)
- Interest rate (annual percentage rate)
- Term length (number of months)

## Goal Seek Tool

[[Goal Seek]] is an **optimization tool** that works backward. You specify a desired result, and Excel automatically adjusts an input value to achieve that result.

**The process:**

1. Set up your formula with the desired outcome cell
2. Tell Goal Seek what value you want that cell to show
3. Specify which input cell should be changed
4. Let Excel calculate the required input value

## Conditional Formatting

**What it is:** [[Conditional formatting]] automatically applies visual formatting (colors, fonts, borders) to cells based on their values. The formatting changes dynamically as data changes.

**Common uses:**

- Highlighting values above or below thresholds
- Color scales showing high to low values
- Data bars providing visual magnitude comparison
- Icon sets (arrows, traffic lights) indicating performance

![[Lab 3 – Introduction to Excel#Absolute references (e.g., `$A$1`)]]

## Sorting Data

**What it is:** [[Sorting]] rearranges rows of data based on values in one or more columns. You can sort alphabetically, numerically, by date, or by custom orders.

# Formulas Used

## IF Function (Basic)

```
=IF(condition, value_if_true, value_if_false)
```

## IF Function (Nested for Multiple Conditions)

```
=IF(condition1, result1, IF(condition2, result2, IF(condition3, result3, default_result)))
```

## Average Function

```
=AVERAGE(range)
```

Example: `=AVERAGE(B2:B11)` calculates the mean of values in cells B2 through B11

## PMT Function

```
=PMT(rate, nper, pv, [fv], [type])
```

Where:

- **rate** = interest rate per period
- **nper** = total number of payment periods
- **pv** = present value (loan amount)
- **fv** = future value (optional, usually 0 for loans)
- **type** = when payments are due (optional, 0 = end of period)

## Cross-Sheet Reference

```
=SheetName!CellAddress
```

Example: `=Legend!A1` pulls the value from cell A1 on the Legend sheet

## Absolute Reference

```
=$A$1
```

The dollar signs lock the reference when copying formulas

## Percentage Calculation with Absolute Reference

```
=value * $reference
```

Example: `=B2 * $B$10` multiplies B2 by the locked cell B10 (which contains 4%)

To calculate a value increased by a percentage:

```
=value * (1 + $rate)
```

Example: `=B2 * (1 + $B$10)` increases B2 by the rate in B10

# Tags

#excel #business-applications #spreadsheets #if-function #financial-functions #data-visualization #conditional-formatting #formulas #goal-seek #data-analysis