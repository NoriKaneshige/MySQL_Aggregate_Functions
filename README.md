# MySQL_Aggregate_Functions

## COUNT
```
mysql> SELECT author_fname FROM books;
+--------------+
| author_fname |
+--------------+
| Jhumpa       |
| Neil         |
| Neil         |
| Jhumpa       |
| Dave         |
| Dave         |
| Michael      |
| Patti        |
| Dave         |
| Neil         |
| Raymond      |
| Raymond      |
| Don          |
| John         |
| David        |
| David        |
| Dan          |
| Freida       |
| George       |
+--------------+
19 rows in set (0.00 sec)

mysql> SELECT COUNT(*) FROM books;
+----------+
| COUNT(*) |
+----------+
|       19 |
+----------+
1 row in set (0.03 sec)

mysql> SELECT COUNT(author_fname) FROM books;
+---------------------+
| COUNT(author_fname) |
+---------------------+
|                  19 |
+---------------------+
1 row in set (0.00 sec)

mysql> SELECT COUNT(DISTINCT author_fname) FROM books;
+------------------------------+
| COUNT(DISTINCT author_fname) |
+------------------------------+
|                           12 |
+------------------------------+
1 row in set (0.01 sec)

mysql> SELECT COUNT(DISTINCT author_lname) FROM books;
+------------------------------+
| COUNT(DISTINCT author_lname) |
+------------------------------+
|                           11 |
+------------------------------+
1 row in set (0.00 sec)

mysql> SELECT COUNT(DISTINCT author_lname, author_fname) FROM books;
+--------------------------------------------+
| COUNT(DISTINCT author_lname, author_fname) |
+--------------------------------------------+
|                                         12 |
+--------------------------------------------+
1 row in set (0.00 sec)

mysql> SELECT title FROM books WHERE title LIKE '%the%';
+-------------------------------------------+
| title                                     |
+-------------------------------------------+
| The Namesake                              |
| A Hologram for the King: A Novel          |
| The Circle                                |
| The Amazing Adventures of Kavalier & Clay |
| Consider the Lobster                      |
| Lincoln In The Bardo                      |
+-------------------------------------------+
6 rows in set (0.01 sec)

mysql> SELECT COUNT(*) FROM books WHERE title LIKE '%the%';
+----------+
| COUNT(*) |
+----------+
|        6 |
+----------+
1 row in set (0.00 sec)
```

## GROUP BY
![group_by_1](https://github.com/NoriKaneshige/MySQL_Aggregate_Functions/blob/master/group_by_1.png)
![group_by_2](https://github.com/NoriKaneshige/MySQL_Aggregate_Functions/blob/master/group_by_2.png)
```

```

