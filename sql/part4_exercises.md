# SQL Part 4: Exercises
----

There may be other ways to achieve the same result.  Remember that SQL commands are not case sensitive (but data values are).

## Exercise: Alter

Create and populate the `food` table below using the commands provided. 

Then add a new text column `color`.

Read how to alter a table by [changing a column name](http://www.postgresqltutorial.com/postgresql-rename-column/) (or [official documentation](https://www.postgresql.org/docs/current/static/sql-altertable.html)).  Then rename the `color` column you just created to `primary_color`.

```sql
CREATE TABLE food (
	id serial primary key,
	name text not null,
	type text,
	favorite boolean default false	
);

INSERT INTO food (name, type) 
VALUES 
	('broccoli','vegetable'), 
	('lime', 'fruit'), 
	('green beans', 'vegetable'), 
	('milk', 'dairy'), 
	('yogurt', 'dairy'), 
	('banana', 'fruit'), 
	('lemon', 'fruit'), 
	('tortilla', 'carbohydrate'), 
	('rice', 'carbohydrate');
``` 


## Exercise: Update

Using the food table created and altered above, set the values of the `primary_color` column.  Then set the values of the `favorite` column based on your favorites.


## Exercise: Delete

Using the table created, altered, and updated above, delete any white foods that aren't a favorite.


## Challenging Exercise: Update with Join

Read about [updating via a join](http://www.postgresqltutorial.com/postgresql-update-join/) (or [official documentation](https://www.postgresql.org/docs/9.6/static/sql-update.html)).

Create and populate tables using the supplied code below.

Then set the value of `last_taught` in `course` to the most recent date the course was taught using the `course_offering` table.

Hint: you'll need to join to a subquery (the results of another query).  Think first about how to get the most recent date for each course, and then how to use that information in the update.

```sql
CREATE TABLE course (
	id int primary key,
	name text not null,
	last_taught date
);

INSERT INTO course (id, name) 
VALUES 
	(1, 'Chemistry'),
	(2, 'Physics'),
	(3, 'History'),
	(4, 'English'),
	(5, 'French');
	
CREATE TABLE course_offering (
	course_id int references course(id),
	quarter_name text,
	date date,
	primary key (course_id, quarter_name)
);

INSERT INTO course_offering 
VALUES 
	(1, 'Spring 2015', '2015-03-01'),
	(1, 'Spring 2017', '2017-03-01'),
	(2, 'Fall 2016', '2016-09-01'),
	(2, 'Spring 2017', '2017-03-01'),
	(3, 'Spring 2016', '2016-03-01'),
	(4, 'Winter 2015', '2015-01-01'),
	(4, 'Winter 2017', '2017-01-01'),
	(4, 'Winter 2016', '2016-01-01');
```


