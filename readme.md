## Requirements

* git
* Ruby 2.4.2
* Jekyll 2

## Setup

Verify that you have git installed.

`git -v`

Verify you have the correct version of ruby.

`ruby -v`

Install Jekyll.

`gem install jekyll bundler`

Clone the documentation site to your local machine to get started. 

`git clone https://github.com/astronomerio/documentation.git`

Change directories into the newly downloaded folder. 

`cd documentation`

Install any requirements for the project.

`bundle install`

Run a version of the site locally.

`jekyll serve`

## Where to edit

Remember that others make frequent changes to the site. It's best to `git pull` before you start making changes for the day. If you run into issues just ask for help in `#engineering` and someone can help you with issues.

The hompage is located in the `root` directory in `index.md`.

All additional content is located inside of the `v2` folder. 

Adding pages to the sidebar can be accomplished by editing `_data/sidebars/platform_sidebar.yml`

## Commiting your changes

To add your changes to the site. 
* Add your changes to git. 
* Check to make sure your changes were tracked. 
* Commit your code changes. Make sure to leave a nice message.
* Push your changes to github. 

```
git add .
git status
git commit -m "What did you change?"
git push origin master
```


## Going live!

[Astronomer Temp Doc Site]("https://astronomerio.github.io/documentation/") 