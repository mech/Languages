# Rails Migration

## References

* [Pare back default `index` option for the migration generator](https://github.com/rails/rails/pull/23179)

```ruby
# index: true is only available in Rails 4
t.references :user, index: true

# In Rails 5, no longer need to index: true because we almost always want to index references.
t.references :session_user, type: :uuid
```