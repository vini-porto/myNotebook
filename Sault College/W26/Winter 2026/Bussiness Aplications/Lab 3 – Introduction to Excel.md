# Overview

This lab introduces [[Microsoft Excel]], a powerful [[spreadsheet software]] used for organizing, analyzing, and visualizing data.

## Key Concepts

## Spreadsheet Structure

A [[spreadsheet]] is organized into a grid of **cells**, each identified by a unique address combining a **column letter** and a **row number** (e.g., A1, B5, C12).

**Important terminology:**

- **Cell**: The basic unit where data is entered (intersection of a row and column)
- **Cell Reference**: The address of a cell (e.g., `A1`, `D5`)
- **Range**: A group of cells (e.g., `A1:A10` means cells A1 through A10)
- **Active Cell**: The currently selected cell, highlighted with a border

## Data Types in Excel

Excel recognizes different types of data and treats them accordingly:

- **Text**: Labels, names, descriptions (left-aligned by default)
- **Numbers**: Values that can be used in calculations (right-aligned by default)
- **Dates**: Special format for calendar dates
- **Formulas**: Expressions that perform calculations

## Formulas and Functions

[[Formulas]] are the heart of Excel's computational power. They allow you to perform calculations automatically and update results when data changes.

**Key principles:**

- All formulas begin with an **equals sign** (`=`)
- Formulas can reference other cells by their address
- When source data changes, formula results update automatically
- Formulas can use [[cell references]] instead of hard-coded numbers (making them flexible and reusable)

## Built-in Functions

Excel provides hundreds of pre-built [[functions]] for common calculations. Functions take inputs (called **arguments**) and return results.

**Common functions introduced:**

- **`SUM()`**: Adds a range of numbers
    
    - Example: `=SUM(A1:A10)` adds all values from A1 to A10
- **`AVERAGE()`**: Calculates the [[arithmetic mean]] of a range
    
    - Example: `=AVERAGE(B1:B5)` finds the average of five values
- **`MAX()`**: Returns the largest value in a range
    
- **`MIN()`**: Returns the smallest value in a range
    

> [!NOTE] Why functions matter:
> Instead of writing `=A1+A2+A3+A4+A5`, you can write `=SUM(A1:A5)`

## Relative vs. Absolute Cell References

Understanding [[cell references]] is crucial when copying formulas to multiple cells.

### Relative references (e.g., `A1`):

- Adjust automatically when copied to other cells
- Example: If `=A1*2` in cell B1 is copied to B2, it becomes `=A2*2`

### Absolute references (e.g., `$A$1`):

- Stay fixed when copied
- Use the **dollar sign** (`$`) to lock the row, column, or both
- Example: `=$A$1*2` will always reference cell A1, no matter where it's copied

### Mixed references (e.g., `$A1` or `A$1`):

- Lock only the column or only the row

---

**When to use each:**

- Use **relative** when you want the reference to change (e.g., applying the same calculation to each row)
- Use **absolute** when you need to reference a constant value (e.g., a tax rate or conversion factor stored in one cell)

# Formatting and Presentation

Proper [[spreadsheet formatting]] makes data easier to read and understand.

**Key formatting techniques:**

- **Number formatting**: Display numbers as currency, percentages, decimals, etc.
- **Cell alignment**: Center, left-align, or right-align text
- **Borders and shading**: Visually separate sections
- **Column width/row height**: Ensure all data is visible
- **Font styles**: Emphasize headers and important information

# Formulas Used

## Basic Arithmetic Operations

- Addition: `=A1+B1`
- Subtraction: `=A1-B1`
- Multiplication: `=A1*B1`
- Division: `=A1/B1`

## Statistical Functions

- Sum: `=SUM(range)`
    - Example: `=SUM(A1:A10)`
- Average: `=AVERAGE(range)`
    - Example: `=AVERAGE(B1:B20)`
- Maximum: `=MAX(range)`
- Minimum: `=MIN(range)`

## Cell Reference Types

- Relative: `A1` (adjusts when copied)
- Absolute: `$A$1` (stays fixed when copied)
- Mixed: `$A1` (locks column) or `A$1` (locks row)

# Tags

#computer-science #spreadsheets #data-analysis #excel #information-technology