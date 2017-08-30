---
layout: page
title: Table of Contents
permalink: /contents/
---
<style>
// Using numbers instead of bullets for listing
#markdown-toc ul {
    list-style: decimal;
}

#markdown-toc {
    border: 1px solid #aaa;
    padding: 1.5em;
    list-style: decimal;
    display: inline-block;
}
</style>

* Table of Contents
{:toc}
  
---
  
# Chapters  
[Chapter 1: The Typical Run](/Ground_Control/ch1/)  
[Chapter 2: Types of Runners](/Ground_Control/ch2/)    
[Chapter 3: Finding Player Comparables through Distribution Matching](/Ground_Control/ch3/)    
[Chapter 4: Embracing the Random](/Ground_Control/ch4/)  
[Chapter 5: Context is Everything](/Ground_Control/ch5/)  
[Chapter 6: Surprisal Me](/GroundControl/chapters/ch6/)  
  
---

# Apps  
(Click title link for description. Enter the runGitHub command into RStudio after library("shiny") to run the app directly.)  
  
[Installation Instructions for Apps](/Ground_Control/apps/install_apps/)  
  
[Player Distribution Plotter:](/Ground_Control/apps/rbdist/)  
{% highlight R %}runGitHub("Forever-Peace/GroundControl", subdir = "Chapters/shinyapps/rb_dist/"){% endhighlight %}<br/>  
  
[Player Comparison Machine:](/Ground_Control/apps/rb_contrast/)  
{% highlight R %}runGitHub("Forever-Peace/GroundControl", subdir = "Chapters/shinyapps/rb_contrast/"){% endhighlight %}<br/>    
  
[Player vs. Teammates:](/Ground_Control/apps/rb_vsteam/)  
{% highlight R %}runGitHub("Forever-Peace/GroundControl", subdir = "Chapters/shinyapps/rb_distvsteam/"){% endhighlight %}<br/>    
  
[Distribution Matching:](/Ground_Control/apps/rb_distmatch/)  
{% highlight R %}runGitHub("Forever-Peace/GroundControl", subdir = "Chapters/shinyapps/rb_distmatch/"){% endhighlight %}<br/>    
  
[Head to Head Competitions:](/Ground_Control/apps/rb_head2head/)  
{% highlight R %}runGitHub("Forever-Peace/GroundControl", subdir = "Chapters/shinyapps/rb_head2head/"){% endhighlight %}<br/>    
  
[Defensive Yards Against:](/Ground_Control/apps/rb_def/)  
{% highlight R %}runGitHub("Forever-Peace/GroundControl", subdir = "Chapters/shinyapps/rb_def/"){% endhighlight %}<br/>    

[Game Score:](/Ground_Control/apps/rb_surp/)  
{% highlight R %}runGitHub("Forever-Peace/GroundControl", subdir = "Chapters/shinyapps/rb_surp/"){% endhighlight %}<br/>    


---

# Quick Hits
[Official NFL rushing attempt brain-teasers](/Ground_Control/quickhits/teasers/)    
[Player Growth from years 1 to 2](/Ground_Control/quickhits/sophgrowth/)  
[How much variability is there between players?](/Ground_Control/quickhits/playervar/)  
A basic taxonomy of run distributions  
[What the fuck is up with Melvin Gordon?](/Ground_Control/quickhits/melvin15/)  
[The ten yard divot](/Ground_Control/quickhits/divot/)  
[It's Miller Time](/Ground_Control/quickhits/millertime/)

---  
  
# Scripts
[Chapter 1 script: The Typical Run](https://github.com/Forever-Peace/GroundControl/tree/master/Chapters/ch1%20num_to_dist/num_to_dist.R)  
[Chapter 2 script: Types of Runners](https://github.com/Forever-Peace/GroundControl/blob/master/Chapters/ch2%20player_dist/player_dist.R)  
[Chapter 3 script: Finding Player Comparables through Distribution Matching](https://github.com/Forever-Peace/GroundControl/blob/master/Chapters/ch3%20dist_match/dist_match.R)  
[Chapter 4 script: Embracing the Random](https://github.com/Forever-Peace/GroundControl/blob/master/Chapters/ch4%20resampling/resampling.R)  
[Chapter 5 script: Context is Everything](https://github.com/Forever-Peace/GroundControl/blob/master/Chapters/ch5-context/context.R)  
[Chapter 6 script: Surprisal Me](https://github.com/Forever-Peace/GroundControl/blob/master/Chapters/ch6-surprisal/gamescore.R)  
[Game Score calculator standalone script](https://github.com/Forever-Peace/GroundControl/blob/master/Chapters/ch6-surprisal/gamescore_calc_only.R)  

