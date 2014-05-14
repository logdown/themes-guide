## Example Template

* <https://github.com/logdown/themes/blob/gh-pages/its-compiling/index.liquid>
* <https://github.com/logdown/themes/blob/gh-pages/fabric/index.liquid>
* <https://github.com/logdown/themes/blob/gh-pages/greyshade/index.liquid>

<hr>

# Logdown Themes API

## Blog Variables

These variables will print infos of your blog. Some of them can be changed in your blog settings.

| Variable Name                           | Description                                                            |
| --------------------------------------- | ---------------------------------------------------------------------- |
| `{{blog.absolute_url}}`                 | Absolute URL to your blog.                                             |
| `{{blog.title}}`                        | Title of your blog.                                                    |
| `{{blog.tagline}}`                      | Tagline of your blog.                                                  |
| `{{blog.description}}`                  | Description of your blog.                                              |
| `{{blog.rss_url}}`                      | URL of RSS Feed for your blog.                                         |
| `{{blog.search_posts_url}}`             | The Search action URL for your blog. Can be used for blog search form. |
| `{{blog.archives_url}}`                 | URL to your blog archives page.                                        |
| `{{blog.author_about_me}}`              | The “About Me” text of the blog's creator.                             |
| `{{blog.author_gravatar_hash}}`         | The gravatar hash for the blog's creator.                              |
| `{{blog.author_display_name}}`          | The display name of the blog's creator.                                |
| `{{blog.author_about_me_link}}`         | URL to the about.me profile of the blog's creator.                     |
| `{{blog.author_github_profile_link}}`   | URL to the github profile of the blog's creator.                       |
| `{{blog.author_facebook_profile_link}}` | URL to the Facebook profile of the blog's creator.                     |
| `{{blog.author_google_plus_link}}`      | URL to the Google Plus profile of the blog's creator.                  |
| `{{blog.author_twitter_link}}`          | URL to the Twitter profile of the blog's creator.                      |


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

### Post Tags List

```
{% block tag_list %}
<span class="tags">
  {% block tags %}
    <a class='category' href='{{tag.url}}'>{{tag.name}}</a>
  {% endblock %}
</span>
{% endblock %}
```

###  Disqus Comment Block

This block will render the disqus comment block for you, only if you have set the disqus shortname in your blog settings. If a blog post is explicitly comment-disabled through the octopress markdown header, this block will not render on the post page.

The `{% block disqus %}` is the conditional block which renders its content if the page can show a comment block. And the `{% disqus %}` will be replaced with markup needed for disqus.

```html
{% block disqus %}
<section id="comment">
  <h2 class="title">Comments</h2>
  {% disqus %}
</section>
{% endblock %}
```

### Traversing through previous/next post

These block can give your reader quick access to previous or next post.

```html
{% block previous_post %}
  <a class="prev" href="{{previous_post_url}}">
    &larr; {{previous_post_title}}
  </a>
{% endblock %}

{% block next_post %}
  <a class="next" href="{{next_post_url}}">
    {{next_post_title}} &rarr;
  </a>
{% endblock %}
```

## Social Sharing Conditional Blocks

These blocks will only render its wrapped content if you enable social sharing options in your blog settings. You still have to provide the social plugin markup in the conditional blocks (so you can choose to add a Facebook Like Button or Share Button, for instance.) But Logdown will load the official scripts from Facebook, Twitter and Google Plus for you.

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

## Blog Index Pagination

```html
{% block pagination %}
  CONTENT INSIDE BLOCK
{% endblock %}
```

This block will render on your blog index if pagination is needed. You can set how many posts you want to show per page in your blog settings.

### Pagination Component Blocks

All pagination component blocks should be put within the `{% block pagination %}` wrapper block.

```html
{% block (block_name) %}
  CONTENT INSIDE BLOCK
{% endblock %}
```

| Block Name        | Description                                      |
| ----------------- | ------------------------------------------------ |
| `previous_page`   | Render if a “prev” page navigation is available. |
| `next_page`       | Render if a “next” page navigation is available. |
| `jump_pagination` | Render the page jump links.                      |

And Variables:

| Variable Name           | Description                                                                              |
| ----------------------- | ---------------------------------------------------------------------------------------- |
| `{{previous_page_url}}` | URL to previous pagination page. Should be put inside `{% block previous_page %}` block. |
| `{{next_page_url}}`     | URL to next pagination page. Should be put inside `{% block next_page %}` block.         |

### Page Jump Components

These components should be put in the `{% block jump_pagination %}` block to build the page jump markups.

| Block Name     | Description                                               |
| -------------- | --------------------------------------------------------- |
| `current_page` | Wrap markups to show number of current page.              |
| `page_gap`     | Wrap markups to show the pagination gap (usually “...”).  |
| `jump_page`    | Wrap markups to show the page jump link with page number. |

And Variables:

| Variable Name     | Description                                                                              |
| ----------------- | ---------------------------------------------------------------------------------------- |
| `{{page_number}}` | Number of the pagination page where the page jump links to. Should be put inside `{% block current_page %}` or `{% block jump_page %}` block.
| `{{page_url}}`    | URL to the pagination page where the page jump links to. Should be put inside `{% block jump_page %}` block.

### Complete example for a pagination block

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

Stylesheet for the example pagination block above: <http://logdown.com/stylesheets/default_pagination.css>

## Recent Posts List

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
