---
date: "2016-04-09T16:50:16+02:00"
title: blogdown
output: 
  learnr::tutorial
weight: 3
---

## blogdown: Creating Websites with R Markdown

"A well-designed and maintained website can be extremely helpful for other people to know you, and you do not need to wait for suitable chances at conferences or other occasions to introduce yourself in person to other people. On the other hand, a website is also highly useful for yourself to keep track of what you have done and thought. Sometimes you may go back to a certain old post of yours to relearn the tricks or methods you once mastered in the past but have forgotten." [Yihui Xie](https://yihui.name/en/)[blogdown: Creating Websites with R Markdown](https://bookdown.org/yihui/blogdown/)

In this section you will learn how to crate static websites using the [blogdown](https://cran.r-project.org/web/packages/blogdown/index.html) package in R that allows you to create websites from [R Markdown](https://bookdown.org/yihui/rmarkdown/) files using [HUGO](https://gohugo.io), an open-source static site generator written in Go.  


<img src="images/rmd_hugo_blogdown.png" width="600px" />

#### What is blogdown?

From Yihui: <https://slides.yihui.name/2017-rmarkdown-UNL-Yihui-Xie.html#35>.

- [R Markdown](https://rmarkdown.rstudio.com) <img src="https://www.rstudio.com/wp-content/uploads/2015/12/RStudio_Hex_rmarkdown.png" width="10%" align="right" />
    - (relatively) simple syntax for writing documents
    
    - the simpler, the more portable (multiple output formats)
    
    - not only convenient (maintenance), but also reproducible
    
    - most features of R Markdown _and_ [**bookdown**](https://bookdown.org) (technical writing)!!



- [Hugo](https://gohugo.io) <img src="https://gohugo.io/img/hugo.png" width="10%" align="right" />

    - free, open-source, and easy to install (a single binary)
    
    - lightning fast (generates one page in one millisecond)
    
    - general-purpose (not only for blogs)

##### Why not WordPress, Tumblr, Medium.com, Blogger.com, etc?

From Yihui: <https://slides.yihui.name/2017-rmarkdown-UNL-Yihui-Xie.html#36>.

- No R Markdown support (even math support is often nonexistent or awkward)

- Huge benefits of static websites compared to dynamic websites
    - all static files, no PHP or databases, no login/password, work everywhere (even offline)
    
    - typically fast to visit (no computation needed on the server side), and easy to speed up via CDN


### Build your website

We will do it step by step. Let us start by setting a GitHub repo for our website project.

##### Prep with GitHub

We are already familiar with GitHub basics, which you can find from [Happy Git with R](http://happygitwithr.com) to connect RStudio with your GitHub account.


<img 
src="http://happygitwithr.com/img/watch-me-diff-watch-me-rebase-smaller.png" align="middle" img width="60%"  
/>

We are going to assume you are already familiar with and have done:

☑️ Capter 5: [Register a GitHub account ](http://happygitwithr.com/github-acct.html)

☑️ Chapter 6: [Install or upgrade R and RStudio ](http://happygitwithr.com/install-r-rstudio.html)

* Go to your GitHub account and create a new repository

<img src="images/New_Repo.png" width="200px" style="display: block; margin: auto auto auto 0;" />

* Give it a meaningful name 
<img src="images/Create_New_Repo.png" width="300px" style="display: block; margin: auto auto auto 0;" />

* Copy repo's **HTTPS** address
<img src="images/HTTPS_GitHub.png" width="350px" style="display: block; margin: auto auto auto 0;" />

##### In RStudio

* Open a new project in RStudio: **File** ➡️ **New Project...**
<img src="images/RS_New_Project.png" width="250px" style="display: block; margin: auto auto auto 0;" />

* Select **Version Control** ➡️ **Git**
<img src="images/Select_Version_Control.png" width="250px" style="display: block; margin: auto auto auto 0;" />

* Paste the address of your Git repo  
<img src="images/set_up_git_connection.png" width="250px" style="display: block; margin: auto auto auto 0;" />

#### Install the packages

* Install <span style="color:red">**blogdown**</span>

`install.packages("blogdown")`


* Install <span style="color:red">**Hugo**</span> using blogdown

`blogdown::install_hugo()`


💡! If you already have those packages installed, you can check to update your <span style="color:red">Hugo</span> package

`blogdown::hugo_version() # check version`

`blogdown::update_hugo() # force an update`

💡! If you are having trouble installing the package try:

`install.packages("blogdown", repos = "http://cran.us.r-project.org")` 🤞

#### Build a website

We'll adopt a *simple is beautiful* approach and start building a website using a <span style="color:red">default theme</span>.

`blogdown::new_site()`

💡! To use a different theme (for example: *hugo-academic*):

`blogdown::new_site(theme = "gcushen/hugo-academic", theme_example = TRUE)`


To see the current **Hugo themes** go to <https://themes.gohugo.io/>.

Let the knowledge and familiarity with `blogdown` and `Hugo` grow first.🧐 Once you get familiar with `blogdown` and `Hugo` you can always switch to a different theme. 💇 <https://bookdown.org/yihui/blogdown/other-themes.html>

#### Structure of a HUGO site

<img src="images/Site_Structure.png" width="200px" style="display: block; margin: auto;" />

<img src="images/main_structure.png" width="200px" style="display: block; margin: auto;" />

<https://gohugo.io/getting-started/directory-structure/>

#### Serve site

* In the console type:

`blogdown::serve_site()` 

or, from `Addins` menu select `servesite` 

<img src="images/Serve_Site.png" width="200px" style="display: block; margin: auto;" />

Don't try to view your site in your teeny RStudio viewer, instead click on <span style="color:red">Show in new window</span>.

<img src="images/show_in_new_window.png" width="250px" style="display: block; margin: auto;" />

#### Notation we will adopt

- **Trailing slash** will indicate a directory name, e.g. `content/` means we are referring to a directory called *content*, not to a file named *content*.

<img src="images/trailing_slash.png" width="150px" style="display: block; margin: auto auto auto 0;" />

- **Leading slash** will indicate the root directory of your *project website*, e.g. `/content/about.md` means we are refering to `about.md` file which is under the root directory of the website project.  

<img src="images/leading_slash.png" width="150px" style="display: block; margin: auto auto auto 0;" />

### Building a website Step by Step

#### 👉 Go to the following GitHub repo to download the material: <https://github.com/TanjaKec/BlogdownWS>

##### From here on we will follow the steps given in Xaringan presentation available from [ 👉 here](https://tanjakec.github.io/BlogdownWS/Blogdown_WS_Slides/blogdown_workshop.html)

### Happy Blogging! 📢 



-----------------------------
© 2019 [Sister Analyst](https://sisteranalyst.org)
