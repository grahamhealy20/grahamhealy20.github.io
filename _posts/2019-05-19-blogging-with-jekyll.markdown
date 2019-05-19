---
layout: post
title:  "Blogging with Jekyll"
date:   2019-05-19 14:21:00 +0100
categories: jekyll blog programming pizza github pages
---
Hi, in this blog article I'm going to go through how I set up this blog (blog-ception 🤯) using Jekyll.

### What's Jekyll?

[Jekyll](https://jekyllrb.com/) is a static-site generator used for generating websites using [Markdown](https://en.wikipedia.org/wiki/Markdown). This means you don't need to worry about writing custom HTML/CSS (you can if you want!) and you can focus on writing your own content.

Jekyll is different than the traditional CMS systems such as Wordpress in the fact that it doesn't use a traditional database such as MySQL. Everything is composed as files which are then picked up by Jekyll and converted into HTML/CSS which can be served as a website.

### Why I chose Jekyll
I decided to go with Jekyll for my website/blog as I didn't want the operational overhead of having to install and manage a more heavyweight option such as a CMS like Wordpress. I just wanted something simple where I could configure how I wanted the site to look and then it was just a matter of me writing my blog posts in Markdown. I also didn't want to have to pay for hosting (we'll talk about that later! 😉). One other benefit is that since it's compiled static files, there is some great SEO optimisation.

If you are willing to go a little bit lower level then you traditionally would with something like Wordpress/Drupal then you can have a nice blog with very minimal effort!

## Prerequisites
### Ruby
Before we go any further, we are going to make sure we have a few things installed first.
Firstly we are going to require [Ruby](https://www.ruby-lang.org/en/) since that is what Jekyll is written in, so make sure you go off and [install it](https://www.ruby-lang.org/en/documentation/installation/).

### Bundler and Jekyll
Once Ruby is installed then we need to go ahead and install [Bundler](https://bundler.io). Bundler is used to manage Ruby library dependencies. If you've worked in other programming languages before it would be similar to pip or Maven. We can also install Jekyll itself at this point too since its also a Ruby gem.

```bash
gem install bundler jekyll
```

You should see some output like this:

```bash
Successfully installed bundler-2.0.1
Parsing documentation for bundler-2.0.1
Done installing documentation for bundler after 2 seconds
Successfully installed jekyll-3.8.5
Parsing documentation for jekyll-3.8.5
Done installing documentation for jekyll after 0 seconds
2 gems installed
```

## <a name="generating-the-jekyll-project"></a> Generating the Jekyll project
### Run the Jekyll generator
Now that we have Ruby, bundler and Jekyll installed, it's time to actually generate the Jekyll project. This is super easy and it's just a matter or running the `new` command that Jekyll provides:

```bash
jekyll new my-awesome-blog
```

You should see something like this:

```bash
Running bundle install in /Users/grahamhealy/workspace/blogs/my-awesome-blog...

  Bundler: Fetching gem metadata from https://rubygems.org/...........
  Bundler: Fetching gem metadata from https://rubygems.org/.
  Bundler: Resolving dependencies...
  Bundler: Using public_suffix 3.0.3
  Bundler: Using addressable 2.6.0
  Bundler: Using bundler 2.0.1
  Bundler: Using colorator 1.1.0
  Bundler: Using concurrent-ruby 1.1.5
  Bundler: Using eventmachine 1.2.7
  Bundler: Using http_parser.rb 0.6.0
  Bundler: Using em-websocket 0.5.1
  Bundler: Fetching ffi 1.11.0
  Bundler: Installing ffi 1.11.0 with native extensions
  Bundler: Using forwardable-extended 2.6.0
  ...
  Bundler: Bundle complete! 4 Gemfile dependencies, 29 gems now installed.
  Bundler: Use `bundle info [gemname]` to see where a bundled gem is installed.The dependency tzinfo-data (>= 0) will be unused by any of the platforms Bundler is installing for. Bundler is installing for ruby but the dependency is only for x86-mingw32, x86-mswin32, x64-mingw32, java. To add those platforms to the bundle, run `bundle lock --add-platform x86-mingw32 x86-mswin32 x64-mingw32 java`.
New jekyll site installed in /Users/grahamhealy/workspace/blogs/my-awesome-blog.
```

This is great! This means that Jekyll has successfully generated the blog inside the `my-awesome-blog` folder. Looking inside this folder with the `tree` command we see the following folder structure:

```bash
~/workspace/blogs/my-awesome-blog tree
.
├── 404.html
├── Gemfile
├── Gemfile.lock
├── _config.yml
├── _posts
│   └── 2019-05-19-welcome-to-jekyll.markdown
├── about.md
└── index.md
```
We don't need to worry about most of these files yet but for now the ones we should be concerned about are `_config.yml` and `index.md`.

### Serve the Jekyll site
We have the Jekyll site generated, but how do we actually see it? To achieve this, Jekyll provides a `serve` command which runs a small lightweight web server. Run the following command to start the Jekyll server:

```bash
bundle exec jekyll serve
```

We should see some console output letting us know that compilation and server startup was all good:

```bash
Configuration file: /Users/grahamhealy/workspace/blogs/my-awesome-blog/_config.yml
            Source: /Users/grahamhealy/workspace/blogs/my-awesome-blog
       Destination: /Users/grahamhealy/workspace/blogs/my-awesome-blog/_site
 Incremental build: disabled. Enable with --incremental
      Generating...
       Jekyll Feed: Generating feed for posts
                    done in 0.606 seconds.
 Auto-regeneration: enabled for '/Users/grahamhealy/workspace/blogs/my-awesome-blog'
    Server address: http://127.0.0.1:4000/
  Server running... press ctrl-c to stop.
```

Note the server address (`http://127.0.0.1:4000`) that is output to the console, we can navigate to this in our browser of choice and see our new Jekyll blog in all its glory! 😎

![Screenshot of Jekyll homepage at 127.0.0.1:4000](/assets/jekyll_homepage.jpg)

Well.. maybe not glory, it's a little plain right now. But we can change that! Let's go and add some content to the homepage.

## Adding Content
Firstly, let's change the name of our site, I want to name it after myself (since it's my personal blog and I'm a littttle bit full of myself! 😜)

We can do this very easily by modifying the global `_config.yml` file we seen earlier [when we generated the Jekyll project](#generating-the-jekyll-project).

Let's look inside. We can see that inside contains a number of key, value pairs which indicate settings that Jekyll uses when generating our site. Since we want to change the title, we are  going to change, yes, you guessed it.. the `title` property:

```
# Welcome to Jekyll!
#
# This config file is meant for settings that affect your whole blog, values
# which you are expected to set up once and rarely edit after that. If you find
# yourself editing this file very often, consider using Jekyll's data files
# feature for the data you need to update frequently.
#
# For technical reasons, this file is *NOT* reloaded automatically when you use
...
...

title: Graham Healy's Blog!
email: your-email@example.com

...
...
#   - vendor/bundle/
#   - vendor/cache/
#   - vendor/gems/
#   - vendor/ruby/
```
We now need to rebuild and reserve the Jekyll site to pick up our changes.

```bash
bundle exec jekyll serve
```

![The new updated Jekyll blog title!](/assets/new_title.jpg)

Check it out! Our new title has shown up! Now that we've done the title, let's add a little something about ourself to the home page.

This time, instead of modifying the global `_config.yml` we are going to add some new content using markdown.

Open `index.md` in your favourite editor and change it to the following (or add your own fact about yourself!)

```markdown
---
# Feel free to add content and custom Front Matter to this file.
# To modify the layout, see https://jekyllrb.com/docs/themes/#overriding-theme-defaults

layout: home
---
Hi! I'm Graham. I'm mildly addicted to Pizza and Coffee!
```
One cool thing about Jekyll is that it will automatically take your edits/updates and automatically recompile them for you without having to stop and re-run the `serve` command again. This is a really nice timesaver!

Going back to our website, when we refresh we can see the updated content! Nice!
![The new content on the homepage!](/assets/new_index.jpg)


## Adding blog posts
Now that we've changed the title and added a little bit about ourselves I think it's time that we add some posts to our blog! Another big feature of Jekyll is that it is **blog aware**. This means we simply have to pop in a new file in the posts directory and boom, we're done!

Let's go ahead and do that now. I'm going to add a new post talking about my favourite types of Pizza. To do this, I'm going to create a new Markdown file called `2019-05-19-my-fave-pizza.md` and I'm going to save it inside the `_posts` directory. Our posts directory should now look like this:

```bash
ls _posts
2019-05-19-my-fave-pizza.md           2019-05-19-welcome-to-jekyll.markdown
```

Great! Now I'm going to setup the markdown to what Jekyll expects it to look like. We need to tell Jekyll a few things, such as the type of page it is (post in this case), the time it was created and any tags we want to associate the post with. My file looks like this:

```markdown
---
layout: post
title:  "My Fave Pizza"
date:   2019-05-19 15:27:27 +0100
categories: jekyll pizza food
---
I love big pepperoni pizzas. Pineapple should **NEVER** belong on any pizza ever. Fight me.
```

This file is a Markdown file but there is some Jekyll specific data at the top between the `---` lines. This is called *front-matter* which describes the page data to Jekyll. This is important because if it wasn't there Jekyll wouldn't know what type of HTML template to use or what the title of the page would be. You can learn more about front-matter [here](https://jekyllrb.com/docs/front-matter/).

So my article is done, since we have the Jekyll `serve` command running, we simply need to refresh the page on the browser and we should see our new shiny blog post!

![The new blog post is showing up!](/assets/new_blog_post.jpg)

And when we click on the blog post hyperlink, low and behold! Our blog content! Notice how the Markdown is rendered as HTML, pretty cool!

![The new blog content](/assets/new_blog_content.jpg)

And that's how easy it is to add new posts to our blog!

## Hosting
So now that we have our blog generated with our new post, how can we serve this to to the public internet? Right now it's only running on our local desktop/PC. Since Jekyll simply generates static files from Markdown, it's just a matter of generating said static HTML files and deploying them to the hosting provider of your choice. To generate the static files just run the following command:

```bash
jekyll build
```

The resulting static files generated by Jekyll will be stored in the `_site` directory. We would then need to upload these somehow, usually via SFTP or SSH.
This is good as a once off, but if we needed to make a change or add a new blog post we would need to regenerate the static files and upload them again and again which would become tedious.

But what if I told you there was a way to automate the static file generation and host your blog for **free?**

<p style="text-align: center;"> *audible gasps 😱* </p>

![Morpheus explains to Keanu Reeves how to host his blog for free](/assets/morpheus.jpeg)


### GitHub Pages
You can! By using [GitHub pages!](https://pages.github.com/) This will deploy the latest version of your Jekyll site and serve the files whenever you push your latest changes to the GitHub repository. Find out how to set this up [here](https://jekyllrb.com/docs/github-pages/).

## All done
That's it, your done! You've found out how to install Jekyll, generate your new blog, add your own content, publish your new blog posts and host it all for free! Now you can push your extremist views on Pizza toppings to the entire world 🍕!

Thanks for reading.
Graham
