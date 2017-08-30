---
title: Head to Head Competition Simulations
---
![app5](http://i.imgur.com/5hdYvPN.png)

#### Run command:  
{% highlight R %}
library("shiny");
runGitHub("Forever-Peace/GroundControl", subdir = "Chapters/shinyapps/rb_head2head/")
{% endhighlight %}<br/> 
  
This app is the simulator from [chapter 4](/Ground_Control/chapters/ch4/). Pick two players, pick a sample size (i.e. the number of carries you want them to take in their competition), and hit "Run", and it will calculate the proportion of the time (out of 10,000 competitions) that each player will "win" the competition (IE have the most yards / highest yards per carry). It uses actual NFL runs from each player, chosen at random. The plot shows the possible distributions of yards per carry for each player given that sample size (so, for example, if each player only takes 10 carries, maybe even Adrian Peterson can average as low as 1YPC or so every now and then, and lose to Alfred Blue).  
  
The second tab of the app shows you some information about the types of outcomes you can expect from each player, given the number of carries you selected.  
  
![app5_2](http://i.imgur.com/iQLSli5.png)  
  
To get the app, make sure you have R and Rstudio (described [here](/Ground_Control/apps/install_apps/)), then copy-paste the run command into the "console" window of RStudio.  
  
Note: "career carries" only includes carries since 2010 (when my data starts)