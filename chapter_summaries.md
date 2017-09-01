---
layout: page
title: Chapter Summaries
permalink: /ch_sum/
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

# Chapter 1: The Run Distribution
[Read chapter 1 here](/Ground_Control/ch1/)
* The average run goes for about 4.2 yards. The average NFL running back has an average YPC of about 3.5.
* The three most common outcomes of a run every year for the past six years have been gains of 1, 2, or 3 yards (usually in the order of 2/3/1).
* The 1-3-5 rule: Over a quarter of rushing attempts are over by 1 yard, about half of rushing attempts are over by 3 yards, and about ¾ of rushing attempts are over by 5 yards.
* The 10 at 10 rule: any run that goes at least 10 yards is among the longest 10% of rushing attempts.
* On the field, the ball is spotted “exactly”, but on the stat sheets, field position (and thus yardage) is rounded “up” towards the end zone to the nearest whole yard (except in some particular circumstances, such as when there is less than a yard to go for a first down, in which case the yardage is rounded down in order to leave 1 yard remaining for the first down instead of 0).
* A rushing attempt can be thought of as taking a sample from a distribution of possible outcomes. Examining the distribution across runs for certain players and circumstances can tell us a lot about the nature of the possible outcomes for that players or circumstances. The distribution of all runs is significantly right-skewed (i.e. has a long right tail indicating that there are just a few runs that go for a very long yardage – the “bill gates” of runs).
* A cumulative density plot shows the proportion of runs that make it to particular yardages.
* There are three phases to a run: the yards that are blocked, the yards that are contested (where most runs are stopped), and the open field. The yards that are blocked are mostly “free” for the running back, who generally uses that time to rapidly approach the contested zone. In contrast, open field running has a special type of momentum: each step past the contested zone increases the expected yards remaining on the run. Running gets easier the further the running back goes.  
  
# Chapter 2: Types of Runners
[Read chapter 2 here](/Ground_Control/ch2/)
* 20% of all RB runs in the NFL over the past six years are attributable to just ten players: Gore, McCoy, Lynch, CJ2K, Peterson, Forte, Foster, Steven Jackson, DeMarco Murray, and Morris.
* Half of all active running backs over this 6-year period accumulated fewer than 60 total attempts. A quarter of all running backs since 2010 never made it past 15 total carries.
* The run distributions reveal different running styles. We’ve identified six “archetypes”: High-volume Grinders, Home Run Hitters, Short-Yardage Bruisers, JAGS, Elite Pass-Catching backs, and Game-Breaking Talents.
* __Grinders__ include Gore, Morris, Ingram, MJD, Blount, and Lacy. Their value lies in maintaining a high usage rate without sacrificing efficiency in any part of the game.
* __Home Run Hitters__ include McCoy, Peterson, Forsett, Reggie Bush, and Christine Michael. Their value lies in tremendous open-field running that can kick-start a scoring drive.
* __Short-Yardage Bruisers__ include John Kuhn, Shonn Greene, Peyton Hillis, Daniel Thomas, and Law Firm. Their value lies in hitting the line hard and falling forward, reliably picking up at least a yard or two before going down.
* __JAGS__ have value mostly as depth. Most running backs on NFL rosters are JAGs or worse.
* __Elite Pass-Catching backs__ include Woodhead, Pierre Thomas, Sproles, Vereen, and Helu. Their value lies in their versatility, their ability to keep defenses honest as a dual threat, and their ability to exploit soft fronts.
* __Game-Breaking Talents__ include DeMarco Murray, Le’Veon Bell, LaDainian Tomlinson, and Jamaal Charles. They are good at all phases of the run even at a high volume.
* Jamaal Charles looks like the greatest running back of the decade.
* Run distributions are not known to be predictive, but Rawls, Karlos Williams, Jerick McKinnon, and David Johnson are looking very promising. 
* 2008 sucked for the Pats.
  
# Chapter 3: Finding Player Comparables through Distribution Matching
[Read chapter 3 here](/Ground_Control/ch3/)
- We can find the “closest” run distributions for different players using an algorithm to find the shortest distance between the curves. We used a few tricks and settled on “Nearest Neighbor Retrieval”.  
- Finding matches from the archetypes we explored last time allowed us to find other players who seem to belong to that archetype. CJ Spiller appeared to be a home run hitter, Jonathan Grimes a pass-catching back, and Fred Jackson looked suspiciously like a game-breaking talent.  
- The algorithm helped identify Matt Forte and Arian Foster (who are extremely closely matched) as an interesting case of elite pass-catchers who still run like Grinders (carrying a high volume when active and producing an output similar to Frank Gore).  
- “Backward matching” entailed the process of using older veterans to find younger players who are running in a similar way. Le'Veon Bell, Giovani Bernard looked a lot like FJax. Jerick McKinnon and David Johnson looked a lot like DeMarco Murray. Kendall Hunter looked like he maybe could have been a McCoy type runner.  
- “Forward matching” entailed the process of running the younger players through the algorithm to see which established players they most resemble. All of the rookie and sophomore running backs are described above, along with some notes.  
