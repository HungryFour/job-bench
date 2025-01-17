# join-order-benchmark

This repository is a fork of the [project](https://github.com/gregrahn/join-order-benchmark).
Here we unite queries and data in one place.
Main goal of this repository is simplifying of the deploy process.

Large tables divided into chunks each less than 100 MB.

Repository contains some scripts for quick deploy & run of the benchmark:
* *schema.sql* - creates the data schema.
* *copy.sql* - copies data from csv files into the tables. Uses `datadir` variable to make absolute paths to csv files. Use `psql -v` to define it.
* *parts.sql* - script which splitted the tables. Just for future reusage.
* *job* - a template script for quick launch of the benchmark.

Example below shows export procedure of all tables:

```
psql -f ~/jo-bench/schema.sql
psql -vdatadir="'/home/user/jo-bench'" -f ~/jo-bench/copy.sql
```

如果遇到这个报错，需要将copy.sql中的代码WIN1251更换为UTF8
```
psql:copy.sql:37: ERROR:  character with byte sequence 0x98 in encoding "WIN1251" has no equivalent in encoding "UTF8"
CONTEXT:  COPY aka_title, line 1275
SQL statement "COPY aka_title FROM '/job/csv/aka_title.csv' WITH (FORMAT csv, NULL '', DELIMITER ',', QUOTE '"', ESCAPE '\', ENCODING 'WIN1251');"
```


NB! Deploying tested on database with C-locale.
