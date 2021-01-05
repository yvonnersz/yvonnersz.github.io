---
layout: post
title:      "CLI Data Gem Portfolio Project"
date:       2020-04-25 07:43:20 -0400
permalink:  cli_data_gem_portfolio_project
---


First portfolio project down! Coming from someone who has no background in coding, when I first started the CLI project, I had a mini panic attack thinking that I did not have the knowledge to be able to complete the project. I went through many frustrating moments of my code not working the way I want it to, but today is the sixth day of coding my project and I can finally say that my code works! I find that by coding a little bit every day made the daunting task more bearable. FlatIron also have useful references and resources that could be used to look back to when you are stuck.

## Project Requirements
1. Provide a CLI
2. Your CLI application must provide access to data from a web page.
3. The data provided must go at least one level deep. A "level" is where a user can make a choice and then get detailed information about their choice.


## Step 1: Planning
Below is the app flow diagram that I created which I eventually had to scrap due to having an incompatible website.

https://drive.google.com/file/d/1CNTyJcqgZwcJBM5fOqBX4FDjf2oHimSz/view?usp=sharing

I originally wanted to base my project on activities to do in Japan since I was supposed to be travelling to the country this year until the whole COVID-19 epidemic occurred. I thought the planning step would be the easiest but it actually took more time than I anticipated. Unfortunately, most of the websites that I took a particular liking to contained Javascript, so they could not be used. 

I eventually stumbled upon this webite:

https://www.japan-guide.com/e/e2292.html 

The website provided above did not contain any Javascript and the information provided through the website was fairly consistent (or so I thought). I also came to the conclusion that my original idea of wanting to base it on activities in Japan would be extremely time-consuming, so I had to go through many rounds of having to narrow my focus on what I wanted my project to do. 

I eventually settled on onsens (hot springs). Based in the Kanto region, what onsens are popular based on the cities that the user is interested in? The user would also be able to pick the onsens that they are interested in and the program would return the hours and a small description.


## Step 2: Project Skeleton
Starting the project from scratch was another obstacle that had my head scratching. I panicked when I was building my code and binding.pry was not functioning as intended. Fortunately, FlatIron has many resources and after watching a few videos, I was able to build the project skeleton!

The most important thing was to edit the .gemspec file and create a file in ./bin/ that would launch the program. After building the skeleton, it just comes down to coding.


## Step 3: Coding
After watching a couple videos, I knew that I would need a JapanInfo, Scraper, and a CLI class. When I first started coding the project, I was focused on trying to make my code as abstract as possible; however, I found that by doing this, I was slowing down and not typing any code. I then shifted my focus on just trying to make the code work, despite the code being long and ugly. As soon as I got my code to work, I worked on refactoring it so that I can have the code as concise as possible.

When I got my code to work, I had over 1000+ lines of code in my japan-info file. I was able to cut that down to just 200 lines! I was truly impressed by how the refactored code could give me the same results as a code that is over 1000+ lines long!

After refactoring my code, I compared my code to the worlds-best-restaurants gem. I found that my code required manual work of copying and pasting the urls that each object took me to. Here's the snippet of the code I had before that was in my Scraper class: 

```
module JapanInfo
  class Scraper

    def self.onsen_page
      Nokogiri::HTML(open("https://www.japan-guide.com/e/e2292.html"))
    end

    def self.kusatsu_page
      Nokogiri::HTML(open("https://www.japan-guide.com/e/e7402.html"))
    end

    def self.manza_page
      Nokogiri::HTML(open("https://www.japan-guide.com/e/e7495.html"))
    end

    def self.hakone_page
      Nokogiri::HTML(open("https://www.japan-guide.com/e/e5209.html"))
    end

    def self.minakami_page
      Nokogiri::HTML(open("https://www.japan-guide.com/e/e7463.html"))
    end

    def self.nasu_page
      Nokogiri::HTML(open("https://www.japan-guide.com/e/e3842.html"))
    end

    def self.nikko_page
      Nokogiri::HTML(open("https://www.japan-guide.com/e/e3807.html"))
    end

    def self.ikaho_page
      Nokogiri::HTML(open("https://www.japan-guide.com/e/e7477.html"))
    end

    def self.kinugawa_page
      Nokogiri::HTML(open("https://www.japan-guide.com/e/e3877.html"))
    end

    def self.shiobara_page
      Nokogiri::HTML(open("https://www.japan-guide.com/e/e3843.html"))
    end

    def self.shima_page
      Nokogiri::HTML(open("https://www.japan-guide.com/e/e7435.html"))
    end

  end
end
```

Ugly, right?  After intently reviewing the worlds-best-restaurants gem, I realized that I could condense my code even further by having the code automatically instantiate the cities by finding the "href" attribute. I thought this was genius! Here's a snippet of the code that does EXACTLY the same thing, but is more concise and abstract.

```
def self.new_from_index_page(city)
	self.new(
		city.css(".spot_list__spot__name").text,
		"https://www.japan-guide.com#{city.css(".spot_list__spot__main_info a").attribute("href").value}",
		city.css("div.spot_list__spot__desc").text
		)
end

def initialize(name=nil, url=nil, description=nil)
	@name = name
	@url = url
	@description = description
	@@all << self
end
```


## Step 4: Debugging
The most exciting(?) part: debugging.

As soon as I finished refactoring my code, I worked on debugging it. Thinking back, I probably should have worked on debugging it AFTER I got my code working to avoid wasted time. Most of the cities that the user was interested in aligned with the information on the website... until the last two cities! I had to find out what was making my data inconsistent. After fumbling around for a bit, I realized that not every section on the webpage had hours listed, as seen in the images below:

![https://ibb.co/MNj77rR](https://ibb.co/MNj77rR)
![https://ibb.co/qDbgCYx](https://ibb.co/qDbgCYx)

Certain sections did not have hours posted which ruined the index consistency. To make the code consistent to the index, I had to rewrite that particular method so that the information matched up with the website. After a couple hours, I  was able to fix the flaw in my code and finally got every spot to match up with the hours. Here was the finished code that wrapped everything up:

```
doc.css(".spot_list__spot__main_info").collect do |bio|
		if bio.text.include?("Open") || bio.text.include?("Hours:")
			schedule = bio.css(".spot_meta__text_wrap")
			split_schedule = schedule.text.gsub(/(?<=[a-z])(?=[A-Z])/, "\n")
			number_split_schedule = split_schedule.gsub(/(?<=[0-9])(?=[A-Z])/, "\n")
			@schedule << paranthesis_split = number_split_schedule.gsub(/(?<=[)])(?=[A-Z])/, "\n")
		else
			no_schedule = "We could not find any information on shop hours."
			@schedule << no_schedule
		end
	end
```

Looks daunting but that is because this snippet of code also fixes some spacing issues. This was done so that it would be easier to read the shop hours and description.


## Finished Project
If anyone is interested, here is the link to the final project: https://github.com/yvonnersz/japan-info.

