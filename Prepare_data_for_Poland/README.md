# Running ImperialCollegeLondon\/covid19model for Poland

Topic of this task is to run the `covid19model/base.r` script, which features data for European 14 countries.

## Data preparation

### File data/COVID-19-up-to-date.rds

This file contains basic data about daily cases, deaths and information about country. To feed program with data for
Poland we need to add rows in `data/COVID-19-up-to-date.csv` that fits format:

```text
dateRep,day,month,year,cases,deaths,countriesAndTerritories,geoId,countryterritoryCode,popData2018,continentExp
24/04/2020,24,04,2020,381,40,Poland,PL,PLN,37829969,Europe
```

Then we need to convert file to _*.rds_ format using function in R:

```R
csv_to_rds <- function(){
  readedCSV <- read.csv('data/COVID-19-up-to-date.csv')
  colnames(readedCSV)[colnames(readedCSV) == "countriesAndTerritories"] <- "Countries.and.territories"
  colnames(readedCSV)[colnames(readedCSV) == "dateRep"] <- "DateRep"
  colnames(readedCSV)[colnames(readedCSV) == "cases"] <- "Cases"
  colnames(readedCSV)[colnames(readedCSV) == "deaths"] <- "Deaths"
  saveRDS(readedCSV, 'data/C OVID-19-up-to-date.rds')
  return(0)
}
```

### File data/interventions.csv

This file contains data about non-pharmaceutical interventions in countries. For best results for `base.r` script
it's necessary to insert data about these interventions:

- Schools + Universities
- Public events
- Lockdown
- Social distancing encouraged
- Self-isolating if ill

Data should fit format:
```text
Country,Type,Event,Date effective,Link,,
Poland,Schools + Universities,Nationwide school closures,12.03.2020,https://pl.wikipedia.org/wiki/Pandemia_COVID-19_w_Polsce,,
```

### File data/popt_ifr.csv

File contains data about country, population and IFR. Data specified in format:

```text
"number","country","popt","ifr"
"15","Poland",37829969,0.010289760240957
```

### File data/regions.csv

This file contains list of regions.
```text
Regions
Denmark
Italy
...
Poland
```

## Results

Data prepared like this enables program to model Covid-19 for Poland. Probably some modifications in code are
necessary, because error occurs during `make-tablr.r` script runtime.

Script was run in `DEBUG` mode, that features 40 iterations. Quality of received data is not so good. Authors of
script recommend standard mode (1000 iterations) or `FULL` mode (1800 iterations). It would be done when script will
be fully adapted for the polish data.