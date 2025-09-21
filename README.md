# Weather Data Cleaning with R

## Project Overview
This project demonstrates a complete data cleaning and preparation workflow for a weather dataset (`tempo.csv`) using base R functions.  
The cleaned data is prepared for exploratory data analysis or predictive modeling.

---

## Dataset Description
The dataset contains weather observations with the following variables:

- **Aparencia**: Weather conditions (Categorical)  
- **Temperatura**: Temperature readings (Numerical)  
- **Umidade**: Humidity percentage (Numerical)  
- **Vento**: Wind presence (TRUE/FALSE) (Categorical)  
- **Jogar**: Decision to play outdoors - Target variable (Categorical)

---

## Code Explanation

### 1. Data Loading
```r
data = read.csv("tempo.csv", sep=";", na.strings="", stringsAsFactors=T)
```
- **`read.csv()`**: Loads the dataset from a CSV file  
- **`sep=";"`**: Specifies semicolon as the field separator  
- **`na.strings=""`**: Treats empty strings as missing values (`NA`)  
- **`stringsAsFactors=T`**: Converts character strings to categorical factors  

---

### 2. Initial Data Inspection
```r
head(data)
summary(data)
```
- **`head()`**: Displays the first 6 rows of the dataset  
- **`summary()`**: Provides descriptive statistics for each column  

---

### 3. Cleaning `Aparencia` (Weather Appearance)
```r
unique(data$Aparencia)
summary(data$Aparencia)
table = table(data$Aparencia)
barplot(table, main="Aparência", xlab="Aparência")

data[data$Aparencia == "menos",]$Aparencia = "sol"
data$Aparencia = factor(data$Aparencia)
```
- **`unique()`**: Identifies distinct values in a column  
- **`table()`**: Creates frequency counts of categorical data  
- **`barplot()`**: Visualizes frequency distributions  
- **Subsetting `[ ]`**: Filters and replaces specific values  
- **`factor()`**: Ensures proper categorical variable handling  

---

### 4. Cleaning `Temperatura` (Temperature)
```r
boxplot(data$Temperatura)
data[data$Temperatura > 130,]$Temperatura = median(data$Temperatura)
data[data$Temperatura < -130,]$Temperatura = median(data$Temperatura)

table2 = table(data$Temperatura)
barplot(table2, main="Temperatura", xlab="Temperatura")
```
- **`boxplot()`**: Identifies outliers in numerical data  
- **`median()`**: Calculates the median value for imputation  

---

### 5. Cleaning `Umidade` (Humidity)
```r
table3 = table(data$Umidade)
boxplot(data$Umidade)
barplot(table3, main="Umidade", xlab="Umidade")

data[is.na(data$Umidade),]$Umidade = median(data$Umidade, na.rm=T)
data[data$Umidade > 100,]$Umidade = median(data$Umidade)
```
- **`is.na()`**: Identifies missing values in the dataset  
- **`na.rm=T`**: Removes NA values from statistical calculations  

---

### 6. Exploring `Jogar` (Target Variable)
```r
unique(data$Jogar)
summary(data$Jogar)
```

---

### 7. Cleaning `Vento` (Wind)
```r
table4 = table(data$Vento)
barplot(table4, main="Vento", xlab="Vento")

data[is.na(data$Vento),]$Vento = "FALSO"
```

---

## Data Cleaning Summary
| Variable    | Issue Handled                  | Action Taken              | R Functions Used                         |
|-------------|--------------------------------|---------------------------|------------------------------------------|
| Aparencia   | Invalid value `"menos"`        | Replaced with `"sol"`     | `unique()`, `table()`, `[ ]`, `factor()` |
| Temperatura | Extreme outliers (>130 & <−130)| Replaced with median      | `boxplot()`, `median()`, `[ ]`           |
| Umidade     | Missing values (NA)            | Imputed with median       | `is.na()`, `median()`, `na.rm`           |
| Umidade     | Invalid values (>100)          | Replaced with median      | `[ ]`, `median()`                        |
| Vento       | Missing values (NA)            | Replaced with `"FALSO"`   | `is.na()`, `[ ]`                         |

---

## Key R Functions Overview
- **`read.csv()`**: Load data from CSV files  
- **`head()` / `summary()`**: Initial data exploration  
- **`unique()` / `table()`**: Analyze categorical variables  
- **`boxplot()`**: Identify outliers in numerical data  
- **`median()`**: Calculate central tendency for imputation  
- **`is.na()`**: Detect missing values  
- **`factor()`**: Manage categorical variables  
- **`barplot()`**: Visualize distributions  
- **Subsetting `[ ]`**: Filter and transform data
