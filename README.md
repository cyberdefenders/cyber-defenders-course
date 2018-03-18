# Cyber Defenders Course Website

This static website hosts the **Introduction to Cyber Security Course** for the Cyber Defenders Hackathon.

## Adding New content

Course documentation is written in markdown and is converted to html when the site is served using Jekyll and Kramdown. [Here](https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet#html) is a quick reference on how to write in markdown.

Since the markdown is converted to html, Youtube videos can be embedded by adding the following code directly into the markdown:

`<br>
<div class="embed-responsive embed-responsive-16by9">
  *Embedded link from youtube*
</div>
<br><br>`

The wrapping class makes the youtube video resize with the website. This is done using bootstrap.
