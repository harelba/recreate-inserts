# Purpose 

This utility gets the output of a Mysql SELECT query and generates a set of matching INSERT commands.

# Usage
		Usage: 
			recreate-inserts [options] <output_table_name>

		Options:
		  -h, --help            show this help message and exit
		  -b BATCH, --batch=BATCH
					Batch size - how many rows to put in each insert.
		  -d DELIMITER, --delimiter=DELIMITER
					Delimiter
		  -c COLUMN_LIST, --column-list=COLUMN_LIST
					User-set column list (instead of reading the list from
					the first row)
		  -r, --relaxed         Fill with nulls missing fields or trim extra fields

## Usage Details

The first row of input is expected to have the table's column names (as in mysql's output). The user can provide his own set of column names using the -c option.

Example:
  echo "select * from mydb.my_table limit 100" | ./recreate-inserts -b 20 mydb.my_other_table

  This example will take a maximum of 100 rows from mydb.mytable and generate INSERT commands for table my_other_table. Each insert command will contain a maximum of 20 rows.

The utility uses the default \t delimiter of mysql. If you use other delimiters, use the -d option.

If needed, turn on relaxed mode by using -r. It will cause missing fields to be filled with nulls and extra fields to be ignored.

NOTE: Please note that there is no way to determine the table name from the output, so it must be provided as an argument
     to the script. Look at it as a feature that allows a simple way to copy rows between tables with identical structure.

