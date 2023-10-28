# ЧАВо по лексическому и синтаксическому разборам

# Что из общего почитать по теме?

##  Dick Grune, Ceriel J.H. Jacobs. Parsing Techniques: A Practical Guide (Monographs in Computer Science) 2nd ed. 2008 Edition

_Комментарий от @ksromanov._ Книгу не читал, судя по оглавлению и рекомендациям
уважаемых участников чата Compiler Development в книге представлена достаточно
хорошо структурированная информация для разработки большого класса собственных генераторов
и комбинаторов. Книгу рекомендуют глубокоуважаемые [suhr](https://t.me/zukaboo) и
[Yaroslav Schekin](https://t.me/Yaroslav_Schekin)

## Шень А. Программирование: теоремы и задачи.

_Комментарий от @ksromanov._ Приятно написанная книга для начинающих: хороший баланс между строгостью и понятностью,
в последних двух главах просто и понятно рассказывается про некоторые типы контекстно-свободных грамматик,
рассказывается про разные методы разбора, в том числе и метод рекурсивного спуска. Фактически, главы 15 и 16
самодостаточны, и являются «дешёвым и сердитым» введением в задачу грамматического (синтаксического) разбора, чтобы понимать
о чём вообще идёт речь, и как примерно всё устроено.

## A. Afroozeh, A. Izmaylova. Practical general top-down parsers

https://pure.uva.nl/ws/files/36086100/Thesis.pdf

_Комментарий от @gsvgit._
Хороший материал для желающих более глубоко изучить одно из современных направлений развития алгоритмов синтаксического анализа — обощённый нисходящий синтаксический анализ. Рассмотрены не только особенности алгоритма, но и такие вопросы как разрешение неоднозначеностей, подходы к data-dependent parsing. Работа интересна как сама по себе, так и представленными в ней ссылками на другие работы.

## Giorgios Robert Economopoulos. Generalised LR parsing algorithms

https://citeseerx.ist.psu.edu/document?repid=rep1&type=pdf&doi=2ff74ea9a0147318bc19e30c6d0f72e29a5f92c3

_Комментарий от @gsvgit._
Хороший материал для того, чтобы начать изучать различные варианты обобщённого LR разбора. От классического варианта Томиты, до современных модификаций типа BRNGLR или RIGLR.

# Что почитать по инкрементальному разбору

_пока пусто_

## Чем отличаются лексический и синтаксический разбор?

_пока пусто_

# Что использовать в качестве генераторов и комбинаторов для разных языков?

## C/C++

1. *flex/bison* — классическая связка генераторов лексического и синтаксического разбора.
Работают с форматами *lex/yacc* соответственно. Не очень удобны для разработки парсеров,
т.к. теряют типы при передаче в основную программу, но зато обладают феноменальной обратной
совместимостью — _написал и забыл_. Можно быть уверенным, что написанная и отлаженная грамматика не потребует
поддержки лет 20.

## OCaml

1. *ocamllex/Menhir* — современная свзяка генераторов лексического и синтаксического разбора.
*Menhir* по всем параметрам превосходит *ocamlyacc*, у него были несовместимые изменения, но давно.

2. *ocamllex/ocamlyacc* — классическая связка генераторов лексического и синтаксического разбора,
аналогичная *flex/bison*, не теряет типы при передаче в основную программу. Аналогично
*flex/bison* поддерживает совместимость. Увы, *ocamlyacc* устарел и постепенно меняется на *Menhir*.

Грамматику, разработанную на *ocamllex/ocamlyacc* очень легко портировать на *flex/bison*, поэтому
OCaml с этой связкой можно использовать для прототипирования.

3. *angstrom* — популярная библиотека комбинаторов.

## Haskell

1. *alex/happy* — связка генераторов, используется в GHC, поэтому можно более-менее надеяться
на стабильность.

2. *parsec* — классическая библиотека комбинаторов. Удобна и проста в использовании.
По её мотивам написаны *megaparsec*, *attoparsec* и пр.

## Универсальные генераторы

1. *ANTLR4* — универсальный инструмент: реализует и лексический, и синтаксический разбор, поддерживает очень широкий спектр возможностей по заданию грамматики и семантических действий, имеет несколько бэкендов для генерации кода на разных языках, может генерировать как традиционную CST + Visitor, так и событийно-ориентированную инфраструктуру, используется в ряде промышленных проектов. Сообщество пользователей ANTLR поддерживает довольно обширный [репозиторий грамматик](https://github.com/antlr/grammars-v4).

2. *BNFC* — универсальный инструмент схожий с *ANTLR4*, поддерживает языки Haskell, Agda, C, C++, Java, Ocaml.