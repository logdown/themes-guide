## Pages

*  `{% block index_page %}`
*  `{% block show_page %}`
*  `{% block tags_page %}`
*  `{% block search_page %}`
*  `{% block archives_page %}`

## Post

### Title / URL

* `{{post.title}}`
* `{{post.absolute_url}}`

### Content

* `{{post.content}}`

### Content in Search Page

```
{% block search_page %}
  {{ post.content | search_content: query_string }}
{% endblock %}

```

### Excerpt Content & Read More

```
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

```
{% block facebook_sharing %}
    YOUR CONTENT HERE
{% endblock %}

```

### Twitter Sharing

```
{% block twitter_sharing %}
    YOUR CONTENT HERE
{% endblock %}

```

### Google Plus Sharing


```
{% block google_plus_sharing %}
    YOUR CONTENT HERE
{% endblock %}

```


