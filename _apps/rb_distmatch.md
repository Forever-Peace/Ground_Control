---
title: Player Distribution Matching
---
![app4](http://i.imgur.com/5O4PNAs.png)

#### Run command:  
{% highlight R %}
library("shiny");  
runGitHub("Forever-Peace/GroundControl", subdir = "Chapters/shinyapps/rb_distmatch/")
{% endhighlight %}<br/>  
  
This app allows you to do the same sort of distribution matching that we utilized in [chapter 3](/Ground_Control/chapters/ch3/). Pick a player, and you will be given A) an ordered list of matches (best at the top to worst on the bottom) that you can choose from to plot against the player you ran through the matcher, and B) a text list of the top 10 matches. If you felt that 50 carries was too small of a sample size for matching, you can select higher cutoffs at the top right. This will remove any "matches" below that limit.  
  
This is a very naive player matcher - it ONLY finds similar cumulative run distributions. It doesn't factor in anything else. It also doesn't rescale the different distance rates, so the algorithm is most influences by the distances with the most player-by-player variation (i.e. 3-5 yards).  
  
To get the app, make sure you have R and Rstudio (described [here](/Ground_Control/apps/install_apps/)), then copy-paste the run command into the "console" window of RStudio.  
  
Note: "career carries" only includes carries since 2010 (when my data starts)
