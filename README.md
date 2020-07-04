# Multiscale Biological Modeling Test Website

*Remember to use F5 as a hard refresh when looking to make rapid edits + previews* 
Strange refresh order: it seems certain elements do not update on Github Pages at same time. E.g.
  1. Edit text in file to say "Hi" + change navigation
  2. Wait a few minutes, refresh preview, see changed navigation but no text
  3. Edit text in file to say "Hi2"
  4. Wait a few minutes, refresh preview, see changed navigation and "Hi"

Github Pages References: https://mmistakes.github.io/minimal-mistakes/docs/quick-start-guide/

Kramdown Markdown Reference: https://kramdown.gettalong.org/quickref.html

Which page layout to use? https://mmistakes.github.io/minimal-mistakes/docs/layouts/

The home page is "/index.md"

**Notice** Text in a notice should start with a double asteriks for emphasis, and requires a special piece of code on the next line 
{: .notice--primary}

To add a new page, add a file (html or markdown) to "_pages" update "_data/navigation.yml"

Quick References: 

~~~~~~
This is also a code block.
~~~
Ending lines must have at least as
many tildes as the starting line.
~~~~~~~~~~~~

~~~ ruby
# specify the language at the starting tilde
def what?
  42
end
~~~


A [link](http://kramdown.gettalong.org "hp")
to the homepage.

Can also use a variable, delcared below, to [link][kramdown hp]
to the homepage.

[kramdown hp]: http://kramdown.gettalong.org "hp"

An image: ![gras](assets/images/bio-photo.jpg)
