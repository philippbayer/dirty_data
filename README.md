# Dirty data

A small table of example data I use to teach data cleaning in R. Australian dinosaurs!

Some problems:
- the xlsx file has groups in colored cells, which the csv lost
- the T column will get converted into TRUE by read_csv, read.csv, not by readxl::read_xlsx()
- the measurements end in m and t so R will recognise these columns as character, not numeric
- there are spaces in the column names which might make things more complicated
- -9 is used for NA
- one of the publication years is negative

Example code to clean up the csv:
```
library(tidyverse)
df <-read_csv('./Dinosaurs.csv', col_types = cols(
    Genus = col_character(),
    Length = col_character(),
    Weight = col_character(),
    `Best base` = col_character(),
    Citation_year = col_character()), 
    na = c('NA', '-9')
)

clean_df <- df %>% 
    mutate(Length = str_remove(Length, 'm')) %>% 
    mutate(Length = as.numeric(Length)) %>% 
    mutate(Weight = str_remove(Weight, 't')) %>% 
    mutate(Weight = as.numeric(Weight)) %>% 
    separate(col = Citation_year, sep='_', into=c('Author', 'Year')) %>% 
    mutate(Year = as.numeric(Year)) %>% 
    mutate(Year = abs(Year))

# now code like the following is possible
clean_df %>% ggplot(aes(x = Year, y = Length)) + geom_point()
```
