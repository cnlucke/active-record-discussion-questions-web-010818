# ActiveRecord Discussion Questions

## Part One - Reading the Documentation

Looking at Documentation is an important part of programming. You don't have to memorize anything, but you should get familiar with the types of information you can find in different docs. For this exercise, go through the ActiveRecord documentation [here](http://guides.rubyonrails.org/active_record_querying.html#retrieving-objects-from-the-database) with your table mates and answer the following questions about each method.

1. What argument or arguments does the method take?
2. What type of object does the method return?
3. What happens if none of the parameters match? (i.e. what if `Tweet.find(5)` can't find that tweet? How about `Tweet.find_by(id: 6)`?

Methods:

1. `find`
    a. Takes: A primary key value or an array of primary key values.
    b. Type of object returned: class instance for single primary key provided, or array of class instances when array of primary keys is provided.
    c. Unmatched parameters causes: "ActiveRecord::RecordNotFound: Couldn't find Movie with 'id'=<id>"
2. `.find_by` (finds the first record matching some conditions)
    a. Takes: A column name as a symbol with the value you're looking for.
    b. Type of object returned: class instance for first matching record
    c. Unmatched parameters causes: If no record found it returns nil
3. `.where`
    a. Takes: conditions similar to the WHERE statement in SQL. Can be in the form of a string, array, or hash. The first argument is a string of the condition using "?" or a symbol as a placeholder for any parameters and followed by parameters referenced in the condition if used.
    b. Type of object returned: array of class instances matching condition
    c. Unmatched parameters causes: empty array to be returned
4. `.all`
    a. Takes: no argument
    b. Type of object returned: entire table as an array of object instances
    c. Unmatched parameters causes: N/A
5. `.first`
    a. Takes: no argument
    b. Type of object returned: first instance of class object in order returned by what is left of .first
    c. Unmatched parameters causes: nil
6. `.destroy`
    a. Takes: a single primary key or an array of primary keys
    b. Type of object returned: Either single class instance of record destroyed or an array of class instances of multiple records destroyed
    c. Unmatched parameters causes: ActiveRecord::RecordNotFound error

## Part Two - Name that SQL!

Pretend that you have a `tweets` table with two columns - `message` and `user_id`. Given the code below, write in a notebook or on a whiteboard what SQL statements will fire when the following methods are called?

```
class Tweet < ActiveRecord::Base

end
```

1. `Tweet.all`
```
  SELECT * from tweets;
```
2. `Tweet.find(5)`
```
  SELECT * from tweets WHERE user_id = 5;
```
3. `Tweet.find_by(user_id: 7)`
```
  SELECT * from tweets WHERE user_id = 7;
```
4. `Tweet.where(user_id: 7)`
```
  SELECT * from tweets WHERE user_id = 7;
```
5. `Tweet.create(user_id: 5, message: 'making some coffee')`
```
  INSERT INTO tweets VALUES (5, 'making some coffee');
```
6. `Tweet.destroy(7)`
```
  DELETE FROM tweets WHERE user_id = 7;
```
