# YetAnotherSimpleSystem
## Author: Michael Simpson

## 1) Importer & Database
Usage: `$ ./ingest [source file]`

The database will appear in the current working directory as `./data/`. Within
the top level directory the files are partitioned into directories by date.
Within the date directories, the rows are further partitioned into files by
their 'STB' value. This structure could be tuned for optimization of access
patterns, but for now serves as a general organization scheme.

Example:
```
  data/
  |
  |-- 2014-04-02/
  |   |
  |   |-- stb1
  |   |-- stb2
  |-- 2014-05-02/
  .   |
  .   |-- stb1
  .   .
      .
      .
```

## 2.1) Select, Filter, and Order Query Functionality

Usage: `$ ./query [-s [ARGS] |  -o [ARGS] | -f [ARGS]]`

The query tool can be run with any order and combination of flags enabled.
Query results are stored in `./results/` and are named using Unix timestamps.
Running the query tool with no arguments will retrieve all records
currently in the database.

### OPTIONS
  -f, --filter
      The filter flag will accept string matching arguments of the form
      `COLUMN_NAME=STRING` It will return rows that contain a match to 
      the string argument in the provided column. Any matching string containing
      whitespace must be surrounded with single quotes. Ex:
      
      -f DATE=2014-02-04

      -f TITLE='the matrix'
      
  -o, --order
      The order flag will accept a comma seperated sequence of column names.
      Query results will be sorted column wise by each column in the argument
      sequence with precedence decreasing from left to right. Ex:
      
      -o REV,TITLE,DATE
      
  -s, --select
      The selection flag accepts a comma seperated sequence of column names.
      Query results will contain only the columns given in the argument
      sequence. Ex:
      
      -s STB,PROVIDER
      
### Recognized Column Names
  [STB|TITLE|PROVIDER|DATE|REV|VIEW_TIME]
      
