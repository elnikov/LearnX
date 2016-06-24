# Controllers


# Models

#AutoSave
Заменяеть процедуру сохранения нестед атрибута
```Ruby
belongs_to :client, :autosave => true

private def autosave_associated_records_for_client
    if new_client = Client.find_by_email(client.email)
      self.client = new_client
    else
      self.client.save!
end
```


##Вложеные аттрибуты 
https://github.com/alloy/complex-form-examples/tree/master/app/models
https://github.com/plataformatec/simple_form/wiki/Nested-Models

Создание вложенный атрибутов моделей для мульти модельных форм. 
:reject_if отклонение создание с условием
```Ruby
accepts_nested_attributes_for :tasks, :tags, :allow_destroy => true, :reject_if => proc { |a| a['name'].blank? }
```

##Валидация
###Контекст

Есть один момент, валидация у которой есть контекст, по умолчанию выполняеться не будет.

Если у валидации нет контекста, она выполниться в любом контекст
```Ruby
validates :client, presence: true, on: :context_name
```
Model.valid?(:context_na,e)

Model.validate(:context_name)



# Routing


# Rake

rake 
