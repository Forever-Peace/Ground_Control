---
title: What the fuck is up with Melvin Gordon?
comments: true
---
I wasn't crazy about the pick, but a lot of smart people were. The Chargers themselves liked Gordon enough to trade *up* for him in the *first round*. Was a monster in college, with 12 100-yard games, 6 200-yard games, and one game with over 400 yards. Led the big ten in YPC for two consecutive years, and led the entire NCAA in both yards and touchdowns his senior year *among all positions*. Great build, isn't afraid of contact, supposedly runs well in tight spaces.  
  
But then ~~lol Wisconsin~~ he took a bit under 200 carries in the NFL and just did not look good. The pick is already being heralded as a bust - evidence of how important it is to build a running game from the inside out (i.e. get your O-line together and the run game follows). So what the fuck is up with Melvin Gordon?  
  
I took a spin through our apps to find out, and added a few extra analyses for good measure.  
  
First, let's compare him to the league average distributions. This is our bread and butter.  
  
* * * 
  
![Gordon Run Distribution](/Ground_Control/img/Gordon_v_rbdist.png)  
  
* * * 
  
  
* * * 
  
![Gordon Cumulative Run Distribution](/Ground_Control/img/Gordon_v_rbdistcum.png)  
  
* * * 
  
Right off the bat, we can see some tendencies. Gordon is sort of the king of the 2-yard run. He gets hit early a lot, but has the push to make it a bit past the line of scrimmage a decent amount of the time. But at the same time, he is looking really bad at breaking out middle-distance runs. Essentially, a good proportion of his runs are cut short at 2-3 yards - runs that other folks would generally take 5-10 yards.  
  
This is really apparent in the boxplots we developed in a previous quick hit:  
  
* * * 
  
![Gordon Boxplot](/Ground_Control/img/Gordon_rundencum.png)
  
* * * 
  
He was below average last year in his ability to make it to the 1 yard line, but even starting from that deficit, he was able to gain that extra yard quick frequently, ending significantly above average in yards that went at least 2 yards. This is not typical: usually the guys that go down a lot early do so because they don't have a lot of fight. Gordon appeared to fight hard in those first 2 yards from scrimmage, in order to make up for the deficit of the leaky offensive line. But then, everything crashed, and he ran significantly below average for every distance past that. I took this to mean that he may have developed a habit of churning his feet into the line and falling forward, without ever really breaking out respectable gains. Possibly a survival strategy for dealing with a shit line?  
  
The poor line play didn't just impact Gordon. The rest of his teammates also didn't fare so well this year.  
  
* * * 
  
![Gordon vs Team1](/Ground_Control/img/Gordon_v_team.png)  
  
* * * 
  
  
* * * 
  
![Gordon vs Team2](/Ground_Control/img/Gordon_v_teamcum.png)  
  
* * * 
  
We see exactly the same propensity this year for Chargers running backs to get cut short. They just weren't breaking through to the open field. And we *know* that Woodhead has historically been really effective on the ground - above-average middle-distance running is actually kind of his thing as an elite pass-catching back. Here's his distribution for the past 6 years overall:  
  
* * * 
  
![Woodhead Run Distribution](/Ground_Control/img/ch2_fig22_WOODHEADden.png)  
  
* * * 
  
The fact that not even Woodhead could break through for his typical gains tells me that problem may have been in the offense as a whole, rather than specifically for Melvin Gordon (though Woodhead getting old is also a plausible hypothesis, meaning the lack of long gains could have been coincidental rather than systematic). Better offensive linemen and better playcalling could help Gordon see better gains.  
  
But Gordon isn't free from responsibility by a long shot. In particular, he still went down *way more often* at the line of scrimmage than his teammates this past year. It would be nice to think that defenses were just keying more on the run when Gordon was in the game, but as far as I'm concerned, even that is still mostly his fault - pass-catching was supposed to be one of his strengths, and if defenses are keying on his runs, it means they either aren't convinced by his threat through the air or can just tell when he's getting the ball.  
  
This is backed up by the distribution matching. Gordon doesn't look look like a grinder, much less a pass-catching guy. Hey looks like a JAG.  
  
* * * 
  
![Gordon Matches](/Ground_Control/img/Gordon_matches.png)
  
* * * 
  
Shaun Draughn has almost the exact same distinctive pattern of A) lots of falling over on top of the line of scrimmage, B) making up "lost" ground by falling forward to the 2 more often than is suspected, and C) failing to break middling and long runs. Other top-10 comparables include Trent Richardson and Alfred Blue so far.  
  
Finally, all this should lead us to ask: how much of this shaky performance could have been due to chance? How often does a league-average running back have a season like Gordon's?  
  
The answer is "not very often". Given the number of touches Gordon has, a league-average back does better about 95% of the time:  
  
* * * 
  
![Gordon Resampling](/Ground_Control/img/Gordon_resampling.png)  
  
* * * 
  
The smart money is on "yeah there's probably a problem here".  
  
Just to demonstrate where Gordon currently sits on the pecking order, I ran a head to head simulation of Melvin Gordon vs Trent Richardson, using the number of carries Gordon had during the year. Essentially, we're asking "what are the chances that Trent Richardson would have outperformed Melvin Gordon if given an equivalent season of carries?" (or rather, we're ballparking an estimate to the hypothetical using simulations).  
  
* * * 
  
![Gordon Head2Head](/Ground_Control/img/Gordon_TRich_head2head.png)  
  
* * * 
  
TRich would have been better than Gordon in about a third of those seasons.  
  
Hopefully he can turn it around, but I wouldn't hold my breath. Things are looking pretty grim so far.  
