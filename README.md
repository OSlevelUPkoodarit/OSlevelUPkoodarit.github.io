## Information about the repository
This repository is created for having a place for education material. Currently only materials on the site are from data science workshops.

## Running the website locally
These instructions work have been tested with MacOS, not Windows or Ubuntu.

In order to use the code one has to have Ruby and Jekyll installed. More information about installing them can be found in [Jekyll-website](https://jekyllrb.com/docs/installation/). 

After installing them you need to run (in terminal):
````
bundle install
````

and after that 
````
jekyll serve --livereload
````
This starts the webserver so that one can see how the page looks in http://localhost:4000. Livereload option means that changes in files can be seen immediately. 

Drafts of new materials can be located under directory _drafts. If one wishes to see them locally, one should add option --drafts when starting the server. When it is ready for publishing, it should be located under directory _posts. Each published teaching material is in its file and the file should be named like yyyy-MM-dd-material-name.md where yyyy means current year, MM means current month and dd means current day. The file should include lines 
````
---
layout: post
---
````
at the beginning of the file so that the layout is right. File content should be markdown (markdown cheatsheet can be found [here](https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet)).

