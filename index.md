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
