# VLOOKUP Function

### What It Is

[[VLOOKUP]] (Vertical Lookup) is a function that searches for a value in the leftmost column of a table and returns a value from a specified column in the same row. 

Think of it as a phonebook lookup: you search for a name and retrieve the corresponding phone number.

## How It Works

The basic structure involves four components:

1. **Lookup Value**: The value you're searching for (what you know)
2. **Table Array**: The range where the data is stored
3. **Column Index**: Which column contains the information you want to retrieve
4. **Range Lookup**: Whether you want an exact match (FALSE) or approximate match (TRUE)

## Dan's VLOOKUP Example

The lab uses a practical scenario with **student grade data**:

|Student|Grade|
|---|---|
|Dan|85|
|Sarah|92|
|Mike|78|

**Scenario**: You have a list of students in one location and their grades in another table. Using VLOOKUP, you can automatically retrieve each student's grade by searching for their name.

# Data Visualization and Charting

![[Lab 5 – Data Research and Excel Charting#Column Charts (3D)]]

![[Lab 5 – Data Research and Excel Charting#Pie Charts]]

# Chart Components

Understanding the parts of a chart helps you create effective visualizations:

- **[[Chart Title]]**: Describes what the chart represents
- **[[Axis Labels]]**: Identify what each axis measures
- **[[Legend]]**: Explains what different colors or patterns represent
- **[[Data Labels]]**: Show exact values on chart elements
- **[[Gridlines]]**: Help viewers read values more accurately

# Choosing the Right Chart Type

Different data requires different visualization approaches:

- **Comparison** (comparing values between categories) → Column Charts or Bar Charts

- **Trend Analysis** (showing change over time) → Line Charts

- **Part-to-Whole** (showing proportions) → Pie Charts

- **Key Principle**: The chart type should make the data's story clearer, not more confusing.

# Formulas Used

### VLOOKUP Function

```
=VLOOKUP(lookup_value, table_array, col_index_num, [range_lookup])
```

**Parameters**:

- `lookup_value`: The value to search for
- `table_array`: The range containing the data (use absolute references: $A$1:$C$10)
- `col_index_num`: The column number in the table from which to retrieve the value
- `range_lookup`: FALSE for exact match, TRUE for approximate match

**Example**:

```
=VLOOKUP(A2, $D$2:$E$10, 2, FALSE)
```

This searches for the value in A2 within the range D2:E10 and returns the value from the 2nd column of that range.

# Tags

#excel #data-analysis #spreadsheets #vlookup #data-visualization #charting #computer-applications