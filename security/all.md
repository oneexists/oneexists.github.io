## Computer Security Blog Posts

<ul>
  {% for post in security.posts %}
  <li>
    <a href="{{post.url}}">{{post.title}}</a>
  </li>
  {% endfor %}
</ul>
