---
layout: post
title:  "Octopress? No Thanks."
date:   2014-10-20 22:00:00
categories: jekyll ruby octopress
image: 'http://i.imgur.com/8gtUvb1.jpg'
---

### Keep it Simple Stupid
When I went down the path of using Jekyll for blogging, I really liked how in control I was of my content.  The source was exactly as I had wrote it, WYWIWYG (what you write is what you get), and every post I wrote in markdown would be pushed to GitHub in its original format.  I was able to edit posts easily from any device right on GitHub.  However, when I switched over to Octopress, for the fancy plugins, I would lose that flexibility and it would ultimately bite me in the ass.

### Managing Two Repos
Using plain jane Jekyll you push markdown files to your GitHub Pages repo and GitHub knows how to do the rest to generate viewable HTML files.  Octopress is sort of counter intuitive, in that it generates HTML out of your Markdown files and puts that into a deploy folder that will be pushed to your GitHub pages repo.  You then have to create a second repo for the source code Octopress uses to generate the HTML.  Now you are managing two repos for the same content.

Since Octopress has to generate HTML files out of your markdown, this makes editing or adding new posts more cumbersome.  You can no longer use the power of markdown or liquit templates on the fly. No more going to your GitHub repo and editing the files remotely, or adding files remotely.  You now have clone your Octopress source repo and generate the content from there and deploy from there.... 

Needless to say, I am no longer using Octopress.

### Conclusion
Now I know there are all sorts of ways around the described problem above, but it's so much overhead for such a little gain.  Jekyll is lightweight, fast and easy.   Why complicate it with such a bloated framework like Octopress? The answer is, you shouldn't.



