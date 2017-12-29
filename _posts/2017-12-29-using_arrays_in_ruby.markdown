---
layout: post
title:      "Using Arrays in Ruby"
date:       2017-12-29 17:32:52 +0000
permalink:  using_arrays_in_ruby
---


### What you need to know..

To begin, let's define what an array in Ruby is! W3Schools puts it quite easily,
> An array is a special variable, which can hold more than one value at a time.

If you have a list of items (a list of car names, for example), storing the cars in single variables could look like this:
> car_1 = Saab <br><br>
> car_2 = BMW <br><br>
> car_3 = Mercedes

However, what an array allows us to do is group these variables into a single element, defined by an index starting with 0.
> cars = [Saab, BMW, Mercedes] <br><br>
> Saab** is equal to** an index of 0 <br><br>
> BMW **is equal to
is equal to** an index of 1 <br><br>
> Mercedes **is equal to
is equal to** an index of 2

What does an index do? Simple, it allows us to grab a desired item from within our array. For example, 
> cars[0] **returns** Saab

So how do I change a string into an array, you might ask. It is actually quite easy to do when you use the *.split()*
 method. It would look something like this:
>  string = "Hello, world!" <br><br>
>  string.split(",")  ---> I am separating the string at the comma.. <br><br>
>  This **returns** ["Hello", "world!"]<br><br>
>  string[0] == "Hello"<br><br>
>  string[1] == "world!"

Now, in a far more advanced form, arrays can store a *hash* of *key and value pairs*.  This would look something like:

`array = [{name: Parker_Catalano, location: Carmel_IN, website: http://pathtowebdevelopment.com/}]`

This array is storing just a single hash, so that when you call `array[0]` you would get a **return** of 

`{name: Parker_Catalano
   location: Carmel_IN
	 website: http://pathtowebdevelopment.com/
	}`
	
In this example, the *keys* would be **name: , location: , website:** and the *values* are what each key points to. So, you can see how helpful it would be to be able to store multiple hashes of important data in one place, only to be able to easily call it by index! <br><br>
	
A challenging example of storing multiple hashes within a single array would be demonstrated with the following line of code which scrapes Learn.co and its database of students to pull their names, locations, and websites!
	
	`def self.scrape_index_page(index_url)
    index_page = Nokogiri::HTML(open(index_url))
    students = []
    index_page.css("div.roster-cards-container").each do |card|
      card.css(".student-card a").each do |student|
        student_profile_link = "#{student.attr('href')}"
        student_location = student.css('.student-location').text
        student_name = student.css('.student-name').text
        students << {name: student_name, location: student_location, profile_url: student_profile_link}
      end
    end
    students
	end`
	
Here, the names, locations, and profile_links are being pushed into the students array. Take your time looking over that code to understand it all. Remember, the "shovel" method `<<` is used to push data into an array. <br><br>

Happy Coding! <3






