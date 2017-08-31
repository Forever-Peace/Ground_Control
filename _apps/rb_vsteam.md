---
title: Player vs. Teammates
---
![app3](/Ground_Control/img/rb_distvsteam_guide.bmp)

#### Run command:  
{% highlight R %}
library("shiny");
runGitHub("Forever-Peace/GroundControl", subdir = "Chapters/shinyapps/rb_distvsteam/")
{% endhighlight %}  
  
I'm pretty excited about this app. Essentially, it lets you compare a selected player to all of the other running backs on his team that took carries in the same games.  
  
This is a little different from simply "comparing a player to all of his teammates", because it draws data on a week-by-week basis. So, for example, let's say Marshawn Lynch had to sit during a week that Rawls had a cakewalk opponent, or Randle got to run with Romo as a QB while McFadden had most of his carries under Matt Cassel. This approach should remove those potential sources of bias. It only compares like versus like: drawing from only the competing carries where both the player and his teammates had the same opponent, and probably the same QB and same offensive line composition.  
  
It also lets us include players who jumped teams. Terrance West is only compared against TEN players for his first two games (regardless of what those TEN players did afterwards against different opponents), then is compared against BAL players for the rest of his games (regardless of what those BAL players did at the start of the season).  
  
In essence, it lets us compare a player to his teammates while approximately controlling for game-level factors like opponent, offensive line, weather, QB etc.  
  
This game-by-game approach also lets us introduce a new statistic: "Active Run Share". Usage rates, or the proportion of a team's carries a guy gets during a _season_, can be easily biased by injuries and trades. "Active Run Share" calculates that proportion of carries a guy gets when he's active (or has at least 1 carry, rather) at a game-by-game level.  
  
Hope you enjoy! To get the app, make sure you have R and Rstudio (described [here](/Ground_Control/apps/install_apps/)), then copy-paste the run command into the "console" window of RStudio. 
  
Note: "career carries" only includes carries since 2010 (when my data starts).  
