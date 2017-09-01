---
layout: page
title: Downloads
permalink: /downloads/
---  

You can <a href="http://github.com/Forever-Peace/GroundControl/raw/master/rushing_data_stack.csv" download>download the data stack used for the Ground Control project here.</a>  
  
To download directly into R, use the following commands:  
  
~~~ R  
library(readr)  # for read_csv
library(knitr)  # for github connection
df <- read_csv("http://raw.github.com/Forever-Peace/GroundControl/master/rushing_data_stack.csv")
~~~   
  
To download directly into Python, use the following commands:  
  
~~~ python
import pandas as pd
url = 'http://raw.github.com/Forever-Peace/GroundControl/master/rushing_data_stack.csv'
df = pd.read_csv(url,index_col=0)
~~~
