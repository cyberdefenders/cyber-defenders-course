# Cyber Defenders Course Website

This static website hosts the **Introduction to Cyber Security Course** for the Cyber Defenders Hackathon.

## Adding New Course Content

Course documentation is written in markdown and is converted to html when the site is served using Jekyll and Kramdown. [Here](https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet#html) is a quick reference on how to write in markdown.

Since the markdown is converted to html, Youtube videos can be embedded by adding the following code directly into the markdown:

`<div class="embed-responsive embed-responsive-16by9">`
  *Embedded link from youtube*
`</div><br>`

The wrapping class makes the youtube video resize with the website. This is done using bootstrap.

## Running Locally

There are three dependencies needed to be able to serve webpage with Jekyll. Jekyll runs into a lot of issues on Windows so it is easiest to just use Linux or Mac. In Windows you can create a [Linux Subsystem](https://docs.microsoft.com/en-us/windows/wsl/install-win10). From the Linux terminal within Windows all of the necessary tools can be installed.

### Linux

1. Install ruby
~~~~
$ sudo apt-get install ruby-full
~~~~

2. Install gem
~~~~
$ sudo apt-get install rubygems
~~~~

3. Install Jekyll
~~~~
$ sudo gem install jekyll bundler
~~~~

Once these are installed you can clone or download the repository and navigate to the project directory in the terminal. To run the static site use the jekyll commands below:

Runs a new site at a specified local host. Navigate to that localhost in your browser to access the page. Auto-regeneration (watching for changes in files) is enabled automatically.
~~~~
$ jekyll serve
~~~~

Same as above but watches for changes in the file for live reload.
~~~~
$ jekyll serve --livereload
~~~~

More information about basic usage can be found on the [Jekyll website](https://jekyllrb.com/docs/usage/).
