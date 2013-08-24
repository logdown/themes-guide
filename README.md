## Pages

### Index Page

```
{% block index_page %}
    YOUR CONTENT HERE
{% endblock %}
```

### Show Page

```
`{% block show_page %}`
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

```
{% block search_page %}

    YOUR CONTENT HERE
{% endblock %}
```

###  Archives Page

```
{% block archives_page %}
    YOUR CONTENT HERE
{% endblock %}
```


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


