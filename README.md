# Easy Publish

Easy publish is a Python library that provides a simple abstraction for publishing text files as blog posts. 


## Installation

Requires: Python >= 3.6

`python3 -m pip install easy-publish`


## Usage

To use easy publish call the `generate_posts` function pointing it to the directory your files are located in. Below is an example flask app with jinja templating that utilizes easy publish, however any web framework/templating engine should work with easy publish.

```
from flask import Flask, render_template
from easy_publish import generate_posts

app = Flask(__name__)
posts = generate_posts("~/my/blogposts")

@app.route("/blog")
def blog():
  return render_template("blog.html", metadata=posts.metadata)

@app.route("/blog/<p>")
def blogpost(p):
  return render_template("post.html", post=posts.posts[p])
```

Then you can use the `metadata` and `post` objects in your projects. Metadata is useful for listing all of you blog posts while Post is useful for templating the content. `blog.html` and `post.html` might look like the following:

### blog.html
```
{{% for post in metadata %}}
  <li>{{ post.title }}</li>
  <li>{{ post.date }}</li>
  <li>{{ post.tags }}</li>
  <li>{{ post.author }}</li>
{{% endfor %}}
```

### post.html
```
<h1>{{ post.title }}</h1>
<h4>{{ post.date }}</h1>
<h4>{{ post.author }}</h1>
<p>{{ post.content }}</p>
```

## Formatting Posts

Easy publish currently expects text files to have a field at the top denoting the metadata. The field must be in the following format:

```
~
title: title would go here
date: date would go here
tags: tags, would, go, here (comma separated)
author: author would go here
~
```
The parser looks for information in between the ~'s and strips it out into the metadata. It's on the list of TODO's to add different ways to include metadata. 


## Contributing

Currently in heavy development and not a stable interface. Feel free to contribute ideas as issues or as a pull request.

## License

MIT
