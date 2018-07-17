---
layout: post
title:      "DrinkMaster-Deluxe, The Addition Of JavaScript"
date:       2018-07-17 18:20:46 +0000
permalink:  drinkmaster-deluxe_the_addition_of_javascript
---


So I was tasked to implement a few things involving jQuery and JavaScript. Among them, were AJAX calls, rendering views with JSON, JavaScript Object Models, and the (oh so amazing) Active Model Serializer. I was not too suprised to find out how challenging this actually turned out to be! I was dreadful when it came to JS. I fell hard for Ruby on Rails, and the transition was utterly painful. However, jQuery and JS did seem to grow on me little by little as I started to understand more of how the code worked. 

For example, this implementation of a JavaScript Object Model. What the heck is that right? Essentially, it is a constructor function which allows the creation of Objects with a particular initial set of properties and values. These properties can then be called upon in prototype method calls to display their respective values in the DOM. Providing evidence of this, take a look at the code below: 

![JS Object Model Example Code and Implementation](https://i.imgur.com/KDOW0oe.png)

First, I created the Recipe Object Model with the properties of *name*, *description*, and *ingredients*. I then call `.prototype` on this new Recipe object - which allows me to add new properties to my constructor - in order to build out my `renderIngredients` function. This function references the the properties instantiated in my constructor to append `<li>`'s with the respective ingredient information of *name* and *quantity* generated from my `nextRecipe` method on the RecipesController. To walk you through the process, I call `$(function() {}` first in order to render my JavaScript code **after** the page has fully loaded. I then target my button that has a class of `"js-next"` using the jQuery selector method of `$(".js-next")`. Once this button is found, it responds to an `onClick()` event with a function that carries an argument of *e* (or event) in order to call my `e.preventDefault()` method - which effectively prevents the loading of a new page and any inherit action that would be rendered from clicking on a link. Next, I define a current ID. This is found from the data-id on the button which is passed the information of the current recipe ID using embedded Ruby tags `<%= @recipe.id %>`. By defining the current ID, I am able to fire off an AJAX get request to the route of `/recipes/:id/next_recipe`, whose method is shown in the picture below. I then instantiate my Recipe Object Model with the data that is recieved through the request. Once my constructor is built, I call the `renderIngredients()` method in order to append the `<li>`'s to the `<div>` with the class of *ingredients*. This is what effectively builds out each nested ingredient. The previous shown content is then removed in order to display the new show content of the following recipe. An interesting line of code comes next - `history.replaceState()`. This method takes in three arguments: state object, title, url. If you're curious about this, visit [ReplaceStateMDN](https://developer.mozilla.org/en-US/docs/Web/API/History_API) for an in-depth walkthrough. What I am doing here is replacing my URL with the route fired off by the AJAX get request in order to pull the next recipes ID params. Finally, I implement this concept by replacing the current `data-id` of my button to the ID of the next available recipe. 

![RecipesController nextRecipe Method](https://i.imgur.com/OHpjS0L.png)

Now, you might be wondering what `render json: {@nextRecipe, serializer: RecipeSerializer, status: 200}` is doing. Good question! I am taking advantage of my ActiveModelSerializer (AMS) to render the information regarding the current recipe via JSON (JavaScript Object Notation). Here is what my AMS looks like: 

![Recipe AMS](https://i.imgur.com/d8kaFyp.png)

`Status: 200` indicates that the link is "OK". Here is a little description: 

> 200 OK
Standard response for successful HTTP requests. The actual response will depend on the request method used. In a GET request, the response will contain an entity corresponding to the requested resource. In a POST request, the response will contain an entity describing or containing the result of the action.

With the current understanding of AMS and jQuery Selectors, it's time to introduce the rendering of an index page with JSON. Below is an example of an index route and its accompanying view that will be used in the explanation. 

![RecipesController Index Method](https://i.imgur.com/JG2JAkt.png)

![Index View](https://i.imgur.com/Cydb6uF.png)

We understand what the response of `format.json` does now. We also understand AJAX get requests. So what am I doing here? First, I create an array out of the current url using `window.location.href.split("/")`. This allows me to grab any individual element that I want (the params). Next, I use `parseInt()` on the urlArray in order to create an integer from the stringed number. The implementation of the `if / else` JavaScript statements are then used upon my urlArray in order to determine if the third index contains the word "liquors" or "users". If it contains "liquors," then the AJAX get request to the url of `/liquors/:id/recipes` is fired off. If not, then the url of `/users/:id/recipes` is snagged. The difference between these two routes is that the first displays the recipes for a given liquor on the liquor show page. The second route will grab all the recipes created by the user with the given params (User 1, User 2, etc). Once the proper route is determined, an `<li>` element is created and filled with the HTML of an `<a>` tag with the proper show route of the recipe, as well as a placeholder for the recipe name. 

All in all, the project seemed to be a smooth success. I learned a lot, and I hope you learned a lot reading this as well! In case you had more questions, or just wanted to reach out to me, feel free to at *catalano.work@gmail.com*. Happy Coding! <3
