---
layout: post
title:      "Sinatra Project"
date:       2020-06-28 22:54:23 -0400
permalink:  sinatra_project
---

My project is a forum for guitar players and ethusiast. I chose to do it specifically for guitar players because I am very passionate about guitars, and helping this community connect is a rewarding feeling. 

I learned one thing builiding this project that will definetly stay with me because it helps keep your code clean, organized and DRY. Before I built this project I learned about helper methods, these are methods to simplify and clean your code, people told me about them and their importance, but at the time they seemed unintersting and boring. Building this project made me realize the usefulness if these methods becuase to handle a lot of the requests in my webapp I had to go through the same logic over and over. This meant writing the same lines of code many times which does not look nice and it can sometimes get a lottle confusing and harder to follow.

Here is an example:
```
    get '/posts/:id/edit' do
        post = Post.find_by_id(params[:id])
        if !logged_in? 
            @error = "Please log in"
            erb :'/users/login'
        elsif post && current_user == post.user 
            @post = post
            erb :'/posts/edit'
        else
            redirect '/posts'
        end
    end
```

With helper methods this got transformed to this:
```
    get '/posts/:id/edit' do
        log_in_required
        authorization_required
        @post = Post.find_by_id(params[:id])
        erb :'/posts/edit'
   end
```
In my webapp I had to check if a user had permission or if they were logged in many times. To clean up my code I wrote these helper methods that made my code more abstract, cleaner and easier to read. What was first 12 lines of code is now 6... this is amazing! You get to keep all of your codes functionality, but now it looks better and it's easier to read; it's definetly a win-win. If you ever find yourself going writing the same logic over and over, you need helper methods; it'll make your life way easier.


