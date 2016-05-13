---
title: Creating A Bootstrap Progress Widget
date: 2016-05-12 16:38:24
tags: 
author: Nate Cowen
---
If you haven't figured out already, this site is going to be used for several purposes. First, it's going to be the new home of my portfolio site and blog. Second, it's a testing ground for developing and improving my technical skillset. I hope to solidify my understanding of current technologies and programming concepts through blog posts like this one.

In order to stay on track and continue improving, I want to be able to track my progress. I decided to create a progress bar widget for this purpose. This widget can be seen in the side bar with the title, *"Currently Working On."*  <!-- more -->I stole this idea from one of my favorite authors, Brandon Sanderson. [On his website](http://brandonsanderson.com/), he has a progress bar that tracks where he is at in his writing. I liked this idea and decided to replicate it on my own website.

---
## Starting to Code


My Hexo template is based off the blog [*Create A Hexo Theme*](http://www.codeblocq.com/2016/03/Create-an-Hexo-Theme-Part-1-Index/) on CodeBlocq.com. This tutorial provided a great foundation on static site generators; I highly recommend reading it. After running through this tutorial, I was able to start creating my progress bar widget. 

The first file that needed to edit was the _config.yml file located within the root folder of my theme. This file contains repetitive data that is used in multiple locations of the website. This includes items like site title, site, description, and widgets.  I adding the lines "learning:", "-topic:", and "percent:" within the "widgets:" section of my config.yml file. See the code below: 
<pre>
sidebar: right
widgets:
    about: Hi, I'm Nate. I create code. I work mainly in front-end, but I'm developing my full-stack skillset. <br/><br/>I'm fascinated by data science, programming, and tech in general.
    tags: true
    skills: HTML, CSS, Design, Development, Web Marketing, Digital Concept Creation, Junior Level Programming (C#, VBA, PHP, AS3)
    learning: 
    
        - topic: Static Site Generators (Hexo)
          percent: 35%
        
        - topic: Bootstrap
          percent: 25%
          
        - topic: Node.js
          percent: 15%
          
        - topic: Advanced Programming Concepts and Terminology
          percent: 20%
          
        - topic: Git/Version Control
          percent: 65%
          
        - topic: Unit Testing
          percent: 1 %  
          

</pre>

The code above is used to populate the content for the "currently working on" section. The next step is to create the logic that is responsible for loading the content into the widget. I created a blank file with the name "learning.ejs" within my theme's layout folder. The specific path in my case was */layout/_partial/widget/*.

I began by testing a bit of hardcoded HTML within the "learning.ejs" file. <code>&lt;span&gt;This is some test content&lt;/span&gt;</code>. With Hexo server running, I refreshed the page and verified that my test content had populated the widget. Success! 

With the widget loading test content, I began to work on parsing out the data from my config.yml file. The final code I wrote can be seen below. It uses a combination of Bootstrap objects, EJS (Javascript Templates), and CSS from the CodeBlocq.com tutorial.

---
### Building the Logic

<pre>
&lt;% if(theme.widgets.learning){ %&gt;
    &lt;div class="sidebar-module sidebar-module-inset"&gt;
        &lt;h4&gt;Currently Working On &lt;h4&gt;
            
        &lt;% for(var i=0; i&lt;theme.widgets.learning.length; i++) { %&gt;
            &lt;span&gt;&lt;%= theme.widgets.learning[i].topic %&gt;&lt;/span&gt;
        
       		&lt;div class="progress "&gt;
  				&lt;div class="progress-bar progress-bar-striped" role="progressbar" aria-valuenow="60" aria-valuemin="0" aria-valuemax="100" style="width: &lt;%= theme.widgets.learning[i].percent %&gt;;"&gt;

  				&lt;/div&gt;
			&lt;/div&gt;
    	&lt;% } %>
        
    &lt;/div&gt;
&lt;% } %&gt;

</pre>

That's a lot to digest, so let me break it down into bite sized pieces. The first line of code uses EJS to check if theme.widgets.learning exist.<br/> <code>&lt;% if(theme.widgets.learning){ %&gt;</code>  Essentially, it is looking for the nested "learning" code that was placed under the "widgets" section of the config.yml file. If it returns true, the program moves to the next line. 

Next, a div with the classes of "sidebar-module" and "sidebar-module-insert" is inserted. The div classes are part of the theme CSS from codeblocq.com. The classes provide styling to the widget box section. This particular CSS file is located within the *themefolder/source/css/blog.css.

Next, I used EJS to create a for loop. This for loop counts the number of items within the widgets/learning section of the config.yml file. It then prints the name of the topic using the following code. <br/> <code>&lt;p&gt;&lt;%= theme.widgets.learning[i].topic %&gt;&lt;/p&gt;</code>

Finally, the progress bar width is set to the percent located within the widgets section of the config.yml code. The progress bar is a feature of bootstrap. [You can learn more about it here](http://getbootstrap.com/components/#progress). The code used to set the progress bar can be seen below. <br/> <code> style="width: &lt;%= theme.widgets.learning[i].percent %&gt;;"&gt;</code> 

---
### The End
That's the end of this tutorial. I learned a lot about static site generators, Bootstrap, and Javascript templating through this process. I hope you have too. 