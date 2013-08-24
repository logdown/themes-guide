## Post

### Content

* `{{post.title}}`
* `{{post.absolute_url}}`

### Date / Time

* `{{post.published_at.utc}}` : 2013-04-07 07:59:00 UTC
* `{{post.published_at.date}}` : April  7, 2013


## Social Sharing


```
            <div class="share">
              <div class="addthis_toolbox addthis_default_style ">
                {% block twitter_sharing %}
                <a class="addthis_button_facebook_like" fb:like:layout="button_count"></a>
                {% endblock %}

                {% block twitter_sharing %}
                <a class="addthis_button_tweet"></a>
                {% endblock %}
               
                {% block google_plus_sharing %}
                <a class="addthis_button_google_plusone" g:plusone:size="{{ site.google_plus_one_size }}"></a>
                {% endblock %}
                <a class="addthis_counter addthis_pill_style"></a>
              </div>
              <script type="text/javascript" src="http://s7.addthis.com/js/250/addthis_widget.js#pubid={{ site.addthis_profile_id }}"></script>
            </div>
```            
