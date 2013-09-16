## Example Template

* <https://github.com/logdown/themes/blob/gh-pages/its-compiling/index.liquid>
* <https://github.com/logdown/themes/blob/gh-pages/fabric/index.liquid>
* <https://github.com/logdown/themes/blob/gh-pages/greyshade/index.liquid>

<hr>

# API

## Pages

### Index Page

```html
{% block index_page %}
    YOUR CONTENT HERE
{% endblock %}
```

### Show Page

```html
{% block show_page %}
    YOUR CONTENT HERE
{% endblock %}
```

### Tags Page

```
{% block tags_page %}
    YOUR CONTENT HERE
{% endblock %}
```

### Search Page

```html
{% block search_page %}

    YOUR CONTENT HERE
{% endblock %}
```

###  Archives Page

```html
{% block archives_page %}
    YOUR CONTENT HERE
{% endblock %}
```


## Post

### Title / URL

* `{{post.title}}`
* `{{post.absolute_url}}`

### Authour Info

* `{{post.author_name}}`
* `{{post.author_account_name}}`

### Content

* `{{post.content}}`

### Content in Search Page

```html
{% block search_page %}
  {{ post.content | search_content: query_string }}
{% endblock %}

```

### Excerpt Content & Read More

```html
{% block index_page|tags_page %}
   {{ post.excerpt_content }}
     {% block readmore %}
      <a href="{{post.absolute_url}}" class="more">Read on →</a>
     {% endblock %}
{% endblock %}
```

### Date / Time

* `{{post.published_at.utc}}` : 2013-04-07 07:59:00 UTC
* `{{post.published_at.date}}` : April  7, 2013


## Social Sharing

### Facebook Share

```html
{% block facebook_sharing %}
    YOUR CONTENT HERE
{% endblock %}

```

### Twitter Sharing

```html
{% block twitter_sharing %}
    YOUR CONTENT HERE
{% endblock %}

```

### Google Plus Sharing


```html
{% block google_plus_sharing %}
    YOUR CONTENT HERE
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
