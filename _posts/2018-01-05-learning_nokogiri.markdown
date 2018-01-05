---
layout: post
title:      "Learning Nokogiri"
date:       2018-01-05 20:06:46 +0000
permalink:  learning_nokogiri
---

### The Art of Scraping

What is Nokogiri? That's a pretty solid question to start off with, I'd assume. So here, let's give it a little detailing before we "hit the ball running." According to Wikipedia,

> Nokogiri is an open source software library to parse HTML and XML in Ruby. It is one of the most downloaded Ruby gems: downloaded over 100 million times
> 

Okay. Parsing web files... What does that mean? In layman's terms, you are essentially reading a web page and picking out bits of information which you would like to store elsewhere. Pretty cool! For example, I made a CLI Data Gem project in which I parsed out bits of information regarding the best values for different wine brands from sources such as WineMag and BusinessInsider. I'll show you a snippet of the code and then go line-by-line for a little bit of a walkthrough. Here we go!

`
    
    def deals
        # HTML DOCUMENT
        @doc = Nokogiri::HTML(open("http://www.businessinsider.com/top-pinot-grigios-under-15-2012-9", 'User-Agent' => 'chrome'))
        
        # PARSING THE DOCUMENT TO GET TO THE DEALS
        strings = @doc.search("a strong").text
        wines = strings.split("$")
        
        # DEALS
        puts "BEST VALUES!".green
        puts "1. #{wines[0]}$15, 89pts"
        puts "2. #{wines[1].gsub(/15/, '')}$15, 89pts"
        puts "3. #{wines[2].gsub(/15/, '')}$15, 87pts"
        puts "4. #{wines[3].gsub(/15/, '')}$12, 87pts"
        puts "5. #{wines[4].gsub(/^12/, '')}$14, 87pts"
        puts ""
        
    end`

#### Step 1:

`@doc = Nokogiri::HTML`

This line is telling my code that the file I am about to parse with Nokogiri is an HTML file. This will allow me to use such methods as `.search` and `.css`.

By calling the `open` method, I activate my `open-uri` requirement to access the online web document. Notice that I use the `'User-Agent' => 'chrome'`? This eliminates me from running into a 403 Forbidden Error (which means that I am forbidden from entering a specific site). The User-Agent is telling my program where the data is coming from and how to properly access it.  Try to follow allong in this example of a User-Agent:

![](https://i.imgur.com/O8wK4aT.png)

Here, the User-Agent is defined by a wider spectrum in order to more easily parse any file you pull from! Fun <3


####  Step 2:

Parsing the Document to Get to The Deals

Notice that I used `@doc.search`? This will pull in the CSS values within the document and search for any matches. The `.text` parameter will return the actual text format which is encapsulated within the CSS depicted. The big difference between `.search` and `.css` is the actual **return value** - `.search` will return a *string* whereas `.css` will return an *array*. After getting my list of strings, I call the `.split` method to break them into an array.

#### Step 3:

Finally, I simply call on the array index to choose my specific deal which I would like to present to the user. Easy!

`wines[array_index]`

#### Resources:
What I have given is just the bare-bones basics to using Nokogiri. Here are some super helpful links for you to enjoy!

[Github, Nokogiri Installation ](https://github.com/sparklemotion/nokogiri)
<br><br>
[Nokogiri Tutorials](http://www.nokogiri.org/)
<br><br>
[Searching an XTML or HTML Document](http://www.nokogiri.org/tutorials/searching_a_xml_html_document.html)



