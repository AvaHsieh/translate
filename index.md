<ul>
    {% for article in site.Chinese-English %}
        <li><a href="{{article.url}}" target="_blank">{{ article.title }}</a></li>
    {% endfor %}
    {{article.url}}
</ul>

<ul>
    {% for article in site.English-Chinese %}
        <li><a href="{{article.url}}" target="_blank">{{ article.title }}</a></li>
    {% endfor %}
</ul>

