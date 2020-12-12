## Information about the repository
This repository is created for having a place for education material. Currently only materials on the site are from data science and Git workshops.

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

The site uses "Just the docs" -theme. Information about how to edit site and to add new pages, you will find in theme's documentation [here](https://github.com/pmarsceill/just-the-docs).

File content should be markdown (markdown cheatsheet can be found [here](https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet)).

