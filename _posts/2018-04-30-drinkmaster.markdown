---
layout: post
title:      "DrinkMaster"
date:       2018-04-30 12:05:13 -0400
permalink:  drinkmaster
---


The concept of DrinkMaster is fairly straightforward.  I wanted a resource to host liquor recipes, add them to a playlist - or "DrinkMix", have the ability to create an account to enable basic CRUD functions pertaining to the recipes, and be able to sign in via Facebook. At first, it didn't sound overtly difficut. It was. 

For starters, I enabled Bootstrap and Devise in order to modify the theme and authorization into my site:

![](https://i.imgur.com/cE2hHac.png)

Bootstrap was fundamental to the core of the entire site. It enabled me to create dropdowns, a beautiful URI, and provided the format for my search bars. Not only this, but it came preset with quite a bit of the navigation toolbar which was used in the project:

![](https://i.imgur.com/GoaTvTw.png)

After initializing the devise and bootstrap foundations, I created the migrations. These started with few, and very rapidly, built up to many. Below is a diagram of the tables and their relationships: 

![](https://i.imgur.com/BspfrB9.png)

Explained:

<ul>
<li>User has_many :user_recipes</li>
<li>User has_many :recipes, through: :user_recipes</li>
<li>User has_many :drink_mixes</li>
<li>User has_many :recipes, through :drink_mixes</li>
</ul>

<ul>
<li>UserRecipe belongs_to :user</li>
<li>UserRecipe belongs_to :recipe</li>
</ul>

<ul>
<li>Recipe has_many :user_recipes</li>
<li>Recipe has_many :users, through :user_recipes</li>
<li>Recipe has_many :ingredients</li>
<li>Recipe belongs_to :liquor</li>
<li>Recipe has_many :drink_mix_recipes</li>
<li>Recipe has_many :drink_mixes, through: :drink_mix_recipes</li>
<li>Recipe :accepts_nested_attributes_for :ingredients</li>
</ul>

<ul>
<li>Liquor has_many :recipes</li>
</ul>

<ul>
<li>Ingredient belongs_to :recipe</li>
</ul>

<ul>
<li>DrinkMix has_many :drink_mix_recipes</li>
<li>DrinkMix has_many :recipes, through: :drink_mix_recipes</li>
</ul>



These migrations provided to be quite the challenge when it came to routing and custom resources. The project called for various nested routes, with a "user-submittable attribute" on the join table of one of my many_to_many associations. For this, I chose "Rank" on the join table of drink_mix_recipes. This effectively allowed the user to rate their recipes on a scale of 1 to 10: 

![](https://i.imgur.com/qpw45sT.png)

This gave the user a semblence of memory as to whether or not the drink recipe was particularly enjoyable. Pragmatic? Sort of. In my mind, as the list of recipes on their "DrinkMix" - or playlist - grew, it would be harder and harder to keep track of which recipes were good and which recipes weren't. Hence, rank. 

<br>

Now, adding a recipe to a desired DrinkMix list was a trouble all on its own and required a custom route and action on the RecipesController: 

![](https://i.imgur.com/HHSiE6c.png)

![](https://i.imgur.com/EsDkPyJ.png)

![](https://i.imgur.com/rvDpiA4.png)

Essentially, I created a form_tag element in order to route to my custom resource. From there, the collection_select tool was used in order to grab all of my DrinkMixes and their respective IDs to submit via params to my RecipesController which pushed in the ranking of the recipe as well as its ID to the drink_mix table. 

The rest of the project would take forever to explain, which is why you should check it out here:
[https://github.com/CatalanoWebDevelopment/DrinkMaster](https://github.com/CatalanoWebDevelopment/DrinkMaster) <br>

Leave me some feedback for improvements and any glitches you may run into at: <br>
catalano.work@gmail.com <br>

I appreciate the support! <br>

-Parker







