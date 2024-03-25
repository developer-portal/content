---
title: Jekyll
subsection: web-app
order: 5
---

# Jekyll
Jekyll is simple static site generator that focuses on blogs, but can be used for all kinds of sites. It takes html templates and posts written in [Markdown](https://daringfireball.net/projects/markdown/syntax) to generate static website which is ready to deploy on your favorite web server. Alternatively you can host it on GitHub and publish it via [GitHub Pages](https://pages.github.com), absolutely for free.


## Installation

```
$ sudo dnf install ruby-devel
$ gem install jekyll
```


## Usage

```
$ jekyll new my-site
$ cd my-site
$ jekyll serve
```

Then navigate your browser to <http://localhost:4000> and see the page. It looks quite nice just by default, right? In case you want to re-design or modify the layouts, please visit appropriate [documentation](https://jekyllrb.com/docs/home) to see more info.


## Writing a post
Jekyll makes blogging easy and fun. You do not have to configure database nor write your posts in some uncomfortable web editor. Everything you have to do is just creating a text file in `_posts` directory. Such file must be named in following pattern `YEAR-MONTH-DAY-some-post-title.md` (i.e. `2016-05-02-my-first-post.md`).

At the beginning of the post file belongs [YAML](http://yaml.org) header which is followed by your text. Please see this example post.

```
---
layout: post
title: My first post
---

Here goes some text formated in Markdown. We can do **bold text**,
hyperlinks to our favorite pages, such as [developer-portal](https://developer.fedoraproject.org),
and many other cool stuff.

See <https://daringfireball.net/projects/markdown/syntax>
```

Refresh the page and the post will be there. It is easy as that.


## What next
- See YAML headers magic possibilities [Front Matter](https://jekyllrb.com/docs/frontmatter)
- See how to migrate your current blog [Migrate your blog](https://import.jekyllrb.com/docs/home)
- See how to deploy your page [Deployment](https://jekyllrb.com/docs/deployment-methods)
