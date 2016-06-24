# Controllers


# Models

```Ruby
accepts_nested_attributes_for :tasks, :tags, :allow_destroy => true, :reject_if => proc { |a| a['name'].blank? }
```



# Routing


# Rake

rake 