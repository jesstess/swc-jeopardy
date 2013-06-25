Goals for this project
======================

* Get experience with SQL and querying a relational database.

* Get experience using sqlite3 to query a sqlite database from within
  a Python script.


Dependencies and installation
=============================

1. If you don't already have it, please install SQLite:

Precompiled SQLite binaries for all platforms can be found at:
http://www.sqlite.org/download.html

2. Test database access

jeopardy.db is a sqlite database containing many years of actual
Jeopardy data! Check that you can interact with this database by
running:

    sqlite3 jeopardy.db

You should see a sqlite> prompt.


1. SQLite basics
================

a) Start SQLite by running "sqlite3 jeopardy.db". Then look at the
schema for the category and clue tables in the database:

sqlite> .table
category  clue
sqlite> .schema category
CREATE TABLE "category" (
    id INTEGER PRIMARY KEY,
    name VARCHAR(255) NOT NULL,
    game INTEGER NOT NULL,
    boardPosition INTEGER
    );
sqlite> .schema clue
CREATE TABLE "clue" (
    id INTEGER PRIMARY KEY,
    text VARCHAR(255) NOT NULL,
    category_id INTEGER NOT NULL,
    value INTEGER NOT NULL,
    answer VARCHAR(255) NOT NULL,
    round INTEGER
);

b) What is a schema? What kinds of data types are represented in these tables?

c) Make some simple SELECT queries from the sqlite prompt:

SELECT * FROM category;
SELECT NAME FROM category;
SELECT * FROM clue;
SELECT text, answer, value FROM clue;
SELECT text, answer, value FROM clue LIMIT 10;


2. jeopardy_categories.py
=========================

a) Examine jeopardy_categories.py and then run the script.

b) Go back to the script and carefully examine the steps for
retrieving data from a database in Python:

- setting up the database connection
- forming and executing a query
- retrieving and printing the results

c). Modify the code to print both the category and game number.


3. jeopardy_clues.py
====================

a) Examine jeopardy_clues.py and then run the script.

b) Modify the code to only print clues with an $800 value.


4. Daily doubles
================

Write a script that prints 10 daily doubles and their responses. The
`clue` table has an `isDD` field.


5. Category clues
=================

Write a script that randomly chooses a category and prints clues from
that category.

Hint: SQL supports an "ORDER BY RANDOM()" clause that will return rows
in a random order. For example, to randomly pick 1 category id you
could use:

  SELECT id FROM category ORDER BY RANDOM() LIMIT 1


6. Game categories
==================

Write a script to randomly choose a game number (the category table
has a `game` field) and print the categories from that game.


7. Most common categories
=========================

Read about GROUP BY and ORDER BY clauses and write a script using them
to print the 20 most common categories.

An example of using GROUP BY and ORDER BY to produce an ordered list
of counts on a generic `foo` field is:

  SELECT foo, COUNT(foo) AS count FROM my_table GROUP BY foo ORDER BY count
