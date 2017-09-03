---
title: What's the point? Machine-learning our way to EPA.
---

<i>Originally posted 8/28/2017</i>  

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

# A Tale of Two Touchdowns
__Run #1__: It's the start of the third quarter, and the Titans are buried back at their own nine yard line facing a daunting 3rd and 10. The Houston defense lines up in an aggressive single-deep man defense, and five rushers come crashing down at the snap in order to disrupt the expected pass. Chris Johnson takes the handoff out of shotgun formation, back foot striding off his own four yard line, as he sprints up the middle behind the pulling left guard. One hard cut behind the line, another hard cut behind his blocker into the secondary, and he's gone: 91-yard touchdown. LINK TO VIDEO CLIP HERE.  
  
__Run #2__: Early in the first quarter, the Rams and the Bears line up for a goal-line stand. It's a bad start for Chicago: the misfiring defense has already given up a touchdown on the first drive of the game, and their sole offensive possession was a Matt Forte fumble on their own 9-yard line. After giving up a Defensive Pass Interference penalty in the end zone, it's now first and goal from the 1 yard line. The Rams line up with no recievers. Zac Stacy takes the handoff, follows his fullback to the strong side, and falls into the end zone for the score. LINK TO VIDEO CLIP HERE.  
  
How much is each run worth?  
  
Naturally, each touchdown results in the same number of points added to the scoreboard. The NFL isn't handing out style points quite yet. So while we have an intuition that the Chris Johnson run might have been more difficult or more important, it isn't reflected in the box score.  
  
But there is one essential difference: even if Zac Stacy had missed the end zone the first time around, the Rams were likely to score anyways. They had 3 more opportunities to put points on the board, only had to travel a yard, had plenty of time on the clock, and were well within easy field goal range as a last resort. Zac Stacy was simply the guy taking care of the nearly-inevitable (though there are always exceptions - just ask a Seahawks fan). The Titans, on the hand, would have almost definitely had to punt if they couldn't convert the third and 10 in the tricky field position that makes throwing risky. And even then, on a 10-yard gain, the Titans would have been right back to square one on the drive, as if they had just come out after a touchback. The prospects of points were grim: most teams, given this situation, would be in damage control mode. Chris Johnson took that opportunity and made something out of nothing. His run was more valuable, because the 7 points came in the context of a grim outlook for the drive. What mattered here was the _difference_ between the expected value of the drive before and after the play.  
  
In short, the value of a run can be measured in the amount it adds (or subtracts) from an offense's outlook. To do this, we just need a reasonable way to estimate what the prospects of a drive are given a state of play. First and 10 from the 1 yard line against a bad defense has pretty good prospects to score some points. Third and 10 from your own 9, not so much. Take the expected points at the start of the play compared to the expected points (or actual points, in this case) after the play, and you get __Expected Points Added__ by the play.

# Measuring Up to Expectations
We aren't the first to explore expected points, of course. Folks have been developing expected points models for decades - many point to [The Hidden Game of Football](https://www.amazon.com/gp/product/0446390917) as one of the first to popularize the approach, and [Brian Burke](https://twitter.com/bburkeespn) picked up the torch in the modern era with [his own spin on EPA](http://www.advancedfootballanalytics.com/index.php/home/stats/stats-explained/expected-points-and-epa-explained). Analytics sites like [Numberfire](http://www.numberfire.com/info/glossary) and [Drive-By Football](http://www.drivebyfootball.com/2011/06/our-expected-points-model.html) took similar approaches, [Harvard joined the party](http://harvardsportsanalysis.org/2015/10/its-a-party/), and [ESPN even jumped on board](http://www.espn.com/nfl/story/_/id/8379024/nfl-explaining-expected-points-metric), hiring Brian Burke and making EPA a mainsty of it's statistical offerrings (see [this](http://www.espn.com/nfl/qbr/_/sort/cwepaTotal), for example). 
  
The approach all took is pretty simple: dice the state of play into pieces, and take the average outcome. What's the average outcome of a First and 10 from your own 20? How about a Third and 5 from midfield? Second and 2 from the 5-yard line? Burke and others also smoothed over some of these situations features, such that epected outcomes from OPP 30 also informed expected outcomes from OPP 25 etc. Then, you can assume that future drive outcomes will be similar to past drive outcomes given similar circumstances, and a "best guess" for what the expected value should be is the mean of the past outcomes.  
  
This approach is tremendously poweful, and can yield lots of very interesting information. A group of researchers from Carnegie Mellon recently put together a [great example of what you can do using this approach](http://www.stat.cmu.edu/~ryurko/pdf/greatlakes_2017.pdf), complete with open-source R package and openly available data.  
  
This approach to calculating EPA has a lot of benefits. It's intuitive, it's simple, it doesn't require many assumptions, and it's reasonably accurate. It's good enough for ESPN to put all over the place!  
  
However, it does have some well-known issues. [Josh Hermsmeyer of Rotoviz](https://twitter.com/friscojosh) put together [a good illustration of some of the problems](http://jhermsmeyer.com/why-expected-points-are-broken) last October in an article titled "Why Expected Points and EPA are kind of broken". To summarize his arguments: 1) the data is too sparse for many situations (i.e. some circumstances just haven't enough for us to know what the mean should be), 2) the assumptions you DO make can wildly impact the resulting EPA value, 3) the metric is unstable (relying a lot on the particulars of past data), and 4) the predictions are very uncertain. I encourage you to read the breakdown through the link.  
  
I got to thinking whether these problems might be tractable. Is it possible to make a better EPA?  
  
Clearly, I thought the answer to this question was "yes". But improvements don't come for free. From the get-go, I was very clear what I was willing to sacrifice and what I wasn't. Specifically, my goal here is to maximize the predictive capability of an expected points model. To go truly overboard making the most accurate one I can. What I'm willing to sacrifice is the ability to interpret how the hell the model actually works. For the first time on this website, we are going to leave aside the world of explanation, and enter the world of prediction. Let's do some machine learning.  
  
# Prediction and Explanation are different
One of my favorite papers on statistics has barely any stats in it at all. Rather, it's a paper about having clarity in what you intend to accomplish with all your number-crunching. It's called, simply, ["To Explain or To Predict?"](https://www.stat.berkeley.edu/~aldous/157/Papers/shmueli.pdf), by Galit Shmueli.  
  
In Shmueli's telling, the goals of the researchers should always guide the math. Often, a researcher is interested in elucidating or articulating the nature of a particular type of relationship between things. Say, between the temperature high and ice-cream sales. We have a lot of sophisticated ways of operationalizing these types of relationships, including a causal way (the landmark work here is by [Judea Pearl](https://www.amazon.com/Causality-Reasoning-Inference-Judea-Pearl/dp/0521773628/) and colleagues). And we have a host of methods with which to test these hypotheses against data to see how they hold up. What Shmueli emphasizes above and beyond any particular approach or another is an approach to building statistical models that serve the goal of explanation well. Explanatory models should often be theoretically coherent and numerically interpretable. It is perfectly acceptable for them to be retrospective, investing how something worked with depth and precision. We often use as much data as we can get our hands on. This should all sound familiar: it is exactly the approach we have taken to every other chapter on Ground Control.  
  
A good predictive model demands an entirely different approach. In predictive modeling, we almost always divide the available data into different parts, so we can estimate (and maximize) predictive capabilities of our models directly. If all we care about is maximizing the quality of predictions, the models don't need to be interpretable. The relationships don't need to be intuitive, or even known to the researcher - we can maximize predictive utility by any arcane technique we have in our toolbox. "Controls" and "nuisance factors" no longer carry much meaning: all of our data becomes useful only insofar as it helps us make better predictions, and there, we cast a wide net and aggressively pursue whatever artificial engineered features yield the best predictions. Today, we are going to do all of these things.  

# Predicting Expected Points with Machine Learning  
In the field of Expected Points models, I guessed that most of the limitations were a consequence of an implicit commitment to sensability. We wanted the model to make sense: good field position is better than bad field position, first down is generally better than second down, 1 yard to go is generally better than 10 yards to go. And the relationship between the predictors (down, distance, field position) and outcomes (expected points) was transparent - it was basically just an average. I speculated that we might be able to improve our predictions if we allow for higher-order interactions, disjoint and discrete effects, opaque (and more complicated) relationships between predictors and outcomes, a greater range of situational factors, and an optimization procedure that explicitly maximizes predictive ability on novel data.  
  
Here's what I did.  
  
## Training versus Testing  
As mentioned above, it is common in machine learning to set aside some of your data in order to explicitly test how good your predictions are on novel data (where predictive accuracy is the thing we intend to maximize). Here, we set aside 15% of our data for testing, chosen at random from our database of plays. The remaining 85% will be used to actually fit and optimize our machine-learning models in order to make good predictions in the first place.  
  
When developing a model, it is also common to simulate additional rounds of training and testing within your training data set through a process called "cross validation". Say I'm building a neural network, and need to choose the right number of neurons in the right configuration. I can split up my training set into additional training and testing sub-sets and see how accurate, on average, various choices are at predicting the hold-out values. Then, once I settle on a good-looking model, I can train it on the entirety of my training data, and generate final predictions against the testing data to see how good it did.  
  
## Feature Engineering
Using our trusty [nfldb](https://github.com/BurntSushi/nfldb/wiki) database, I scraped information about every single game, drive, play, and player since 2009. Right off the bat, this gives us a number of essential pieces of information about each play: __down, distance, field position, and the ultimate result of the drive.__ This will be the heart of the Expected Points model, as previous models have done. We also grab __day of the week__, because why not. Maybe there's something to the "sloppy Thursday offenses" theory. 
  
But a key aspect of machine learning is engineering measures that will help make your predictions more accurate. Things that contain pertinent information relevant to the predictions that can't be found elsewhere in the model. I put together a few things that seemed plausible to me.  
  
### Clock Time  
The nfldb database comes with a clock time, listing the quarter and the timeleft in that quarter. I split __quarter__ off into it's own variable, and converted the clock time into seconds. Then, I used these two pieces of information to construce "seconds left in the half" and "seconds left in the game". These are the two points in the game where the clock really, really matters, because it is possible to flat run out of time. It seemed plausible to me that your outlook after a touchback is pretty different when there's only 50 seconds on the clock. __"Game Time Left"__ could plausibly be sensitive to both halftime and the game end in the right model, while __"Time Left In Half"__ would need to interact with __"1st / 2nd Half"__ in order to serve a similar utility.  
  
### Homefield advantage  
Plays are plausibly harder to call on offense while playing away games, considering the crowd noise. This may or may not interact with all sorts of things in subtle and not-so-subtle ways. We modify the existing data to code wether or not the offense on any given play is __playing at home__.  
  
### Score
The databse includes the score at the time of any particular play. I recode this first into a __point differential__ (how much the possessing team is either up or down), and then into a __"touchdown differential"__ (how many scores it would take to close the difference). Both seemed like they could plausbily hold predictive power. Running the ball is easier when you're losing by a lot, late in the game (see [Chapter 5](/GroundControl/chapters/ch5/)).  
  
### Plays, Sets, and First Downs
Do defenses get tired when they are on the field for a long drive? Is yielding a long string of first downs demoralizing? Do playcalling tendencies get weird when a drive seems to stretch on and on? Maybe! Who knows? But it's plausible enough to include for now. I write a function that determines whether any particular field position resulted in at least one more first down, coded as a binary yes/no outcome called __"first down gained"__. Each new set of downs I called a __"set"__, and I counted the sets in each drive, labeling which set each play belonged to. Finally, I counted and labeled all plays in each drive, calling it the __"play number"__. 
  
### Conversion Probability  
Many machine-learning approaches can handle higher-order interactions between predictors (i.e. the nuances of how down, distance, and field position combine to impact expected outcome of a drive) fairly well. However, it can occasionally be helpful to isolate a particular intermediary between these raw predictors and the outcome, particularly when the intermediary may contain slightly different information and/or shape of relationship to the outcome to the raw predictors alone.  
  
One prime example is the expected probability of converting a first down. In order to score, an offense needs to keep the drive going. We know already that field position has a big impact a team's ability to score, where a long way to go diminishes the prospects of the drive. But it's also plausible that there may be some critical stretch of the field (perhaps within your own 10) where it is unusually difficult to even convert a first down. Perhaps defenses become more aggressive in their pursuit of a safety, and an interception is incredibly likely to become a pick-six, so teams are less inclined to throw the ball. 7-step dropbacks might become too dangerous to utilize, and screen passes could easily turn into a safety, so they are avoided. In this area, field position all of a sudden changes what it is sensitive to: it is measuring the impact on the ability to keep a drive going as much as it is measuring the long distance required to reach the end zone.  
  
Within the opponent's 15 might be an even more interesting region, because the impact on first down conversion rates could plausibly diverge from the likelihood of scoring a touchdown. As the field compresses and "levels" passing concepts become harder to implement, teams become less efficient at moving the ball as they near the endzone, despite the fact that nearing the endzone should also increase their expected points (because having less distance to go is better). The field position measure "wants" to provide information about two contrasting effects in opposite directions, and left alone as a raw measure, it might just simply "try" to split the difference between them. Factor in that down, distance, score, and clock time etc all might impact the ability to convert a first down in slightly different ways than the ability to score a touchdown (e.g. teams down late might have an easier time running for a first down but a harder time passing for big gains against prevent defenses), and you can see the potential problem.  
  
What we can do here is engineer a measure of the expected probability of converting a first down given the game situation. Then, we can enter that probability alongside the other predictors in our machine-learning models. First down probability will account for the chances of keeping the drive alive, while field position etc. is left to account for the other ways above and beyond conversion rate that the yardline could impact the expected points (e.g. by being close or far from the end zone or field goal range).  
  
Since we're already familiar with it from [Chapter 5](/Ground_Control/ch5/), we'll use a Generalized Additive Model to estimate the probability of converting a first down. You can think of this as drawing a series of curves through our predictors to represent the different effects, then adding them all up. The effect of yards to go is estimated for each down, the effect of field position is similarly estimated for each down, the effect of time left in the game is estimated seperately for winning and losing offenses, and we adjust for day of the week (where Thursday is expected to be bad), homefield advantage, week in the season, and the quality of the defense. We also specify that the error is binomially distributed, that our outcome should be in log-odds space, and that we should only use our training data set.
  
Things look about as we expected. Converting a first down is harder the further away the line to gain is:
  
* * *   
  
![2nd down and yards to go](/img/EP_CP_yards_to_go_2.png)  
  
* * *   

And as we expected, all else held equal, converting a first down is easiest in midfield, and hardest close to either your own endzone (where playcalling is limited and defensive looks are different) or close to the opposing endzone (where the field compresses):
  
* * *   
  
![conversion rate effect of yards til goal](/img/EP_CP_yards_til_goal_2.png)  
  
* * *   
 
Finally, also as expected, losing teams gradually have an easier and easier time converting first downs (the end of the game is on the left):
  
* * *   
  
![losing teams timeleft](/img/EP_CP_gameleft_losing.png)  
  
* * *   
 
While teams that are ahead late in the game show a massive decrease in their first-down conversion rate (initially because they want to run the clock out, and eventually because they will choose to take a knee and kill the game).
  
* * *   
  
![winning teams timeleft](/img/EP_CP_gameleft_winning.png)  
  
* * *   
 
Add together all the effects, and we get some estimates of whether or not a first down is likely to be gained given the current state of play. The testing set indicates that they're pretty good. Here's some metrics of our "set success" model using our testing set:  
  
<style>
table, th, td {
    border: 1px solid black;
    border-collapse: collapse;
}
th, td {
    padding: 4px;
}
</style>  
| Accuracy | 0.6365 |
| Cohen's Kappa | 0.2598 |
| Pos Pred Value | 0.6446 |
| Neg Pred Value | 0.6319 |  
| Sensitivity | 0.4975 |
| Specificity | 0.7587 |
  
    
<br/> 
  
It's a little conservative in calling a first down, but is otherwise showing very little bias and decent predictive validity, considering the irreducible randomness inherent to football outcomes.  
  
We generate predicted probabilities of making a first down given the state of play, add it to our dataset, and move on to the machine learning.  
  
## Modeling Expected Points
Now that we have a plan, some data, plenty of cool features to work with, and training set, we're ready to move on to some machine learning. There are a million different ways to take a set of predictors and use them to generate predictions, each with their own strengths and weaknesses. Because a lot of plays tend to happen on first down and/or close to your own 20 yard line, I could probably do pretty well building a model that handles this situation extremely accurately. But I actually want my predictions to be pretty good over the wide range of possible states of play. Given any random situation, I want my model to be able to put together a pretty good guess. In order to help do this, we can combine the predictions of different models, each with different strengths, into a single aggregate prediction, focusing on covering a wide range of possible circumstances well. This approach is called __ensembling__, because we make an ensemble of models (rather than just a single model) and combine their voices into a single chorus. You can read more about ensemble methods [here](https://www.toptal.com/machine-learning/ensemble-methods-machine-learning).  
  
As such, we will be running a number of different models, each with their own unique considerations. I'll run through the technical specifics of those different models below. Unlike the rest of this website, I won't be explaining every term I use, but the first paragraph of each model will give a plain-english summary of what the model is doing, what it's strengths are, and how it works to generate predictions. If you are not particularly well-versed in machine learning, skimming the first paragraph of each section below will help you get a feel for how we are approaching things. But all the nitty-gritty details are there for the folks that are interested as well!  
  
We'll begin with the familiar generalized additive models, but as we get deeper into other machine learning approaches, we'll be shifting from R back into python, so we can make use of the phenomenal [scikit-learn library](http://scikit-learn.org/stable/). Everything but the GAMs were done in python.
  
### Generalized Additive Model  
We first introduced GAMS in [Chapter 5](/Ground_Control/ch5/) to construct a situation model of how the state of play impacts rushing yardage. Again, you think of a GAM as the process of drawing a series of curves to reflect how the different predictors relate to the outcome (in this case, points). To generate a prediction, we just find the location on the different curves and add them all up (thus, the "additive" part of the "generalized additive model"). You can read more [here](http://multithreaded.stitchfix.com/blog/2015/07/30/gam/).  
  
__Strengths__: smooth, complex non-linear relationships between predictors and outcomes.  
__Weaknesses__: discontinuous effects, high-order interactions and non-additive effects. 
  
I like GAMS because they are very useful for both prediction _and_ explanation. If I want to explain a relationship, I might not get a number, but I do get a picture (of the relationship curve), and I can show you the picture as a way of explaining the relationship. Though our intention here is prediction (and GAMs are more that capable of generating great predictions), many of these pictures are still very interpretable. For example, it still makes a lot of sense that the expected points on 4th down is extremely sensitive to field goal range: 
  
* * *   
![winning teams timeleft](/img/EP_yards_til_goal_4.png)  
* * *   
 
After optimizing a few of the parameters (e.g. K for each smooth term), we arrive at a __correlation between predicted score and actual score of 0.4654 in our test set.__ That is, again, not terrible: given a state of play at any given time, we can explain about a quarter of the variance in likely outcomes. More importantly, while the prediction interval still has plenty of (likely irreducible) noise, the confidence interval of the model features is extremely stable and generally quite tight.  
  
The down makes a big difference in expected points, and we want our models to be accurate regardless of down, so we can interrogate how well the model does with each potential down by calculating the correlation coefficient separetely for each down:  
  
<style>
table, th, td {
    border: 1px solid black;
    border-collapse: collapse;
}
th, td {
    padding: 4px;
}
</style>  
| 1st down r | 0.4406 |
| 2nd down r | 0.4425 |
| 3rd down r | 0.4762 |
| 4th down r | 0.5782 |
| Overall r | 0.4654 |
  
<br/> 

Accuracy gets slightly better as 4th down rolls around (as expected - these will often end in either a punt or a made field goal), but it doesn't seem "bad" anywhere.  
  
### Multinomial Logistic Regression  
Solving for expected points is actually a bit of an odd problem, because while the scores have real values (3 for a field goal, about 7 for a touchdown), they can only take these specific integer values. Above, with the GAM, we simply tried to predict the values directly. But another approach is to try to predict the category of the outcome with some probability (e.g. "35% chance of a touchdown, 10% chance of a field goal" etc.), and only afterwards multiply these probabilities by the values of those outcomes. This handles the distribution of the data much more cleanly, but requires a classifier that gives really good probability estimates (which is somewhat uncommon). Luckily, logistic regression fits the bill. It's another of the simpler ones. We build a regression model (where our predictors relate to the outcome according to some fixed, numerical relationship), and fit it in log-odds space (i.e. trying to predict the odds of this or that category). You can read more about it logistic regression [here](https://dataaspirant.com/2017/03/02/how-logistic-regression-model-works/).  
  
__Strengths__: linear main effects and interactions, probabilistic classification, actually handles the structure of the outcome appropriately.  
__Weaknesses__: nonlinear effects and higher-order interactions, discontinuous effects, does not actually "consider" the real values of our outcomes (e.g. where a touchdown is worth 2.33 times a field goal).  
  
All continuous predictors were z-transformed. To account for interactions, we generate an interaction term for every possible combination of 2 predictors (this is very simple with the "PolynomialFeatures" function in sklearn). The regression model was fit by minimizing the true multinomial loss over all three outcomes by the latest and greatest form of stochastic average gradient descent (called "[saga](https://arxiv.org/abs/1407.0202)"). Regularization strength ([a penalty applied to coefficients to prevent overfitting](https://en.wikipedia.org/wiki/Regularization_%28mathematics%29#Other_uses_of_regularization_in_statistics_and_machine_learning)) was optimized using a [grid search](https://en.wikipedia.org/wiki/Hyperparameter_(machine_learning)#Grid_search) of 100 possible values across 9 orders of magnitude, tested using 6-fold cross-validation.  
  
Since this is also a classifier, we can check the classification accuracy:  

<style>
table, th, td {
    border: 1px solid black;
    border-collapse: collapse;
}
th, td {
    padding: 4px;
}
</style>  
| Accuracy | 0.6506 |
| Cohen's Kappa | 0.3332 |
| Pos Pred Value | 0.76 |
| NoScore Sensitivity | 0.6992 |
| FG Sensitivity | 0.5431 |
| TD Sensitivity | 0.5055 |
| NoScore Specificity | 0.8110 |
| FG Specificity | 0.8362 |
| TD Specificity | 0.8187 |  
    
<br/> 

This is actually pretty darned good for the assumptions and limitations inherent to logistic regression. But what we actually care about here isn't actually just the classification accuracy, it's the accuracy of the _probabilities_ generated by the model, since we'll be multiplying these probabilities by the actual points in order to generate an Expected Points value given that situation. When we do this, we get a __correlation between predicted score and actual score of 0.4790 in our test set.__ This is even better than the GAM. 
  
### Multilayer Perceptron (artificial neural network)  
Artificial neural networks with a large number of layers (so-called "deep" neural networks) have seen an explosion of usage in the past decade or so, particularly in their more sophisticated forms (such as convolutional and recurrent neural networks). In a simple neural network, a set of predictors activates a collection of artificial neurons (where different neurons are sensitive to different inputs and combinations). Each of these neurons then passes its activation forward to the next layer of neurons (where each neuron in the next layer is sensitive to different neurons in the first layer, in different combinations). This continues until you reach an output layer of neurons, the activation of which corresponds with the the model predictions. Neural networks are trained by specifying the shape and rules governing the neural network, starting with random associations for each neuron in the network, and then slowly updating those connections to minimize anything that produces bad predictions. This is an incredibly flexible wy to model relationships between predictors and outcomes, and the things this sort of approach can accomplish are pretty staggering (in the past year, deep convolutional neural networks have totally mopped the floor against the best players in the world in both [no-limits Texas Holdem](https://www.youtube.com/watch?v=jLXPGwJNLHk) and the ancient game of [Go](https://www.youtube.com/watch?v=g-dKXOlsf98) (AlphaGo AI is now the [top-ranked player in the world](https://www.youtube.com/watch?v=nFwj-m3XSgk) - see als [this](https://www.youtube.com/watch?v=XhrXfbwz7fg)). You can read more about neural networks [here](http://neuralnetworksanddeeplearning.com/chap1.html).  
  
__Strengths__: Incredibly flexible, can handle complicated interactions (including local interactions and high-order interactions) and nonlinearities, often very high-performing.  
__Weaknesses__: very large number of parameters (and rules) that need to be set/assumed by the modeler, totally opaque, can't handle discontinuous effects.  
  
We fit a multi-layer perceptron network with 5 layers. The input layer used z-transformed predictors (with no explicit interactions - the model will handle this on its own) which were shuffled during model fitting (see these and other guidelines used for this neural network [here](http://yann.lecun.com/exdb/publis/pdf/lecun-98b.pdf)). The output layer was a single neuron reflecting expected value of the state of play in points (i.e. we are using the MLP to perform a regression). The three hidden layers had 50, 10, and 20 neurons (ordered from from input to output), determined by a manual series of grid searches across number of neurons and number of layers with 4-fold cross validation. Based on past high-performance models, we used a [rectifier activation function for the neurons](https://en.wikipedia.org/wiki/Rectifier_(neural_networks)). The learning rate was constant, but the tolerance for model improvements was set to a very low level to encourage a highly optimized final model. L2 regularization paremeter was determined by iterative manual grid search over 9 orders of magnitude (settling on a = 0.005), with 4-fold cross validation. The network weights were trained using a stochastic optimization algorithm called "[adam](https://arxiv.org/abs/1412.6980)". Initial weights were randomized for all neurons.  
  
The results:  
  
<style>
table, th, td {
    border: 1px solid black;
    border-collapse: collapse;
}
th, td {
    padding: 4px;
}
</style>  
| 1st down r | 0.4452 |
| 2nd down r | 0.4601 |
| 3rd down r | 0.4799 |
| 4th down r | 0.6584 |
| Overall r | 0.4945 |
  
<br/> 

It's lightyears ahead of the GAM on 4th downs (really leveraging it's flexability there in the most predictable circumstances), but the other correlation coefficients are pretty similar (though always higher for the neural network). Overall, the __correlation between predicted score and actual score of 0.4945 in our test set.__ It's not a surprise, really, that this is the sort of problem that neural networks can handle really well, with lots of strange little local interactions (e.g. "field goal range becomes absolutely critical on 4th downs except in cases where the team is down by between 4 and 7 points with little time left on the game clock, unless the probability of converting the 4th down is a lot better than the probability of making the long field goal in which case clock time becomes less important but the quality of the defense becomes more important" etc.). Though we gave the parameter optimization a good shot, it's likely that we could continue to improve upon the neural network more and more given time. The current cutting-edge predictions for EPA would likely come from a single deep-learning model, and while we are doing our best to go overboard here, developing such a model is a little outside the scope of this humble website at the moment.  
  
### Random Forest Regression  
Many of the first EPA models are based on essentially just taking the average outcomes of different game situations. Finding the average outcome on a 1st down from the OPP 29-25, 1st down from the OPP 24-20, 1st down from the OPP 19-15 etc. The "bins" of data points that are averaged together are all specified in advance, on the presumption that the distinctions made are important ones. A slightly similar approach could be to define some kind of rule, like "find the thing that splits the data in a way that seems important" (where "thing", "split", and "important" are all given precise technical definitions), and let the algorithm make the distinctions. Perhaps it splits the data into cases where the ball is within the OPP 6 and cases where it is not. For each "branch" of this split, you then repeat the process. Perhaps for the "further than OPP 6" plays, it splits the data into "plays on 1st down" and "plays not on 1st down", while for the "within the OPP 6", it splits the data into "plays on 4th down" and "plays not on 4th down". You keep growing this "tree" with more and more "branches", with some sort of stopping rule - when it no longer makes sense to continue splitting the data. Then, given this complex hierarchical series of splits, you go all the way down to the bottom of each branch, and take the average. Then, for any new play, you start from the root of the tree (for ease use, we generally orient this as the "top" of the tree so you can work your way down), continue to a terminus, and use that average as your prediction. We're just taking averages, but the splitting is done to maxamize explanatory power in our outcome, rather than assumed in advance. This is called a "decision tree" (you can [read more about decision trees, and see some examples, here](https://medium.com/towards-data-science/decision-trees-in-machine-learning-641b9c4e8052)). Naturally, the exact numerical predictions you get (as well as the structure of the tree) depend on awful lot on the exact trials (and features) you happen to include in your model. To get around this "overfitting to the data" problem, it's common to build lots and lots of trees using random samples of our data set and random combinations of our predictors (see note below). A collection of "decision trees" is called a "forest", and a forest that was grown using this sort of randomization procedure is called a "random forest model" (specifically, when taking averages at the terminal nodes, "random forest regression"). 
  
__Strengths__: Extremely good at finding weird relationships (including nonlinear effects, discontinuous effects, local interactions, high-order interactions), awesome with large data sets, the data can be screwy with really weird distributions.  
__Weaknesses__: Very inefficient way to try to capture simple, continuous, linear effects. Somewhat of an opaque method. Isn't great at projecting rare outcomes. Doesn't benefit from cases where the data has a known structure or distribution. Will often only give you reasonable projections for cases that are similar to a number of previous instances in the training data (i.e. it doesn't do "trends"). Lots of parameters that need to be set by the modeler.  

We fit a random-forest regression model over non-rescaled training data. Quality of candidate splits was assessed using Mean Squared Error over the outcome. Max depth (number of branches in the longest path from root to terminal node), minimum number of samples required to split a node, number of randomly sampled features used to grow each individual tree, and number of trees (which sklearn calls "number of estimators") were all optimized using a series of increasingly precise grid searches with two-fold cross validation. Note: for this last parameter, sklearn documentation claims that using the max possible features for regression problems is recommended, but this is empirically unlikely in cases where overfitting is possible, is not the recommendation of the folks who developed the model (who recommend n/3), and results in something that isn't even techncially a random forest. As such, we conducted an exhaustive grid search over possible values of this as well, rather than assume any particular recommendation, and chose the parameter that provided the empirical best fit. Our final, optimized parameters were a max depth of 10, a minimum requirement of 100 samples to implement a new split, 7 possible features per tree (out of 11), and 1500 trees in the forest.  
  
The results:  
  
<style>
table, th, td {
    border: 1px solid black;
    border-collapse: collapse;
}
th, td {
    padding: 4px;
}
</style>  
| 1st down r | 0.4447 |
| 2nd down r | 0.4556 |
| 3rd down r | 0.4796 |
| 4th down r | 0.6578 |
| Overall r | 0.4932 |
  
<br/>  
  
Overall, great predictive accuracy. On par with the neural network models. Like the neural network models, it's also likely that we could continue to acheive incremental improvements in this model by continuing to optimize the parameters. We did a reasonable job optimizing the four most important parameters, but there are [about a dozen](http://scikit-learn.org/stable/modules/generated/sklearn.ensemble.RandomForestRegressor.html) that we have available to fiddle with. Unlike the neural networks, however, it's likely that we would hit up against diminishing returns here a bit more quickly. The limited data for rare events is a really hard problem for random forests to surpass, because it doesn't "use" information that could potentially be gleaned from potentially similar circumstances that happened to end up in a similar terminal node. In contrast, deep (convolutional) neural networks are extremely good at identifying local patterns that are conceptually similar to local patterns elsewhere in the data, and projecting to novel situations is usually not a problem (because it is actually modeling the nuances of the relationships).  
  
### Support Vector Machine Regression Ensemble  
Support Vector Machines (SVMs) were hot shit in the 90s. It's very much a computer scientist's way of thinking about regression: rather than assuming some particular type of relationship between predictors and outcomes and finding the exact numerical values that maximize the likelihood of the data given that relationship (a statistician's approach to regression), we instead set some rules about a "desire to keep error acceptably low" (where the exact error doesn't matter so long as it is within acceptable bounds) and a "desire for the line to be flatter when possible" (where we are given a free parameter to tell the algorithm how much to go out of it's way to catch data points), and then programming a clever way to iteratively approach the best solution for those rules. A quirk of this approach is that a good chunk of your data doesn't actually matter and has no impact on the exact form that the regression line takes - SVMs "care" a lot about any situation where it might make a significant error if it doesn't do a decent job of drawing a line, and a lot less about any case a sufficiently large error is unlikely (or, rather, not present in the training data). SVMs turned out to be extremely good at binary classification problems (is it this thing or that other thing?), because focuses in like a lazer on the boundary between classes and doesn't get distracted by all the data that is clearly one thing or another. Regression is a tougher problem than binary classification, but SVMs are flexible enough that decent results are usually obtainable.  
  
__Strengths__: Continuous, non-linear relationships. Weird distributions. Manages to be extremely flexible with only a handful of free parameters that need to be set by the modeler.  
__Weaknesses__: Doesn't handle discontinuous relationships (and discrete data) particularly well. Very prone to over-fitting unless a lot of brute force is applied to optimizing parameters. 
  
It's worth mentioning that the high flexibility obtainable by just a handful of parameters makes fitting a good SVM basically a problem of optimization: which values make for the best predictions? We don't need to assume much, we can just try out a huge number of possible values and see what works the best. In fact, we know in advance that different situations (e.g. downs) might be best explained by different optimal parameters, so we can take advantage of the optimizability of SVMs by fitting the best parameters for each of these different circumstances, such that we have a different predictive model for each different down, meaning that we don't need to compromise on the predictive capacity of any particular down in order to do the others well. So instead of fitting a single SVM regression model, we'll fit (and optimize) four.  
  
The primary parameters that we need to optimize are the "capacity" (denoted by C), which determines how strongly the SVM will "prefer" simpler regression lines (vs more flexible regression lines that will go out of their way to capture training data points), and the "acceptable error" threshold (denoted by epsilon), within which the SVM will ignore the particular error values. C is used to balance predictive power with possible overfitting, while epsilon determines how much of the data is "important" to fitting the model. For each down, we conducted an exhaustive grid search over every possible combination of 6 different orders of magnitude of C and 9 different orders of magnitude of epsilon, then further refined in successively more precise values within those best-fit orders of magnitudes. 1st and 2nd downs were optimized using 5-fold cross-validation with 7000 SVM iterations, while 3rd and 4th downs (which have less data and thus are fit more quickly) were optimized using 6-fold cross-validation and slightly more iterations. All available kernels were initially explored by hand ('linear', 'poly', 'rbf', and 'sigmoid'), but the [radial basis function kernel](http://openclassroom.stanford.edu/MainFolder/DocumentPage.php?course=MachineLearning&doc=exercises/ex8/ex8.html) consistantly provided the best results, so we used it for all optimization and final models. The final optimized models for each down were all fit using 10,000 iterations. 
  
It's also possible to use the SVMs for multinomial classification rather than regression, and then take the class probabilities as our outcome, like we did for logistic regression. However, SVM classification probabilities are notoriously circumspect. I tried it out anyways and it was, indeed, terrible. We stick with SVM regression.  
  
The results (remember that each down is a different SVM model with different optimized parameters):  
  
<style>
table, th, td {
    border: 1px solid black;
    border-collapse: collapse;
}
th, td {
    padding: 4px;
}
</style>  
| 1st down r | 0.4025 |
| 2nd down r | 0.2977 |
| 3rd down r | 0.4520 |
| 4th down r | 0.6229 |
| Overall r | 0.3203 |
  
<br/>  

For reasons that are not at all clear to me, the SVM is absolutely terrible with 2nd downs, despite being optimized separetely for each down. It's also a bit sub-par with first downs. But it still handily beats the GAM on 4th downs, and may be picking up on some unique explanatory power considering the unique way it's approaching the problem. __As such, we will only use the Support Vector Machine predictions from 3rd and 4th downs in our final ensemble predictions. SVM will be omitted from 1st and 2nd down predictions.__  
  
