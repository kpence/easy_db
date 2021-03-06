NOTE:

This is a fork from the original repo in order for me to add changes and make pull requests.
If you want to use easy_db, go [here](https://github.com/zachbateman/easy_db)

# easy_db

easy_db is a tool designed to quickly allow Python database interaction capabilities from a consolidated, intuitive user interface provided by the "DataBase" class.

# Goals

 - Make common database tasks very easy
 - Intelligently handle different database types
 - Provide intuitive, consistent, Pythonic methods for accessing data
 - Provide good performance without requiring polished query code
 - Expose database connection and cursor to users wanting fine-grained control
 - Just get the data into Python so we can use it!

# Quick Start

Let's first connect to a SQLite database.
```sh
import easy_db
db = easy_db.DataBase('test_sqlite3_db.db')
```

Now let's see what tables are available in this database.
```sh
tables = db.pull_all_table_names()
```

Table columns and types are simple to investigate.
```sh
print(db.table_columns_and_types('example_table'))
```

Let's pull all of the data from a table.  We could start with something like "SELECT * ..." but this is way more fun:
```sh
data = db.pull_table('example_table')
```

Note that the table/query data is returned as a list of dictionaries with column names as dictionary keys.

 - Pro Tip:  If desired, a Pandas dataframe of the same form as the database table can be easily created from this data structure using:
```sh
import pandas
df = pandas.DataFrame(data)
```


Now perhaps we have an Access database and would like to pull in a table from our SQLite database.  easy_db makes this quick and easy and gracefully handles the nuances of dealing with the different databases.
```sh
import easy_db

db = easy_db.DataBase('test_sqlite3_db.db')
db_2 = easy_db.DataBase('test_access_db.accdb')

db_2.copy_table(db, 'example_table')
```

Thanks for checking out easy_db, and please take a look at the methods of the DataBase class if you'd like to see what other capabilities are currently available!


License
----
MIT
