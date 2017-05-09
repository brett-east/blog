---
layout: post
title: 'Making the move to Jekyll'
excerpt_separator: <!--- more --->
comments: true
description: 'Making the move to Jekyll'
twitterdescription: 'Making the move to Jekyll - by Brett East'
tags: ['jekyll', 'liquid', 'markdown']
---

I’m always slack with keeping my blog up to date, whether through lack of time to write something, lack of topics to write about, or more recently the effort it takes to write a blog and post it on my site.
<!--- more --->

In an attempt to solve this last point, I took a couple of evenings last week to learn about the static site compiler Jekyll and to then move my blog over to a statically generated site, and what better post to try out this new process than with than a brief tale about how I went about doing that.

## What is Jekyll

An important part of this post is to know what Jekyll is, I imagine if you’re reading this you already know a little about Jekyll, but I’ll give a quick explanation here anyway. So from their website:
> Jekyll is a simple, blog-aware, static site generator. It takes a template directory containing raw text files in various formats, runs it through a converter (like Markdown) and our Liquid renderer, and spits out a complete, ready-to-publish static website suitable for serving with your favorite web server.

Here is a link to the [Jekyll][jekyll] website for you to have a look yourself, but basically, once setup, it allows you to write page templates and content using [Liquid](https://shopify.github.io/liquid/) and [Kramdown](https://kramdown.gettalong.org/) flavour of Markdown, and then you can run a command from the terminal and it will compile your templates, partials and content into a static website. There’s nothing exciting or crazy that needs to happen on the server, you’re only serving up a static site, all the magic happens when you compile your partials locally – and that can all happen in the background while you’re working away on your site.

Jekyll is great for building any static website even if you only use it for Liquid’s templating syntax (I’ve used it before to create simple internal help docs and style guides), but some of its greatest advantages come in the form of being ‘blog aware’. Up until moving my own blog over to Jekyll, I hadn’t really had much to do with the blogging side of the site generator, but knowing it had these capabilities, I decided to jump in and see what I could do.

## Step 1: Identify what I want to end up with and why

Before moving my blog over to using Jekyll, I needed to make sure I could still do what I wanted with it and that it would solve the problems I was looking to solve (I want to quickly note, that Jekyll is a site generator and not a blogging platform, so when I talk about moving my blog to Jekyll, I just mean to using it to generate my blog).

The first place to start is the ‘why’, and that was pretty easy to answer. Up to this point, I had been writing my blog posts in straight up html and essentially hardcoding the posts into my site, I mean I was crudely using AngularJS as a way to template in my header, footer and nav, but that was overkill and my initial setup to write a blog post often required copying code from an old post and swapping out the content. This was my own fault and was a result of "let’s just get a post up there and come back later and put a better process/framework in place" – which is exactly what I was doing now, it had just taken 11 months to get around to doing.

So what did I want? I wanted:

**An easy way to upload new posts**

<i class="fa fa-check checkmark" aria-hidden="true"></i> once set up I could just write a new post in markdown, run Jekyll and my post would be added

**To keep using disqus comments**

<i class="fa fa-check checkmark" aria-hidden="true"></i> a quick look online showed there was no issue with using disqus and Jekyll

**To add tags to my blog posts**

<i class="fa fa-check checkmark" aria-hidden="true"></i> this is something that Jekyll is really good at

**To use a consistent, reusable template**

<i class="fa fa-check checkmark" aria-hidden="true"></i> again something Jekyll, using liquid templating, is great at

**To move my blog to a subdomain and use git-ftp to upload it**

<i class="fa fa-check checkmark" aria-hidden="true"></i> being that I’m just hosting a static website, that’s super easy, no need for a massive deployment pipeline

## Step 2: Where to start

Thankfully this was really easy, given that I already had a blog with pretty much the design that I wanted, it meant that moving to Jekyll was super easy. No need to come up with too much of a design or even to write that much code, I would just have to take what I had and break it up into logical pieces for templating. Given how easy this process was, I think that if I was coding up a Jekyll blog from scratch, I would nearly start with just writing a plain blog in html first and then pulling it out into templates. I think being able to jump into straight html gives you a lot of freedom, mostly because you’re not moving between multiple files and any changes that come up a really easy to implement. I’m not saying that starting with Jekyll would be all that difficult, just that I personally found with process of taking an existing website and separating it into pieces really straightforward.

So already, things were looking great, being able to use my existing code was going to save me a tonne of time.

## Step 3: Starting with Jekyll

This was actually one of the biggest pains I had, and all my own fault. I had in the weeks previous been playing around with Yarn, cleaning up some global npm packages and basically trying to clean up my environment, I had also had a couple of issues with homebrew and decided to get rid of it. Foolishly in all of this, I had removed the OS version of Ruby and a few other packages that I shouldn’t have :/ - in the end I had to reinstall homebrew, get Ruby back and Ruby Version Manager. Once I’d done that however, installing Jekyll was as simple as

{% highlight bash %}
$ gem install jekyll
{% endhighlight %}

The next step is simply to run

{% highlight bash %}
$ Jekyll new <directory> --blank
{% endhighlight %}

to create a new Jekyll project in the directory provided. By default, Jekyll comes with a theme and a hides the `assets`, `_sass`, `_layouts` and `_includes` directories in the theme’s gem file, but using the `--blank` flag sets up a project with no theme. Given I already had a design and layout to use from my existing blog, I didn’t want to install an extra theme – and I’m not a big fan of not being able to see files that get pulled into the design.

## Step 4: Move my existing code into my Jekyll blog

This blog post isn’t meant to be seen as a Jekyll tutorial more just a look back at my experience with it, so I will gloss over some of the details here. Essentially I began by copying my header and footer into include files, and then setting up my default layout and adding an index page. I just used static content to get the layout right, that is to say I wasn’t pulling any content in from blog posts to display on the homepage, I was just coding it directly onto the page. Running `Jekyll serve` let me run a local server and preview changes as I saved files, and I could see how the layout looked and if the basics were working.

Then I was able to move onto converting my existing blog posts to markdown and including them in a posts directory, and adding their relevant yaml front matter. This process wasn’t too hard, a few online services let me quickly convert html to markdown by cutting and pasting it into the browser. The front matter let me pick which layouts to use, add some content like ‘title’, ‘date’, some metadata for SEO and let me pick a breakpoint for content to be displayed on the homepage. By this point I had my blog looking the same as it did currently  and I was able to then look at adding some of the extra features that come with Jekyll like tags and pagination.

## Step 5: Add the extras

With my blog running the same as it was currently, minus the disqus comments, it was time to get stuck into adding some of the extra features I now had access to thanks to Jekyll. Firstly, pagination on my index page, I wanted to display 4 posts on my homepage and add pagination after that. Adding pagination was relatively simple after adding the plugin and updating the `_config.yml` file, getting the next and previous buttons to appear on the homepage took a little more work, mostly just due to the verbose liquid syntax needed to get it to work properly.

{% highlight bash %}
$ gem install jekyll-paginate
{% endhighlight %}

Then my this in my `_config.yml`

{% highlight yaml %}
paginate: 4
paginate_path: '/page:num/'
{% endhighlight %}

This was the necessary liquid

{% highlight html %}
{% raw %}
<div class="row">
  <div class="pagination"> {% if paginator.previous_page %}
    {% if paginator.previous_page == 1 %}
    <p class="prev-link"><a href="{{site.baseurl}}/" class="previous">&larr; newer entries</a></p>
    {% else %}
    <p class="prev-link"><a href="{{site.baseurl}}/page{{paginator.previous_page}}" class="previous">&larr; newer posts</a></p>
    {% endif %}
    {% endif %}
    {% if paginator.next_page %}
    <p class="next-link"><a href="{{site.baseurl}}/page{{paginator.next_page}}" class="next">older posts &rarr;</a></p>
    {% endif %} </div>
</div> <!-- paginator row -->
{% endraw %}
{% endhighlight %}

Tags are as easy to add to a post as simply including them in the front matter of a post, creating an archive page is a little more tricky, but thankfully I was able to follow a great [Lynda.com](https://www.lynda.com/Jekyll-tutorials/Jekyll-Web-Designers/383124-2.html) I was able to include a pretty cool page that included all my posts sorted by tags.

Setting permalinks was also pretty easy, as was providing the url structure that I wanted for my posts. Adding `permalink: /:title/` in my `_config.yml` file meant that my posts had pretty urls without the .html extension.

## Step 6: Adding Disqus comments

This was actually really easy, and I found a great blog post that showed exactly how to make it happen. All you have to do though is moved your existing disqus comment code into an include file and pass in whatever custom properties you need from the blog post front matter. I did update a few of the settings in my disqus file, as I was moving my blog to a new subdomain, and this meant I lost previous comments (for a little bit). Had I have simply replaced my existing blog posts at the same url, all my previous comments would have persisted and that would have been fine. To get my old comments back, I just needed to go into disqus and migrate them across – moving a blog to a new domain is pretty common and disqus make this relatively easy.

## Step 7: Deploy to a subdomain

I moved my blog to a blog.bretteast.me subdomain rather than bretteast.me/blog to keep it separate from the rest of my site, in reality this doesn’t really matter all that much, I just prefer it. I was naturally using git to track my blog as I went, and I knew that I would later use git-ftp to publish to my subdomain. When it came time to do this, I hit a little hiccup, using git-ftp and setting `--syncroot` to `_site` resulted in the entire \_site directory uploading, meaning that my homepage was actually at blog.bretteast.me/\_site/index.html instead of blog.bretteast.me/index.html. That was my fault in the end, a little digging showed that I just needed a `/` at the end of my `--syncroot _site/`.

While this would have been a fix, I decided in the end that I wanted to ignore the \_site directory from my git repo anyway, so that it could just track the changes that I had made, and I wouldn't need to push the generated pages to github. So ignored the \_site directory and initialised a new repo inside it, and then I could use this for just git-ftp, which I think worked out better in the end. 

## Conclusion

So now I’m up and running with my Jekyll blog, and ‘initial setup time’ can no longer be used as an excuse to not write blogs, so here I am kicking it off with this first post, hopefully there will me more to come.

[jekyll]: https://jekyllrb.com/ "Jekyll website"
