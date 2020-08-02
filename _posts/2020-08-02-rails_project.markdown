---
layout: post
title:      "Rails Project"
date:       2020-08-02 21:43:35 +0000
permalink:  rails_project
---


For my rails project I made a webapp called WorkoutBuddy, and like the name suggests, with this app you can create workout plans with exercises, and also, add them to your calendar. So you can keep track of your own workout schedule. You can also share your workouts with everyone, so anyone else can add them to their schedule. 

The process of building this app was vey fun and challenging; this project tested my patient many times and made me realize how important it is to be patient with yourself when learning. When I was building out my project, I made the relationship of User and Workout only thorugh a join table, but then I also wanted to have Users and Workouts to have a direct relation ship. This is a part of rails I found very fascinating and useful:

At first:
```
class User < ApplicationRecord
    has_many :scheduled_workouts  #join table
    has_many :workouts, through: :scheduled_workouts
		...
end

class Workout < ApplicationRecord
    has_many :scheduled_workouts  #join table
    has_many :users, through: :scheduled_workouts
		...
end
```

Since I wanted to make a User `have_many :created_workouts` and Workout `belongs_to :user`, just putting a foreign key in the Workout table wasn't going to cut it because the User already `has_many :workouts`. So I started by adding a `user_id` column to Workout table:

```
class AddUserIdToWorkout < ActiveRecord::Migration[6.0]
    def change
      add_column :workouts, :user_id, :integer
    end
end
```

In my Workout class I added `belongs_to :user` and to specify what to call the array of `created_workouts` in my User class I added:

```
class User < ApplicationRecord
    has_many :created_workouts, foreign_key: "user_id", class_name: "Workout"
end
```

Now when `#created_workouts` is called on a user instance, it knows to look inside the Workout class for the foregn key of `user_id`. This is an easy way to customize the names of any foreign key in your models.


