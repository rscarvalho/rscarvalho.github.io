---
layout: post
title: "Taking advantage of your rails model generator"
date: 2014-11-30 09:51:26 -0500
comments: true
categories: [rails, ruby, generators, web frameworks, backend]
---

This is a quick trick I haven't explored until now (no really, didn't know it like 5 minute ago).

When you're calling `rails g model` to generate your models, you have the option to pass in the field names inline, like this:

```sh
rails g model UserRole user_id:integer role_id:integer extra_permissions:text
```

The example above has something interesting: you create two columns of type `integer`: `role_id` and `user_id`. What you really want to express, however, is that you want ot hook up two *associations* in your `UserRole` model: `belongs_to :role` and `belongs_to :user`. After you generate this migration, you may have to do a couple of things by hand:

* add `add_index` commands on the migration to create the index on `role_id` and `user_id` **before** running `rake db:migrate`
* add `belongs_to` associations in `app/models/user_role.rb`

Well, all of this manual typing can be just eliminated if you use this syntax instead:

```sh
rails g model UserRole user:belongs_to role:belongs_to extra_permissions:text
```

That's it! We express the model with its **data relations** instead of raw database columns. As you can see in the generated code, rails already included the appropriate `belongs_to` and indexes to the files, like below:

```ruby app/models/user_role.rb
class UserRole < ActiveRecord::Base
  belongs_to :user
  belongs_to :role
end
```

And to the migration file:

```ruby db/migrate/20141130144340_create_user_roles.rb
class CreateUserRoles < ActiveRecord::Migration
  def change
    create_table :user_roles do |t|
      t.belongs_to :user, index: true
      t.belongs_to :role, index: true
      t.text :extra_permissions
  
      t.timestamps
    end
  end
end
```

All done in a single call to `rails g`. Hope you enjoy!