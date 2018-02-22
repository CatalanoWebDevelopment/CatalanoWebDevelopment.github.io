---
layout: post
title:      "MMOFreaks, Sinatra and Activerecord"
date:       2018-02-22 14:12:34 -0500
permalink:  mmofreaks_sinatra_and_activerecord
---


I created MMOFreaks in order to save meta builds from the massively online roleplaying game, Neverwinter. I intend to add a lot more substance to the forms and to the gem itself in order to instantiate artifacts, pictures, equipment stats, etc. Below is a rough outline of how I made it!

### The Table Setup

![](https://i.imgur.com/1b1BwCJ.png)

As you can see, it got a bit complicated. Essentially, I have to join tables: `gear_equipments` and `builds`. The following associations were made using these:


<ul>
<li>A `user` has_many `builds`</li>
<li>A `user` has_many `comments`</li>
<li>A `build` belongs_to `user`</li>
<li>A `comment` belongs_to `user`</li>
<li>A `build` belongs_to `klass`</li>
<li>A `klass` has_many `builds`</li>
<li>A `build` belongs to `karacter`</li>
<li>A `karacter` has_many `builds`</li>
<li>A `build` has_many `gear_equipments`</li>
<li>A `build` has_many `gears`, through: :`gear_equipments`</li>
<li>A `gear` belongs_to `gear_equipment`</li>
<li>A `build` has_many `comments`</li>
<li>A `comment` belongs_to `build`</li>
</ul>

Pretty intense right? You also may notice some of the more strange spelling of things. There are a few reasons for this. First, `gear` was originally `equipment`; however, because equipment is both singular AND plural, ActiveRecord had difficulty determining which was a table and which was a model. Additionally, because `class` is a protected attribute withing ActiveRecord, I needed to change the spelling to `klass` - ignoring the "c" to trick the models. Additionally, `karacter` was initially `race`, then `character`, but unfortunately, both were also protected classes of ActiveRecord as well. Let's just say that I had to jump through quite a few hoops in order to get this bad boy running (haha). 

### The Slug

![](https://i.imgur.com/akeMxR3.png)

First of all, what is a slug?

> A slug is used to create a name that is not acceptable as a URL for various reasons (special characters, spaces, etc). 

This is great because instead of having a route like /songs/1, you can have a route /songs/hotline-bling which is a much more descriptive route name. In my model, I "slugify" the usernames in order to present them in the appropriate routes of my server. This would give a url such as `https://localhost9393/users/parker`. Not too shabby! The `find_by_slug(slug)` method allows me to locate the slugs in the url when passed through a params hash. 

###  Here's An Example

![](https://i.imgur.com/x0YXx8m.png)

When I find the user's slug, I can associate an instance variable to the user in order to grab that **specific** user. When I go to post to my view page, only that instance of the user would be present. This allows for much more dynamic routes, which allow me to post things such as "Welcome, Parker!" in my headlines. 

###  Logged_in? and Current_User

![](https://i.imgur.com/9gwBBYn.png)

Helper Methods? Yes please! These allow me to indicate which user is currently logged into the individual session. By calling things such as `current_user.builds` or `current_user.username` I can find information specific to that instance of the session. 

###  Here's An Example

![](https://i.imgur.com/2vkayFd.png)

If you can't tell what's being done already, I am simply checking for the specific instance of a build on the build's show page and comparing it to an array of what is held in the current user's repertoire of builds. If the current user owns, or has access to, the currently displayed build, then they are allowed access to the use of editing and deleting forms. 


### Want to See More?

If you enjoy the whole concept of this gem and would like to contribute or see more of the code, please visit:

https://github.com/CatalanoWebDevelopment/MMOFreaks

Additionally, if you have any questions regarding this repository, please do not hesitate to send me an email at:

catalano.work@gmail.com

Enjoy! <3

