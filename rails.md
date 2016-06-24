# Controllers


# Models

##Вложеные аттрибуты 
https://github.com/alloy/complex-form-examples/tree/master/app/models
https://github.com/plataformatec/simple_form/wiki/Nested-Models

Создание вложенный атрибутов моделей для мульти модельных форм. 
:reject_if отклонение создание с условием
```Ruby
accepts_nested_attributes_for :tasks, :tags, :allow_destroy => true, :reject_if => proc { |a| a['name'].blank? }
```



# Routing


# Rake

rake 
