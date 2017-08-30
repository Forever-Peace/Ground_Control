---
title: Installation Instructions
---  

## Running the Apps
Running the apps, for free, compiled directly from the publically available source code, is very simple. You will need to install the R Statistics program, update a few plugins, then simply enter the run command for the app you want to use.  

## How to Install R  

(1) [Install Microsoft R Open here](https://mran.revolutionanalytics.com/open/). You do not need the MKL libraries, but can take the opportunity install them now to enable multithreading support on your R installation. Default installation options is sufficient, but you can change anything that you would like to. Microsoft R Open is a distribution of the [R Statistics Program](https://www.r-project.org) with a fixed repository of plugin versions, ensuring that you and I will be using the same versions of everything. If you are familiar with R, or have an existing R install you would prefer using, that should be fine, and you can move ahead to step 2.  
(2) [Install RStudio here](https://www.rstudio.com/products/rstudio/download/). The default installation options are sufficient. This is a user interface for R that will make it easier for you to use. This step is technically optional, but strongly recommended.  
  
Now, whenever you want to run R, you should launch RStudio. It should look something like this when you first open it:  
![RStudio](/GroundControl/images/Rstudio_firstopen.png)  
  
The "console" panel on the left is where you will enter commands to run. The tabs in the panel at the bottom-right include a number of helpful things, but the most pertinent for now is the "Packages" tab. This lists all of the packages currently downloaded into your R install.  
  
## How to Update the necessary packages  
  
(3) We'll the console panel to udpate the necessary packages. Copy-paste the following commands into the R Console:
{% highlight R %}install.packages("ggplot2")  
install.packages("shiny")  
install.packages("reshape2")  
install.packages("FNN")  
{% endhighlight %}<br/>   

All dependencies will be downloaded and installed automatically to your R Packages folder. The new packages will appear in the "Packages" tab.

## How to Download and Run the Apps  
  
(4) Simply enter the packages "run command" into the R console. All run commands are two lines of code: the first loads the "shiny" package to enable interactive apps, and the second retrieves the source code and data from the github repository and opens the app. For example, this will open the ["Head to Head Competitions" app](/GroundControl/apps/rb_head2head/):  
  
{% highlight R %}
library("shiny");
runGitHub("Forever-Peace/GroundControl", subdir = "Chapters/shinyapps/rb_head2head/")
{% endhighlight %}<br/> 
 
Each of the apps should automatically retrieve the packages they need from your local packages library. But just in case, loading and unloading packages can be done manually by checking or un-checking the box next to that package. 
  
The "library("shiny")" command must be run once after opening RStudio. After that, the "runGitHub" command for the app of your choice can be used to open each app, without re-running the "library("shiny") command. The runGitHub commands for each app are listed in the [table of contents](/GroundControl/contents/#apps).
