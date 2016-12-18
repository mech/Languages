# Ruby or Rails Security

* [Sakurity](http://sakurity.com/blog)
* [How to steal any developer's local database](http://bouk.co/blog/hacking-developers/)
* [Common Rails Security Pitfalls](https://www.sitepoint.com/common-rails-security-pitfalls-and-their-solutions/)
* [Sanitize](https://github.com/rgrove/sanitize/)

```erb
<%= sanitize(@blog.body, tags: %w(b strong em i)).html_safe %>
```

## SQL Injection

* [Rails SQL Injection Examples](http://rails-sqli.org/)