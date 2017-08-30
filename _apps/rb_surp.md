---
title: Game Score
---

![Game Surprisal App Pic](/GroundControl/images/rb_surp_1.png) 

#### Run command:  
{% highlight R %}
library("shiny");
runGitHub("Forever-Peace/GroundControl", subdir = "Chapters/shinyapps/rb_surp/")
{% endhighlight %}<br/> 
  
This app is the Game Score navigator from [chapter 6](/Ground_Control/ch6/). Pick a player, and the plot shows the both the carries that player took in each game since 2010 (along the x-axis) and the quality of the game, measured in bits (where a 1 bit increase in Game Surprisal corresponds with a game that was twice as improbable given league-average running). All games from all players are shown in gray for comparison.
  
The second tab of the app shows Game Score, which is the "marginal Game Surprisal" (or the difference between the red dots and the blue line, aka the difference from average Game Surprisal given that many carries).
  
![app5_2](/GroundControl/images/rb_surp_2.png)  
  
To get the app, make sure you have R and Rstudio (described [here](/Ground_Control/apps/install_apps/)), then copy-paste the run command into the "console" window of RStudio.  
  
Note: "career carries" only includes carries since 2010 (when my data starts)
