# Intro to Rails

Start up the Rails server:

```bash
rails server
```

Create a new model:

```bash
rails g model Dinosaur name:string age:integer image_url:string
```

Create a new controller:

```bash
rails g controller Dinosaurs
```

## Routes

Check the routes:

```bash
rails routes
```

## Database

Create the database:

```bash
rails db:create
```

Create a new migration:

```bash
rails g migration AddValleyToDinosaurs valley:references
```

Run the migrations:

```bash
rails db:migrate
```

Check the status of the migrations:

```bash
rails db:migrate:status
```

Seed the database:

```bash
rails db:seed
```

Or reset the database before hand if you have already seeded it before (it clears out the old data first):

```bash
rails db:reset db:seed
```

## Rails Console

You can start up a new session of the Rails console by running `rails console` in your terminal:

```bash
rails console
```

You should see the following output:

```bash
Running via Spring preloader in process 1157
Loading development environment (Rails 5.0.0)
>>
```

During the class you'll often see us clear out the console. To do that, we use `Command + K` on the Mac. You can also use `Ctrl + L` to clear the screen of your terminal, which works on both Mac and Linux.

The Rails console does not automatically reload code when you make changes in your project files. You could refresh the code by existing the console and starting a new session but there is a better way to do that. Instead, use the `reload!` command to pick up the latest version of your code:

```bash
>> reload!
Reloading...
=> true
```
