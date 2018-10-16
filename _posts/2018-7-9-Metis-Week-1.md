---
layout: post
title: First week at metis!
author: "Douglas Lee"
categories: journal
tags: [project, pandas, mta]
image: subwaycat.jpg 
visible: 1
---

Photo credit: Ian Westcott, https://www.flickr.com/photos/iandavid/3804456709 

The focus of the first week was the Benson project. It was a group project aiming to expose us to the pandas python package and to real world data by making use of subway turnstile data. For our project, my group decided to use the turnstile data to look for a new location for a potential cat cafe. I felt a bit hesitant as I thought it would be hard to find useful data, but the project actually turned out really well. 

The turnstile data gave us a rude welcome to the world of data cleaning. The turnstile counters are going backwards and even resetting completely with no regularity. Luckily, Joe, one of our Metis instructors, guided us through the initial cleaning process and made this project seem doable.

To supplement the turnstile data, we decided to look for the number of pet stores near a subway station as an indicator for the number of pet lovers, and therefore likely patrons, in the area. I was pleasantly surprised to find a list of inspection data of retail businesses, complete with their locations. The data was also much easier to work with than the turnstile data and I was easily able to filter for businesses with 'pet' in their names. As a side note, "petroleum" and "carpet" turned out to be commonly used in business names. 

Below is our main figure, a scatter plot of a station's daily foot traffic compared with the number of pet stores near a station. 

![pet subway scatter plot]({{ site.github.url }}/assets/img/pet_subway_scatter.png)

Looking closer at our top five stations, it turned out that they actually belong to two neighborhoods, hell's kitchen and NoHo. This suggests that the stations may be sampling overlapping groups of pet stores, but it still shows that there is a high density of pet stores in the area. Two of the currently operating cat cafes are around the SoHo area. Coincidence? Maybe not. 

After our presentation of the Benson project today, our first "week" at metis is now officially complete. Our first week has been a little awkward because July 4th landed right in the middle, so it spilled over to Monday. It was a fortunate coincidence as it gave me extra time to absorb the first week's material. Even with the solutions, it definitely takes time and effort just to emulate and understand the code. 


