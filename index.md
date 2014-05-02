# Ruby & Ruby on Rails

!SLIDE
# Ruby & Ruby on Rails
## Лисовский Влад, Lakehouse
### lisovskyvlad@gmail.com

#### puts "Hello, World"

!SLIDE center_bg_full
}}} images/ruby.png

!SLIDE left
# Краткая история Ruby
* Разработан японцем Юкихиро Мацумото
* Вышел в свет в 1995 году
* Что хотел создатель:
  * Более мощныи язык, чем Perl
  * Более ООП язык, чем Python
  * Хотел создать новый язык, в котором парадигма функционального программирования сбаланасирована принципами императивного программирования.

!SLIDE center_bg_full
}}} images/matz.jpeg
##### Matsumoto accepting an award from
##### the Free Software Foundation in 2012

!SLIDE left
# Что нужно знать о Ruby

* Открытое программное обеспечение (англ. open-source software)
* Строгая динамическая(утиная) типизация
* Интерпретируемый язык программирования
* Очень объектно ориентированный, всё объект и всё выражение, то есть вычисляется
* Мультипарадигмальный (объектно-ориентированный, рефлективный, императивный, функциональный)
* Для комфортного написания кода достаточно хорошего текстового редактора
* Основные реализации: MRI (2.1.1), JRuby (1.7.12), Rubinius (2.2.6)

!SLIDE
# Строгая динамическая типизация

``` ruby
x = "Hello world!"
puts x        # => "Hello World!"
puts x.class  # => String
puts x.upcase # => "HELLO WORLD!"

x = 10
puts x        # => 10
puts x.class  # => Fixnum
puts x.upcase # => NoMethodError: undefined method `upcase' for 10:Fixnum
```

!SLIDE
# Интерпретируемый язык
#### В поставку языка входит irb (Interactive Ruby Shell)

``` ruby
irb(main):001:0> x = "Hello World"
=> "Hello World"
irb(main):002:0> puts x
Hello World
=> nil
```


!SLIDE
# Всё в Ruby – объекты.
* Для каждой частицы информации или кода могут быть определены собственные свойства и действия.
* Чистейший объектно-ориентированный подход Ruby может быть продемонстрирован парой строк кода
``` ruby
5.times { print "Мы любим Ruby! Ruby – это замечательно!" }
```
* Во многих языках числа и другие примитивные типы данных не являются объектами (например Python).
* Ruby под влиянием языка Smalltalk позволяет задать методы и переменные объекта всем типам данных.

!SLIDE
# Ruby – функционален
* Итераторы

``` ruby
employees = ["Alex", "Bob", "Eve"]
employees.each do |employee|
  puts "Hello #{employee}"
end

puts employees.map { |e| e.reverse } # => ["xelA", "boB", "evE"]
```

* Лямбды

``` ruby
hello = Proc.new do |string|
  puts "Hello #{string}"
end
hello.call "Alice" # => "Hello Alice"
```

!SLIDE
# Рефлективность
* Ruby очень гибкий язык, так как он позволяет его пользователям свободно менять его части
* Основные части Ruby могут быть удалены или переопределены
* Например, если для сложения чисел вы хотите использовать слово plus:

``` ruby
class Numeric
  def plus(x)
    self.+(x)
  end
end

puts 5.plus 6 # => 11
```

!SLIDE center_bg_full
}}} images/ruby_metaprog_book.jpg

!SLIDE
# Метапрограммирование
* Ruby имеет богатые возможности для создания DSL

``` ruby
class User < ActiveRecord::Base
  %w(director marketing carrier admin vrp).each do |role|
    define_method "#{role}?" do
      self.role_name == role
    end
  end

end

user = User.find_by_email('vl@lakehouse.ru')
user.admin? # => true
```

!SLIDE left
# Основы Ruby
* Комментарии
``` ruby
# однострочный комментарий
```
* Переменные:
``` ruby
snake_case = 1
```
* Константы
``` ruby
CamelCase = 200
USER_ACTIONS = ['clean', 'add']
```
* Числа:
``` ruby
with_delimeter = 1_000_000
decimal = 100.01
```
* Интерполяция
``` ruby
puts "20 * 20 = #{20 * 20}" # => "20 * 20 = 400"
```

!SLIDE left
# Скалярные типы
* Встроенная длинная арифметика
``` ruby
large = 1073741823
puts large.class # => Fixnum
large = large + 1
puts large.class # => Bignum
```
* Строки:
``` ruby
single_quote = 'this string'
double_quote = "double 'quote'"
escape = "double \"quote\""
```
* Символы (неизменяемые строки)
``` ruby
:this_is_a_symbol
puts "test".object_id
puts "test".object_id #different
puts :test.object_id
puts :test.object_id  #same
```

!SLIDE left
# Структруированные типы
* Списки
``` ruby
list = [1, "two", 3]
list << "another item"
list[0] = "uno"
puts list.last # => another item
```
* Хэши
``` ruby
prices = {:soda => 30, :chips => 5}
puts prices[:soda] # => 30
prices[:rice] = 12.50
```
* Диапазоны
``` ruby
(1..10).map { |x| 2 ** x } # => [2, 4, 8, 16, 32, 64, 128, 256, 512, 1024]
puts (200..300).include?(280) # => true
```

!SLIDE left
# Операторы
#### Всё работает так как вы привыкли
* +, -, *, /, %, &&, ||, ==, etc
* Нету ++ и --, но есть **
``` ruby
puts 2 ** 10 # => 1024
```

!SLIDE left
# Управлениe потоком
### Скобочки не нужны
* if - else
``` ruby
if x < 0
  puts "x is negative"
elsif x > 0
  puts "x is positive"
else
  puts "x is zero"
end
# в одну строку
puts "x is negative" if x < 0
```

* unless - else
``` ruby
unless [1,2,3].include?(10)
  puts '10 is not in 1..3'
end
# в одну строку
errors.add(:base, 'Error message') unless @user.valid?
```

!SLIDE left
# Блоки и итераторы
``` ruby
list = [1, 2, 3]
list.each { |x| puts x }
list.each do |x|
  puts x
end

prices = { :ball => 300, :linux => 4_000_000_000 }
prices.each_pair do |key, value|
  puts "#{key}: #{value}"
end

100.times { |x| puts "Hello #{x}" }
100.downto(50) { |y| puts y }
```

!SLIDE left
# ООП
``` ruby
class Person
  attr_accessor :name

  # переменная экземпляра начинается с @
  def initialize(name)
    @name = name
  end

  def greet(great_word = 'Hello')
    puts "#{great_word}, #{@name}"
  end
end

person = Person.new('Anatole')
puts person.greet('Hi')
```

##### 'attr_accessor :name' заменяет:
``` ruby
class Person
  def name
    @name
  end

  def name=(name)
    @name = name
  end
end
```

!SLIDE left
# Модули
### Отличие от классов:
* Нельзя наследовать
* Нельзя создать экземпляр
* Можно "подмешать" в классы

``` ruby
# Modules as Mixin
module Swimmer
  def swim
    puts "I'm swimming!"
  end
end
class Person
  include Swimmer
end
Person.new.swim # => "I'm swimming!"
```


!SLIDE left
# Ещё о модулях
* Объявление модуля или класса - константа
* Модули как пространство имён
``` ruby
module X
  class D
  end
end

module Y
  class D
  end
end
X::D.new # Отличается от класса Y::D
```

* В модулях и классах можно объявлять констаны
``` ruby
module MyConstants
  MeaningOfLife = 42
end
puts MyConstants::MeaningOfLife
```

!SLIDE bottom-left
}}} images/rubygems.png


!SLIDE bottom-left
# IDE не нужна - большинство моих знакомых рубистов используют Sublime или Vim
}}} images/sublime.png

!SLIDE left
# Почему Ruby – это круто?
* Высокая скорость разработки
* Практикуется TDD и BDD
* Практикуется применение паттернов и следования принципу DRY
* Мощные средства для написания DSL (Domain Specific Language)
* Большое сообщество движимое чувством прекрасного, любовью к красивому коду и хорошему софту

!SLIDE center_bg_full bottom-left
}}} images/ruby_way.jpeg
# http://therubyway.org/

!SLIDE left
# The Ruby Way™
* Просто, но не слишком просто
* Принцип наименьшего удивления
* Вторичность скорости работы программы
* Динамичность
* Простые строгие правила, выполнение которых не доходит до педантизма
* Потребность создавать полезные и красивые программы, как причина программирования

!SLIDE center_bg_full bottom-left
}}} images/ror.svg
# Ruby on

!SLIDE center_bg_full bottom-left
}}} images/ruby_on_rails.jpg

!SLIDE left
# Краткая история Ruby On Rails
* Разработан датчанином Дэвидом Хейнемейером Ханссоном
* Изначально код был извлечён из [Basecamp](https://basecamp.com/) - система управления проектами
* Компания 37signals, в которой работает Дэвид, недавно переименовалась в Basecamp
* Известен как [@dhh](https://twitter.com/dhh)
* Первый релиз был выпущен в июле 2004 года.

!SLIDE center_bg_full bottom-left
}}} images/dhh.jpg

!SLIDE left
# Что нужно знать о ROR
* Фреймворк, написанный на языке программирования Ruby.
* Реализует архитектурный паттерн MVC (Model-View-Controller) для веб-приложений
* Использует REST-стиль построения веб-приложений.
* Является открытым программным обеспечением и распространяется под лицензией MIT
* Не является языком программирования

!SLIDE left
# The Rails Way™
* DRY (Don’t Repeat Yourself)
* Convention over Configuration
* Предположение о том, что есть лучшии способ что-то сделать (в некоторых случаях препятствует альтернативам)
* Требует понимания The Rails Way, и карает тех, кто тащит старые привычки в Ruby On Rails
* Используется ряд допущений о том, что нужно каждому разработчику для создания нового проекта

!SLIDE center_bg_full bottom-left
}}} images/mvc.png
# MVC

!SLIDE right_bg_full bottom-left
}}} images/rails_tree.png
# Файловая структура приложения

!SLIDE
# Пример контроллера
``` ruby
class ProjectsController < ApplicationController
  skip_before_filter :authenticate_user!, only: [:show]

  def new
    @project = Project.new
  end

  def create
    @project = ::Projects::CreateService.new(current_user, params[:project]).execute
    flash[:notice] = 'Project was successfully created.' if @project.saved?
  end

  def update
    status = ::Projects::UpdateService.new(@project, current_user, params).execute

    respond_to do |format|
      if status
        flash[:notice] = 'Project was successfully updated.'
        format.html { redirect_to edit_project_path(@project), notice: 'Project was successfully updated.' }
      else
        format.html { render "edit", layout: "project_settings" }
      end
    end
  end

  def transfer
    ::Projects::TransferService.new(project, current_user, params).execute
  end
end
```

!SLIDE
# Пример модели
``` ruby
class Project < ActiveRecord::Base
  belongs_to :creator,      foreign_key: "creator_id", class_name: "User"
  belongs_to :group, -> { where(type: Group) }, foreign_key: "namespace_id"

  has_one :gitlab_ci_service, dependent: :destroy
  has_many :events,             dependent: :destroy
  has_many :notes,              dependent: :destroy

  delegate :name, to: :owner, allow_nil: true, prefix: true

  # Validations
  validates :creator, presence: true, on: :create
  validates :description, length: { maximum: 2000 }, allow_blank: true
  scope :public_only, -> { where(visibility_level: Project::PUBLIC) }

  def repository
    @repository ||= Repository.new(path_with_namespace)
  end

  def saved?
    id && persisted?
  end

  def add_import_job
    RepositoryImportWorker.perform_in(2.seconds, id)
  end

  def can_have_issues_tracker_id?
    self.issues_enabled && !self.used_default_issues_tracker?
  end
```

!SLIDE
# Пример шаблона
``` ruby
<h1>Регистрация</h1>
<%= form_for @project do |f| %>
  <%= f.text_field :title %>
  <%= f.text_field :desc %>
  <%= f.label :doc, 'Прикрепить описание проекта' %>
  <div class="field file-uploader">
    Обзор...<%= f.file_field :doc %>
  </div>
  <%= f.label :agreement, class: 'agreement' do %>
    <%= f.check_box :agreement %>
    <span>
      Я соглашаюсь на обработку персональных данных и с
      <%= link_to 'правилами акции', asset_path('rules.pdf'), :target => '_blank' %>
    </span>
  <% end %>
  <%= f.submit 'Создать проект', class: 'submit' %>
<% end %>
```

!SLIDE
# Пример Gemfile
### в Gemfile хранятся зависимости проекта
``` ruby
source 'https://rubygems.org'

gem 'rails', '4.1.0'
gem 'pg'

gem 'sass-rails', '~> 4.0.3'
gem 'uglifier', '>= 1.3.0'
gem 'coffee-rails', '~> 4.0.0'
gem 'therubyracer',  platforms: :ruby
gem 'jquery-rails'
gem 'rails-i18n'

gem 'validates_email_format_of'
gem 'paperclip'

group :development do
  gem 'spring'
  gem 'quiet_assets'
  gem 'awesome_print'
  gem 'better_errors'
  gem 'binding_of_caller'
  gem 'capistrano', '~> 3.0.1'
end
```

!SLIDE left
# Rails это тоже Gem
### На самом деле это 'мета'-гем, он зависит от других:
* Railtie
* ActiveSupport
* ActiveRecord
* ActiveModel
* ActionMailer
* ActionPack(ActionController, ActionDispatch, ActionView)

!SLIDE left
## Проекты, использующие Ruby
* Twitter (до 2009 года)
* GitHub (почти все сервисы гитхаба на ruby/rails/sinatra)
* Slideshare
* ask.fm
* Shopify
* Groupon (американский сервис в 2013 году мигрировал на node.js и soap)
* Airbnb

!SLIDE left
## Проекты, использующие Ruby
* SoundCloud (часть сервисов в последствии переписана на Go)
* Heroku
* AviaSales
* Head Hunter
* КупиКупон
* Wheely
* kupibilet
* Apple для некоторых своих сервисов

!SLIDE
# Вопросы? Троллинг?
### TO BE CONTINUED...
### Пишите мне в твиттер [@lisovskyvlad](https://twitter.com/lisovskyvlad)
