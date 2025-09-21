# Weather Data Cleaning Project

## Overview
This project involves cleaning and preparing a weather dataset (`tempo.csv`) for analysis. The dataset contains weather attributes that likely serve as features for predicting whether to play a game (the `Jogar` variable).

## Dataset Description
The dataset contains the following variables:
- `Aparencia`: Weather appearance (categorical)
- `Temperatura`: Temperature (numerical)
- `Umidade`: Humidity percentage (numerical)
- `Vento`: Wind presence (TRUE/FALSE) (categorical)
- `Jogar`: Target variable - decision to play (categorical)

## Cleaning Operations Performed

| Variable | Issue Handled | Action Taken |
|----------|---------------|--------------|
| Aparencia | Invalid value ("menos") | Replaced with "sol" |
| Temperatura | Extreme outliers (>130 & <-130) | Replaced with median |
| Umidade | Missing values (NA) | Imputed with median |
| Umidade | Invalid values (>100) | Replaced with median |
| Vento | Missing values (NA) | Replaced with "FALSO" |

R Functions Reference Guide
1. Reading Data (read.csv())
Purpose: Loads a dataset from a CSV file into R as a data frame.

Syntax:

r
data <- read.csv(file, sep = ",", na.strings = "NA", stringsAsFactors = FALSE)
Parameters used:

file: The path to the CSV file ("tempo.csv")

sep: The field separator character (";" for semicolon-delimited files)

na.strings: Character vector of strings to be treated as NA ("" treats empty cells as missing)

stringsAsFactors: Logical indicating whether to convert character vectors to factors (TRUE in your code)

Example:

r
# Read a standard comma-separated file
data <- read.csv("data.csv")

# Read a semicolon-separated file with custom NA values
data <- read.csv("data.csv", sep = ";", na.strings = c("", "NA", "unknown"))
2. Data Inspection Functions
head()
Purpose: Displays the first 6 rows of a data frame.

r
head(data)  # Show first 6 rows
head(data, 10)  # Show first 10 rows
summary()
Purpose: Provides summary statistics for each column in a data frame.

Numeric columns: Min, 1st Quartile, Median, Mean, 3rd Quartile, Max

Factor columns: Frequency count for each category

Logical columns: Count of TRUE/FALSE values

Missing values: Count of NAs

r
summary(data)  # Summary for entire dataframe
summary(data$Temperatura)  # Summary for specific column
unique()
Purpose: Returns distinct values from a vector or column.

r
unique(data$Aparencia)  # List all unique weather appearances
3. Data Manipulation Functions
Subsetting with [ ]
Purpose: Selects or filters specific rows and columns.

Syntax: dataframe[rows, columns]

Examples:

r
# Filter rows where Aparencia equals "menos"
data[data$Aparencia == "menos", ]

# Select specific column for filtered rows
data[data$Aparencia == "menos", "Aparencia"]

# Replace values in filtered subset
data[data$Aparencia == "menos", "Aparencia"] <- "sol"
factor()
Purpose: Converts a vector to a categorical variable (factor).

r
# Convert character vector to factor
data$Aparencia <- factor(data$Aparencia)

# Check factor levels
levels(data$Aparencia)
4. Statistical Functions
median()
Purpose: Calculates the median value of a numeric vector.

r
median(data$Temperatura)  # Overall median
median(data$Temperatura, na.rm = TRUE)  # Median excluding NA values
table()
Purpose: Creates frequency tables of categorical variables.

r
# Frequency table for a single variable
table(data$Aparencia)

# Cross-tabulation of two variables
table(data$Aparencia, data$Jogar)
5. Handling Missing Values
is.na()
Purpose: Identifies missing values (NA) in a vector.

r
# Find missing values in Umidade column
is.na(data$Umidade)

# Count missing values
sum(is.na(data$Umidade))

# Replace missing values with median
data[is.na(data$Umidade), "Umidade"] <- median(data$Umidade, na.rm = TRUE)
6. Visualization Functions
barplot()
Purpose: Creates bar plots from frequency data.

r
# Basic bar plot from table
freq_table <- table(data$Aparencia)
barplot(freq_table)

# Customized bar plot
barplot(freq_table, 
        main = "Weather Appearance Distribution",
        xlab = "Appearance Type",
        ylab = "Frequency",
        col = "steelblue")
boxplot()
Purpose: Creates box plots to visualize distribution and identify outliers.

r
# Basic box plot
boxplot(data$Temperatura)

# Customized box plot
boxplot(data$Temperatura,
        main = "Temperature Distribution",
        ylab = "Temperature (°C)",
        col = "lightyellow")

## Author
Sabryna Rodrigues
