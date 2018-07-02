## Information about the repository
This repository is created for having a place for education material and creating GitHub Pages. Currently materials are not there yet, but there will be materials for learning machine and AI learning. 

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

New materials should be located under directory _posts. Each teaching material is in its file, which should be named like yyyy-MM-dd-material-name.md and include lines 
````
---
layout: default
---
````
at the beginning of the file so that the layout is right. File content should be markdown (markdown cheatsheet can be found [here](https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet)).

