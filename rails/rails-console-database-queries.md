# Rails Console / Database Queries

## find

Find by id - This can either be a specific id (1), a list of ids (1, 5, 6), or an array of ids ([5, 6, 10]). If no record can be found for all of the listed ids, an error will be raised.

```ruby
post = Post.find(1)
# SELECT  "posts".* FROM "posts" WHERE "posts"."id" = $1 LIMIT 1  [["id", 1]]
# => #<Post id: 1, title: "How to code in Rails", post: "Great, great explanation", created_at: "2016-06-13 12:11:44", updated_at: "2016-06-13 12:11:44", user_id: 1>
```

In your application you will often use the ID from the URL:

```ruby
post = Post.find(params[:id])
```

`params` is an object that contains URL parameters. The ID is the number that's in the URL: `http://localhost:3000/posts/1` or `http://localhost:3000/posts/1/edit`.


## find_by

Finds the first record matching the specified conditions. There is no implied ordering so if order matters, you should specify it yourself. If no record is found, returns nil.

```ruby
post = Post.find_by(title: "Relations")
#  SELECT  "posts".* FROM "posts" WHERE "posts"."title" = $1 LIMIT 1  [["title", "Relations"]]
# => #<Post id: 3, title: "Relations", post: "All the great Relations", created_at: "2016-06-13 12:11:44", updated_at: "2016-06-13 12:11:44", user_id: 2>
```

Or with multiple conditions:

```ruby
comment = Comment.find_by(user_id: 3, post_id: 2)
# SELECT  "comments".* FROM "comments" WHERE "comments"."user_id" = $1 AND "comments"."post_id" = $2 LIMIT 1  [["user_id", 3], ["post_id", 2]]
# => #<Comment id: 2, comment: "Meh", user_id: 3, post_id: 2, created_at: "2016-06-13 12:11:44", updated_at: "2016-06-13 12:11:44">
```

## all

Returns all the records for the given model:

```ruby
posts = Post.all
# => #<ActiveRecord::Relation [#<Post id: 1, title: "How to code in Rails", post: "Great, great explanation", created_at: "2016-06-13 12:11:44", updated_at: "2016-06-13 12:11:44", user_id: 1>, #<Post id: 2, title: "Models", post: "All the great Rails Models", created_at: "2016-06-13 12:11:44", updated_at: "2016-06-13 12:11:44", user_id: 1>, #<Post id: 3, title: "Relations", post: "All the great Relations", created_at: "2016-06-13 12:11:44", updated_at: "2016-06-13 12:11:44", user_id: 2>]>
```

## first, second, third, fourth, fifth, last

Get the first, second, third, fourth, fifth or last record from the returned set:

```ruby
Comment.first
# SELECT  "comments".* FROM "comments"  ORDER BY "comments"."id" ASC LIMIT 1
# => #<Comment id: 1, comment: "Great article", user_id: 3, post_id: 1, created_at: "2016-06-13 12:11:44", updated_at: "2016-06-13 12:11:44">

Comment.second
# SELECT  "comments".* FROM "comments"  ORDER BY "comments"."id" ASC LIMIT 1 OFFSET 1
# => #<Comment id: 2, comment: "Meh", user_id: 3, post_id: 2, created_at: "2016-06-13 12:11:44", updated_at: "2016-06-13 12:11:44">

Comment.last
# SELECT  "comments".* FROM "comments"  ORDER BY "comments"."id" DESC LIMIT 1
# => #<Comment id: 3, comment: "Frist post!", user_id: 4, post_id: 1, created_at: "2016-06-13 12:11:44", updated_at: "2016-06-13 12:11:44">
```

## limit

Limits the number of records returned and does it through the database so things stay speedy.

```ruby
Comment.all.limit 2 # Returns the first 2 comments
# SELECT  "comments".* FROM "comments" LIMIT 2
# => #<ActiveRecord::Relation [#<Comment id: 1, comment: "Great article", user_id: 3, post_id: 1, created_at: "2016-06-13 12:11:44", updated_at: "2016-06-13 12:11:44">, #<Comment id: 2, comment: "Meh", user_id: 3, post_id: 2, created_at: "2016-06-13 12:11:44", updated_at: "2016-06-13 12:11:44">]>
```

## where

Returns an array of results (can be empty), which is the result of filtering according to the conditions in the arguments.

```ruby
Comment.where(user_id: 3)
# SELECT "comments".* FROM "comments" WHERE "comments"."user_id" = $1  [["user_id", 3]]
# => #<ActiveRecord::Relation [#<Comment id: 1, comment: "Great article", user_id: 3, post_id: 1, created_at: "2016-06-13 12:11:44", updated_at: "2016-06-13 12:11:44">, #<Comment id: 2, comment: "Meh", user_id: 3, post_id: 2, created_at: "2016-06-13 12:11:44", updated_at: "2016-06-13 12:11:44">]>

Comment.where(created_at: (Time.now - 7.day)..Time.now) # Created in the last 7 days
# SELECT "comments".* FROM "comments" WHERE ("comments"."created_at" BETWEEN '2016-06-06 20:28:44.067321' AND '2016-06-13 20:28:44.067573')
# => #<ActiveRecord::Relation [#<Comment id: 1, comment: "Great article", user_id: 3, post_id: 1, created_at: "2016-06-13 12:11:44", updated_at: "2016-06-13 12:11:44">, #<Comment id: 2, comment: "Meh", user_id: 3, post_id: 2, created_at: "2016-06-13 12:11:44", updated_at: "2016-06-13 12:11:44">, #<Comment id: 3, comment: "Frist post!", user_id: 4, post_id: 1, created_at: "2016-06-13 12:11:44", updated_at: "2016-06-13 12:11:44">]>
```

## order

```ruby
User.order(:name)
# SELECT "users".* FROM "users"  ORDER BY "users"."name" ASC

User.order(email: :desc)
# SELECT "users".* FROM "users"  ORDER BY "users"."email" DESC
```

## Chain them

```ruby
User.where(last_name: "Jansen").order(:first_name).first
```
