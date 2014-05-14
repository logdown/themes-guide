## Example Template

* <https://github.com/logdown/themes/blob/gh-pages/its-compiling/index.liquid>
* <https://github.com/logdown/themes/blob/gh-pages/fabric/index.liquid>
* <https://github.com/logdown/themes/blob/gh-pages/greyshade/index.liquid>

<hr>

# API

## Pages Blocks

These blocks will render wrapped content on specified pages.

### Syntax

Render on only one type of page:

```html
{% block index_page %}
    YOUR CONTENT HERE
{% endblock %}
```

Render on multiple types of page:

```html
{% block index_page|show_page %}
    YOUR CONTENT HERE
{% endblock %}
```

### Available Blocks

| Block Name      | Description                         |
| --------------- | ----------------------------------- |
| `index_page`    | Render on blog homepage.            |
| `show_page`     | Render on blog post page.           |
| `archives_page` | Render on blog archives page.       |
| `search_page`   | Render on search result page.       |
| `tags_page`     | Render on post lists of a tag.      |
| `category_page` | Render on post lists of a category. |
| `static_page`   | Render on every static pages.       |


## Post

There are many variables to print out content or information of a posts. But those variables need to be put *inside* a posts “wrapper block.”

The posts wrapper block defines where a single blog post should be rendered in. The block will repeat itself if the page has more than one post (and it usually does). On a show page, the block will only be rendered once.

### Posts wrapper block

```html
{% block posts %}
  <article class="post">
    POST CONTENT HERE
  </article>
{% endblock %}
```

### Simple post variables

| Variable Name                   | Description                                                                        |
| ------------------------------- | ---------------------------------------------------------------------------------- |
| `{{post.title}}`                | Render the title of a blog post.                                                   |
| `{{post.absolute_url}}`         | Render the absolute URL of a blog post.                                            | 
| `{{post.content}}`              | Render the blog post content.                                                      |
| `{{post.published_at}}`         | Render post publish time. The time can be further formated (see below.)            |
| `{{post.author_name}}`          | Render the display name of a blog post's author.                                   |
| `{{post.disqus_comments_link}}` | The URL to comments part of a post. (Only if you have disqus setup for your blog.) |

#### Publish time format options

Usage: `{{post.published_at.(format_option)}}`

| Format Option  | Description                                                       |
| -------------- | ----------------------------------------------------------------- |
| `short_month`  | Abbreviated month. (ex. “Jan”)                                    |
| `day_of_month` | Day of the month with zero padded. (01–30)                        |
| `full_year`    | 4-digit year. (ex. 2014)                                          |
| `timestamp`    | The time as a number of seconds since the Epoch.                  |
| `utc`          | Time in UTC format. (ex. “2007-11-19 14:18:51 UTC”)               |
| `time_ago`     | Render the relative distance of time from now. (ex. “2 days ago”) |
| `date`         | Formated as date-only. (ex. “April 7, 2013”)                      |

#### Highlighted post content in search results page

```html
{% block search_page %}
  {{ post.content | search_content: query_string }}
{% endblock %}

```

#### Excerpt post content & Read More link

```html
{% block index_page|tags_page %}
   {{ post.excerpt_content }}
     {% block readmore %}
      <a href="{{post.absolute_url}}" class="more">Read on →</a>
     {% endblock %}
{% endblock %}
```



## Social Sharing Condition Blocks

These blocks will only render its wrapped content if you enable social sharing options in your blog settings. You still have to provide the social plugin markup in the condition blocks (so you can choose to add a Facebook Like Button or Share Button, for instance.) But Logdown will load the official scripts from Facebook, Twitter and Google Plus for you.

### Facebook Social Plugins

```html
{% block facebook_sharing %}
  <div class="fb-like" data-href="{{post.absolute_url}}" data-layout="button_count" data-send="false" data-show-faces="false" data-width="90"></div>
{% endblock %}
```

### Twitter Buttons

```html
{% block twitter_sharing %}
  <a href="https://twitter.com/share?" class="twitter-share-button">Tweet</a>
{% endblock %}
```

### Google Plus +1 Button

```html
{% block google_plus_sharing %}
  <div class="g-plusone" data-size="medium"></div>
{% endblock %}
```

###  Comment

This only works when you `enable_comment` & having `disqus_shortname`

```html
{% block disqus %}
<section id="comment">
  <h2 class="title">Comments</h2>
  {% disqus %}
</section>
{% endblock %}
```

### Pagination

```html
  {% block pagination %}
  <div class="pagination pagination-centered">
    <ul>
      {% block previous_page %}
        <li class="prev previous_page ">
          <a href="{{previous_page_url}}">Previous</a>
        </li>
      {% endblock %}

      {% block jump_pagination %}

        {% block current_page %}
          <li class="active">
            <a href="#">{{page_number}}</a>
          </li>
        {% endblock %}

        {% block page_gap %}
          <li class="disabled">
            <a href="#"><span class="gap">…</span></a>
          </li>
        {% endblock %}

        {% block jump_page %}
          <li>
            <a href="{{page_url}}">{{page_number}}</a>
          </li>
        {% endblock %}

      {% endblock %}

      {% block next_page %}
        <li class="next next_page ">
          <a href="{{next_page_url}}">Next</a>
        </li>
      {% endblock %}
    </ul>
  </div>
  {% endblock %}
```

example css: <http://logdown.com/stylesheets/default_pagination.css>

### Recent posts

```
{% block recent_posts %}
  <section class="first odd">
    <h1>Recent Posts</h1>
    <ul id="recent_posts">
      {% block posts %}
      <li class="post">
        <a href="{{ post.absolute_url }}">{{post.title}}</a>
      </li>
      {% endblock %}
    </ul>
  </section>
{% endblock %}
```


### Tag

```
{% block tag_list %}
<span class="tags">
  {% block tags %}
    <a class='category' href='{{tag.url}}'>{{tag.name}}</a>
  {% endblock %}
</span>
{% endblock %}
```




## Blog

<http://logdown.com/account/settings>

* `{{blog.author_about_me}}`
* `{{blog.author_gravatar_hash}}`
* `{{blog.author_display_name}}`
* `{{blog.author_about_me_link}}`
* `{{blog.author_github_profile_link}}`
* `{{blog.author_facebook_profile_link}}`
* `{{blog.author_google_plus_link}}`
* `{{blog.author_twitter_link}}`
