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


## Author
Sabryna Rodrigues
