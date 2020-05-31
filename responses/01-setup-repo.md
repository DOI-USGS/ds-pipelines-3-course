Great, here we go! You'll be revising files in this repository shortly. To follow a process similar to our team's standard git workflow, you should first clone this training repository to your local machine so that you can make file changes and commits there. 

### :keyboard: Activity: Set up your local repository

Open a git bash shell (Windows) or a terminal window (Mac) and change (`cd`) into the directory you work in for projects in R (for me, this is `~/Documents/Code`). There, clone the repository and set your working directory to the new project folder that was created:
```
git clone git@github.com:{{ user.username }}/{{ repo }}.git
cd {{ repo }}
```

### :keyboard: Activity: Install packages as needed

You may need to install some of the packages for this course if you don't have them already. These are:

* **scipiper**
* **remake**
* **tidyverse**
* **dataRetrieval**
* **urbnmapr**
* **leaflet**
* **leafpop**
* **htmlwidgets**

If you don't already have **remake** and **scipiper** installed, refer to the documentation [here](https://github.com/USGS-R/scipiper/blob/master/README.md#installation) to install those packages.

Install **urbnmapr** with `remotes::install_github('UrbanInstitute/urbnmapr')`.

All the rest should be installable with `install.packages()`.

<hr><h3 align="center">When you're set up locally, close this issue.</h3>
