# Anagram Server 2 Ludicrous Speed 
 
##Learning Competencies 

##Summary 

 Our last Anagram Server had a single database table, `words`, with maybe four columns: `(id, word, created_at, updated_at)`.  The dictionary file we imported contained around 250,000 words.

We want to augment our database schema to make the operation "give me all the anagrams of a particular word" fast and simple.  We're talking [ludicrous speed](http://www.youtube.com/watch?v=mk7VWcuVOf0).

## Learning Goals

- Learn about [ActiveRecord callbacks](http://guides.rubyonrails.org/active_record_validations_callbacks.html#callbacks-overview).
- Gain familiarity with a particularly common read / write performance tradeoff.

## Objectives

### Develop a Strategy

What data can we add to the database to make querying for anagrams easier?  Ideally it'd be as simple as:

```sql
SELECT * FROM words WHERE some_field = some_value
```

The nature of `some_field` and `some_value` are for you to determine and define.  `some_value` will not be the word you're interested in finding anagrams for, but it will be determined by it.  Any word that is anagram will share the same `some_value`.

You'll want to set the value of this field using the ActiveRecord `before_save` callback.

### Migrations &amp; Database Indexes

You'll need to create a new migration to add any new fields to your `words` table.  Additionally, you'll want to index these new fields if you're going to be querying against them.

A database index is an auxiliary data structure which allows for faster retrieval of data stored in the database at the cost of maintaining the consistency of all the indexes.  They are keyed off of a specific column or set of columns so that queries like "Give me all people with a last name of 'Smith'" are fast.

### Submit It!

Upload any files you've changed to a gist and post that as your attempt.

## More on Database Indexes

This is purely extra; the below will make more sense later in DBC and after you've been playing around with databases for a few weeks.  Don't sweat it if everything below sounds crazy.

In some instances they work like a hash, e.g., you could imagine a hash where the keys were last names and the values were an array of people with those last names.  Every time we inserted or updated data in the database we'd have to make sure to do the same to our hash index.

This doesn't work for a wide variety of queries, though, like "Give me all people who have been members of our site for longer than a year" or "Give me all the people whose last name begins with 'R'."  For this reason the default data structured used in most databases is something more general than a hash table.

If you're curious, you can read more about [what index types Postgres supports](http://www.postgresql.org/docs/9.0/static/indexes-types.html).  The default index type for most databases is a [B-tree](http://en.wikipedia.org/wiki/B-tree) because it allows for generally efficient inserting, updating, deleting, and searching using both equality and comparison, i.e., `=`, `<`, `>`, `<=`, and `>=`.

Here is an old blog post from Jesse about [database indexes](http://20bits.com/article/interview-questions-database-indexes), which are a common interview question.
 

##Releases
###Release 0 

##Optimize Your Learning 

##Resources