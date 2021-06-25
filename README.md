# Dirty data

A small table of example data I use to teach data cleaning in R. Australian dinosaurs!

Some problems:
- the xlsx file has groups in colored cells, which the csv lost
- the T column will get converted into TRUE by read_csv, read.csv, not by readxl::read_xlsx()
- the measurements end in m and t so R will recognise these columns as character, not numeric
- there are spaces in the column names which might make things more complicated
- -9 is used for NA
- one of the publication years is negative
