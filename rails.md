# Controllers


# Models

##Сброс валидации

Можно скипать валидацию с условием.
```Ruby
	attr_accessor :skip_uniq_validation 
	validates :email, uniqueness: true, unless: :skip_uniq_validation
	#...............
	@model.skip_uniq_validation=true
	@model.save
```
Ещё с помощью **proc**
```Ruby
class Example < ActiveRecord::Base
  has_one :foo
  has_one :bar

  validates_presence_of :foo
  validates_presence_of :bar, :unless => Proc.new { |example| example.foo == Foo.find_by_name('ThisFooDoesntLikeBars') }
end
```

##AutoSave
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

Model.valid?(:context_name)
Model.validate(:context_name)
```




# Routing


# Rake

rake 

# RSPEC

```Ruby
ActiveRecord::Migration.maintain_test_schema!
```

##PhantomJS

Подключения фантом для windows
```Ruby
if Gem.win_platform?
  Capybara.register_driver :poltergeist do |app|
      Capybara::Poltergeist::Driver.new(app, :phantomjs => 'C:/phantomjs/2.1.1/bin/phantomjs.exe')
  end
end
```

##Capybara
###Настройка капибары
```Ruby
require File.expand_path("../../config/environment", __FILE__)
ENV["RAILS_ENV"] ||= 'test'
require 'rubygems'
require 'spork'
require 'factory_girl_rails'
require 'capybara/rspec'
require 'capybara/rails'
Capybara.configure do |config|    # Также необходимо добавить настройки для Capybara
  config.run_server = true 
  config.server_port = 7000
  config.app_host = "http://127.0.0.1:#{config.server_port}" 
  config.default_driver = :poltergeist
  config.current_driver = :poltergeist
  config.javascript_driver = :poltergeist
  config.save_path = "/vagrant/ultaxi/tmp/capybara_output" unless Gem.win_platform?
  config.save_path = "tmp/capybara_output" if Gem.win_platform?
end
```

