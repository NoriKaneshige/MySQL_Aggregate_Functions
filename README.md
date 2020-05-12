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
mysql> SELECT title, author_lname FROM books;
+-----------------------------------------------------+----------------+
| title                                               | author_lname   |
+-----------------------------------------------------+----------------+
| The Namesake                                        | Lahiri         |
| Norse Mythology                                     | Gaiman         |
| American Gods                                       | Gaiman         |
| Interpreter of Maladies                             | Lahiri         |
| A Hologram for the King: A Novel                    | Eggers         |
| The Circle                                          | Eggers         |
| The Amazing Adventures of Kavalier & Clay           | Chabon         |
| Just Kids                                           | Smith          |
| A Heartbreaking Work of Staggering Genius           | Eggers         |
| Coraline                                            | Gaiman         |
| What We Talk About When We Talk About Love: Stories | Carver         |
| Where I'm Calling From: Selected Stories            | Carver         |
| White Noise                                         | DeLillo        |
| Cannery Row                                         | Steinbeck      |
| Oblivion: Stories                                   | Foster Wallace |
| Consider the Lobster                                | Foster Wallace |
| 10% Happier                                         | Harris         |
| fake_book                                           | Harris         |
| Lincoln In The Bardo                                | Saunders       |
+-----------------------------------------------------+----------------+
19 rows in set (0.24 sec)

mysql> SELECT title, author_lname FROM books
    -> GROUP BY author_lname;
+-----------------------------------------------------+----------------+
| title                                               | author_lname   |
+-----------------------------------------------------+----------------+
| What We Talk About When We Talk About Love: Stories | Carver         |
| The Amazing Adventures of Kavalier & Clay           | Chabon         |
| White Noise                                         | DeLillo        |
| A Hologram for the King: A Novel                    | Eggers         |
| Oblivion: Stories                                   | Foster Wallace |
| Norse Mythology                                     | Gaiman         |
| 10% Happier                                         | Harris         |
| The Namesake                                        | Lahiri         |
| Lincoln In The Bardo                                | Saunders       |
| Just Kids                                           | Smith          |
| Cannery Row                                         | Steinbeck      |
+-----------------------------------------------------+----------------+
11 rows in set (0.00 sec)

mysql> SELECT author_lname, COUNT(*)
    -> FROM books GROUP BY author_lname;
+----------------+----------+
| author_lname   | COUNT(*) |
+----------------+----------+
| Carver         |        2 |
| Chabon         |        1 |
| DeLillo        |        1 |
| Eggers         |        3 |
| Foster Wallace |        2 |
| Gaiman         |        3 |
| Harris         |        2 |
| Lahiri         |        2 |
| Saunders       |        1 |
| Smith          |        1 |
| Steinbeck      |        1 |
+----------------+----------+
11 rows in set (0.00 sec)

mysql> SELECT title, author_fname, author_lname FROM books;
+-----------------------------------------------------+--------------+----------------+
| title                                               | author_fname | author_lname   |
+-----------------------------------------------------+--------------+----------------+
| The Namesake                                        | Jhumpa       | Lahiri         |
| Norse Mythology                                     | Neil         | Gaiman         |
| American Gods                                       | Neil         | Gaiman         |
| Interpreter of Maladies                             | Jhumpa       | Lahiri         |
| A Hologram for the King: A Novel                    | Dave         | Eggers         |
| The Circle                                          | Dave         | Eggers         |
| The Amazing Adventures of Kavalier & Clay           | Michael      | Chabon         |
| Just Kids                                           | Patti        | Smith          |
| A Heartbreaking Work of Staggering Genius           | Dave         | Eggers         |
| Coraline                                            | Neil         | Gaiman         |
| What We Talk About When We Talk About Love: Stories | Raymond      | Carver         |
| Where I'm Calling From: Selected Stories            | Raymond      | Carver         |
| White Noise                                         | Don          | DeLillo        |
| Cannery Row                                         | John         | Steinbeck      |
| Oblivion: Stories                                   | David        | Foster Wallace |
| Consider the Lobster                                | David        | Foster Wallace |
| 10% Happier                                         | Dan          | Harris         |
| fake_book                                           | Freida       | Harris         |
| Lincoln In The Bardo                                | George       | Saunders       |
+-----------------------------------------------------+--------------+----------------+
19 rows in set (0.00 sec)

mysql> SELECT title, author_fname, author_lname FROM books GROUP BY author_lname;
+-----------------------------------------------------+--------------+----------------+
| title                                               | author_fname | author_lname   |
+-----------------------------------------------------+--------------+----------------+
| What We Talk About When We Talk About Love: Stories | Raymond      | Carver         |
| The Amazing Adventures of Kavalier & Clay           | Michael      | Chabon         |
| White Noise                                         | Don          | DeLillo        |
| A Hologram for the King: A Novel                    | Dave         | Eggers         |
| Oblivion: Stories                                   | David        | Foster Wallace |
| Norse Mythology                                     | Neil         | Gaiman         |
| 10% Happier                                         | Dan          | Harris         |
| The Namesake                                        | Jhumpa       | Lahiri         |
| Lincoln In The Bardo                                | George       | Saunders       |
| Just Kids                                           | Patti        | Smith          |
| Cannery Row                                         | John         | Steinbeck      |
+-----------------------------------------------------+--------------+----------------+
11 rows in set (0.00 sec)

mysql> SELECT author_fname, author_lname, COUNT(*) FROM books GROUP BY author_lname;
+--------------+----------------+----------+
| author_fname | author_lname   | COUNT(*) |
+--------------+----------------+----------+
| Raymond      | Carver         |        2 |
| Michael      | Chabon         |        1 |
| Don          | DeLillo        |        1 |
| Dave         | Eggers         |        3 |
| David        | Foster Wallace |        2 |
| Neil         | Gaiman         |        3 |
| Dan          | Harris         |        2 |
| Jhumpa       | Lahiri         |        2 |
| George       | Saunders       |        1 |
| Patti        | Smith          |        1 |
| John         | Steinbeck      |        1 |
+--------------+----------------+----------+
11 rows in set (0.00 sec)

mysql> SELECT author_fname, author_lname, COUNT(*) FROM books GROUP BY author_lname, author_fname;
+--------------+----------------+----------+
| author_fname | author_lname   | COUNT(*) |
+--------------+----------------+----------+
| Raymond      | Carver         |        2 |
| Michael      | Chabon         |        1 |
| Don          | DeLillo        |        1 |
| Dave         | Eggers         |        3 |
| David        | Foster Wallace |        2 |
| Neil         | Gaiman         |        3 |
| Dan          | Harris         |        1 |
| Freida       | Harris         |        1 |
| Jhumpa       | Lahiri         |        2 |
| George       | Saunders       |        1 |
| Patti        | Smith          |        1 |
| John         | Steinbeck      |        1 |
+--------------+----------------+----------+
12 rows in set (0.01 sec)

mysql> SELECT released_year FROM books;
+---------------+
| released_year |
+---------------+
|          2003 |
|          2016 |
|          2001 |
|          1996 |
|          2012 |
|          2013 |
|          2000 |
|          2010 |
|          2001 |
|          2003 |
|          1981 |
|          1989 |
|          1985 |
|          1945 |
|          2004 |
|          2005 |
|          2014 |
|          2001 |
|          2017 |
+---------------+
19 rows in set (0.00 sec)

mysql> SELECT released_year, COUNT(*) FROM books GROUP BY released_year;
+---------------+----------+
| released_year | COUNT(*) |
+---------------+----------+
|          1945 |        1 |
|          1981 |        1 |
|          1985 |        1 |
|          1989 |        1 |
|          1996 |        1 |
|          2000 |        1 |
|          2001 |        3 |
|          2003 |        2 |
|          2004 |        1 |
|          2005 |        1 |
|          2010 |        1 |
|          2012 |        1 |
|          2013 |        1 |
|          2014 |        1 |
|          2016 |        1 |
|          2017 |        1 |
+---------------+----------+
16 rows in set (0.00 sec)

mysql> SELECT CONCAT('In ', released_year, ' ', COUNT(*), ' book(s) released') AS year FROM books GROUP BY r
eleased_year;
+----------------------------+
| year                       |
+----------------------------+
| In 1945 1 book(s) released |
| In 1981 1 book(s) released |
| In 1985 1 book(s) released |
| In 1989 1 book(s) released |
| In 1996 1 book(s) released |
| In 2000 1 book(s) released |
| In 2001 3 book(s) released |
| In 2003 2 book(s) released |
| In 2004 1 book(s) released |
| In 2005 1 book(s) released |
| In 2010 1 book(s) released |
| In 2012 1 book(s) released |
| In 2013 1 book(s) released |
| In 2014 1 book(s) released |
| In 2016 1 book(s) released |
| In 2017 1 book(s) released |
+----------------------------+
16 rows in set (0.02 sec)

```

## MIN and MAX
```
mysql> SELECT MIN(released_year)
    -> FROM books;
+--------------------+
| MIN(released_year) |
+--------------------+
|               1945 |
+--------------------+
1 row in set (0.00 sec)

mysql> SELECT MIN(pages) FROM books;
+------------+
| MIN(pages) |
+------------+
|        176 |
+------------+
1 row in set (0.00 sec)

mysql> SELECT MAX(pages)
    -> FROM books;
+------------+
| MAX(pages) |
+------------+
|        634 |
+------------+
1 row in set (0.01 sec)

mysql> SELECT MAX(released_year)
    -> FROM books;
+--------------------+
| MAX(released_year) |
+--------------------+
|               2017 |
+--------------------+
1 row in set (0.00 sec)

mysql> SELECT MAX(pages), title
    -> FROM books;
+------------+--------------+
| MAX(pages) | title        |
+------------+--------------+
|        634 | The Namesake |
+------------+--------------+
1 row in set (0.00 sec)
// Doesn't work.

mysql> SELECT
    ->   title,
    ->   pages
    -> FROM books
    -> WHERE pages = (SELECT
    ->   MIN(pages)
    -> FROM books);
+-----------------------------------------------------+-------+
| title                                               | pages |
+-----------------------------------------------------+-------+
| What We Talk About When We Talk About Love: Stories |   176 |
+-----------------------------------------------------+-------+
1 row in set (0.00 sec)

mysql> SELECT
    ->   title,
    ->   pages
    -> FROM books
    -> WHERE pages = (SELECT
    ->   MAX(pages)
    -> FROM books);
+-------------------------------------------+-------+
| title                                     | pages |
+-------------------------------------------+-------+
| The Amazing Adventures of Kavalier & Clay |   634 |
+-------------------------------------------+-------+
1 row in set (0.00 sec)

mysql> SELECT title, pages FROM books
    -> ORDER BY pages ASC LIMIT 1;
+-----------------------------------------------------+-------+
| title                                               | pages |
+-----------------------------------------------------+-------+
| What We Talk About When We Talk About Love: Stories |   176 |
+-----------------------------------------------------+-------+
1 row in set (0.01 sec)

mysql> SELECT title, pages FROM books
    -> ORDER BY pages DESC LIMIT 1;
+-------------------------------------------+-------+
| title                                     | pages |
+-------------------------------------------+-------+
| The Amazing Adventures of Kavalier & Clay |   634 |
+-------------------------------------------+-------+
1 row in set (0.02 sec)

// Find the year each author published their first book
mysql> SELECT
    ->   author_fname,
    ->   author_lname,
    ->   MIN(released_year)
    -> FROM books
    -> GROUP BY author_lname,
    ->          author_fname;
+--------------+----------------+--------------------+
| author_fname | author_lname   | MIN(released_year) |
+--------------+----------------+--------------------+
| Raymond      | Carver         |               1981 |
| Michael      | Chabon         |               2000 |
| Don          | DeLillo        |               1985 |
| Dave         | Eggers         |               2001 |
| David        | Foster Wallace |               2004 |
| Neil         | Gaiman         |               2001 |
| Dan          | Harris         |               2014 |
| Freida       | Harris         |               2001 |
| Jhumpa       | Lahiri         |               1996 |
| George       | Saunders       |               2017 |
| Patti        | Smith          |               2010 |
| John         | Steinbeck      |               1945 |
+--------------+----------------+--------------------+
12 rows in set (0.01 sec)

// Find the longest page count for each author
mysql> SELECT
    ->   author_fname,
    ->   author_lname,
    ->   MAX(pages)
    -> FROM books
    -> GROUP BY author_lname,
    ->          author_fname;
+--------------+----------------+------------+
| author_fname | author_lname   | MAX(pages) |
+--------------+----------------+------------+
| Raymond      | Carver         |        526 |
| Michael      | Chabon         |        634 |
| Don          | DeLillo        |        320 |
| Dave         | Eggers         |        504 |
| David        | Foster Wallace |        343 |
| Neil         | Gaiman         |        465 |
| Dan          | Harris         |        256 |
| Freida       | Harris         |        428 |
| Jhumpa       | Lahiri         |        291 |
| George       | Saunders       |        367 |
| Patti        | Smith          |        304 |
| John         | Steinbeck      |        181 |
+--------------+----------------+------------+
12 rows in set (0.00 sec)

mysql> SELECT
    ->   CONCAT(author_fname, ' ', author_lname) AS author,
    ->   MAX(pages) AS 'longest book'
    -> FROM books
    -> GROUP BY author_lname,
    ->          author_fname;
+----------------------+--------------+
| author               | longest book |
+----------------------+--------------+
| Raymond Carver       |          526 |
| Michael Chabon       |          634 |
| Don DeLillo          |          320 |
| Dave Eggers          |          504 |
| David Foster Wallace |          343 |
| Neil Gaiman          |          465 |
| Dan Harris           |          256 |
| Freida Harris        |          428 |
| Jhumpa Lahiri        |          291 |
| George Saunders      |          367 |
| Patti Smith          |          304 |
| John Steinbeck       |          181 |
+----------------------+--------------+
12 rows in set (0.02 sec)
```
## SUM
```
mysql> SELECT SUM(pages)
    -> FROM books;
+------------+
| SUM(pages) |
+------------+
|       6623 |
+------------+
1 row in set (0.00 sec)

mysql> SELECT author_fname,
    ->        author_lname,
    ->        Sum(pages)
    -> FROM books
    -> GROUP BY
    ->     author_lname,
    ->     author_fname;
+--------------+----------------+------------+
| author_fname | author_lname   | Sum(pages) |
+--------------+----------------+------------+
| Raymond      | Carver         |        702 |
| Michael      | Chabon         |        634 |
| Don          | DeLillo        |        320 |
| Dave         | Eggers         |       1293 |
| David        | Foster Wallace |        672 |
| Neil         | Gaiman         |        977 |
| Dan          | Harris         |        256 |
| Freida       | Harris         |        428 |
| Jhumpa       | Lahiri         |        489 |
| George       | Saunders       |        367 |
| Patti        | Smith          |        304 |
| John         | Steinbeck      |        181 |
+--------------+----------------+------------+
12 rows in set (0.02 sec)
```
## AVERAGE
```
mysql> SELECT AVG(pages)
    -> FROM books;
+------------+
| AVG(pages) |
+------------+
|   348.5789 |
+------------+
1 row in set (0.00 sec)

mysql> SELECT released_year, AVG(stock_quantity)
    -> FROM books
    -> GROUP BY released_year;
+---------------+---------------------+
| released_year | AVG(stock_quantity) |
+---------------+---------------------+
|          1945 |             95.0000 |
|          1981 |             23.0000 |
|          1985 |             49.0000 |
|          1989 |             12.0000 |
|          1996 |             97.0000 |
|          2000 |             68.0000 |
|          2001 |            134.3333 |
|          2003 |             66.0000 |
|          2004 |            172.0000 |
|          2005 |             92.0000 |
|          2010 |             55.0000 |
|          2012 |            154.0000 |
|          2013 |             26.0000 |
|          2014 |             29.0000 |
|          2016 |             43.0000 |
|          2017 |           1000.0000 |
+---------------+---------------------+
16 rows in set (0.00 sec)

mysql> SELECT author_fname, author_lname, AVG(pages) FROM books
    -> GROUP BY author_lname, author_fname;
+--------------+----------------+------------+
| author_fname | author_lname   | AVG(pages) |
+--------------+----------------+------------+
| Raymond      | Carver         |   351.0000 |
| Michael      | Chabon         |   634.0000 |
| Don          | DeLillo        |   320.0000 |
| Dave         | Eggers         |   431.0000 |
| David        | Foster Wallace |   336.0000 |
| Neil         | Gaiman         |   325.6667 |
| Dan          | Harris         |   256.0000 |
| Freida       | Harris         |   428.0000 |
| Jhumpa       | Lahiri         |   244.5000 |
| George       | Saunders       |   367.0000 |
| Patti        | Smith          |   304.0000 |
| John         | Steinbeck      |   181.0000 |
+--------------+----------------+------------+
12 rows in set (0.01 sec)
```
## Aggregate Function Challenge
```
mysql> SELECT COUNT(*) FROM books;
+----------+
| COUNT(*) |
+----------+
|       19 |
+----------+
1 row in set (0.00 sec)

mysql> SELECT released_year, COUNT(*) FROM books GROUP BY released_year;
+---------------+----------+
| released_year | COUNT(*) |
+---------------+----------+
|          1945 |        1 |
|          1981 |        1 |
|          1985 |        1 |
|          1989 |        1 |
|          1996 |        1 |
|          2000 |        1 |
|          2001 |        3 |
|          2003 |        2 |
|          2004 |        1 |
|          2005 |        1 |
|          2010 |        1 |
|          2012 |        1 |
|          2013 |        1 |
|          2014 |        1 |
|          2016 |        1 |
|          2017 |        1 |
+---------------+----------+
16 rows in set (0.00 sec)

mysql> SELECT author_fname, author_lname, AVG(released_year) FROM books GROUP BY author_lname, author_fname;

+--------------+----------------+--------------------+
| author_fname | author_lname   | AVG(released_year) |
+--------------+----------------+--------------------+
| Raymond      | Carver         |          1985.0000 |
| Michael      | Chabon         |          2000.0000 |
| Don          | DeLillo        |          1985.0000 |
| Dave         | Eggers         |          2008.6667 |
| David        | Foster Wallace |          2004.5000 |
| Neil         | Gaiman         |          2006.6667 |
| Dan          | Harris         |          2014.0000 |
| Freida       | Harris         |          2001.0000 |
| Jhumpa       | Lahiri         |          1999.5000 |
| George       | Saunders       |          2017.0000 |
| Patti        | Smith          |          2010.0000 |
| John         | Steinbeck      |          1945.0000 |
+--------------+----------------+--------------------+
12 rows in set (0.00 sec)

mysql> SELECT CONCAT(author_fname, ' ', author_lname) FROM books
    -> WHERE pages = (SELECT Max(pages) FROM books);
+-----------------------------------------+
| CONCAT(author_fname, ' ', author_lname) |
+-----------------------------------------+
| Michael Chabon                          |
+-----------------------------------------+
1 row in set (0.00 sec)

mysql> SELECT CONCAT(author_fname, ' ', author_lname) FROM books
    -> ORDER BY pages DESC LIMIT 1;
+-----------------------------------------+
| CONCAT(author_fname, ' ', author_lname) |
+-----------------------------------------+
| Michael Chabon                          |
+-----------------------------------------+
1 row in set (0.00 sec)

mysql> SELECT pages, CONCAT(author_fname, ' ', author_lname) FROM books
    -> ORDER BY pages DESC;
+-------+-----------------------------------------+
| pages | CONCAT(author_fname, ' ', author_lname) |
+-------+-----------------------------------------+
|   634 | Michael Chabon                          |
|   526 | Raymond Carver                          |
|   504 | Dave Eggers                             |
|   465 | Neil Gaiman                             |
|   437 | Dave Eggers                             |
|   428 | Freida Harris                           |
|   367 | George Saunders                         |
|   352 | Dave Eggers                             |
|   343 | David Foster Wallace                    |
|   329 | David Foster Wallace                    |
|   320 | Don DeLillo                             |
|   304 | Neil Gaiman                             |
|   304 | Patti Smith                             |
|   291 | Jhumpa Lahiri                           |
|   256 | Dan Harris                              |
|   208 | Neil Gaiman                             |
|   198 | Jhumpa Lahiri                           |
|   181 | John Steinbeck                          |
|   176 | Raymond Carver                          |
+-------+-----------------------------------------+
19 rows in set (0.00 sec)

mysql> SELECT released_year AS year,
    ->     COUNT(*) AS '# of books',
    ->     AVG(pages) AS 'avg pages'
    -> FROM books
    ->     GROUP BY released_year;
+------+------------+-----------+
| year | # of books | avg pages |
+------+------------+-----------+
| 1945 |          1 |  181.0000 |
| 1981 |          1 |  176.0000 |
| 1985 |          1 |  320.0000 |
| 1989 |          1 |  526.0000 |
| 1996 |          1 |  198.0000 |
| 2000 |          1 |  634.0000 |
| 2001 |          3 |  443.3333 |
| 2003 |          2 |  249.5000 |
| 2004 |          1 |  329.0000 |
| 2005 |          1 |  343.0000 |
| 2010 |          1 |  304.0000 |
| 2012 |          1 |  352.0000 |
| 2013 |          1 |  504.0000 |
| 2014 |          1 |  256.0000 |
| 2016 |          1 |  304.0000 |
| 2017 |          1 |  367.0000 |
+------+------------+-----------+
16 rows in set (0.00 sec)
```

