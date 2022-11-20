﻿# Android Interview Session
  
## Intro.Расскажи о себе, чем занимаешься
Привет. Ищем отличного крутого сеньор разработчика. Нам понравилось твое резюме.
Для начала расскажи о своем опыте в андройд разработке и конкретно то, чем ты занимаешься на последнем месте работы. 

- С каким технологическим стеком работал?
- Что входит в лидские обязанности.

### План собеса

Мы построим собеседование из нескольких секции.
- язык Kotlin. Java в ключевых аспектах как о Software Engineer в принципе.
- Андройд
- Архитектура 
- Дизайн задачка.

## OS Broad
Давай начнем с общих вопрос касательно самого Андройда. Что знаешь про Android Runtime
(среда исполнения Android, виртуальная машина?)
- Что такое Dalvik и ART
https://t.me/AndroidSobes/159
- чем отличается JVM от DVM
- полностью ли попадают библиотеки в итоговый апк ,если нет то за счет чего(shrinking)?
-  Во что компилируется ваш код
- Какие изменения произошли с этими средами исполнения за последние годы




## Kotlin.  
- какой опыт с kotlin?
- расскажи 3 своих любимых фичи kotlin,
#### Extension функции.
- Какая цена их использования,как они работают? 
- За счет чего такой функционал появляется?Какие предположения.
Модифицировать не можешь,наследоваться тоже. Как ты такое создавал бы в Java. Как мы можем добавить доп метод,утилитку к библиотечке? Утилитка Площади к rectangle. 
- а где могут объявляться extension и какие у них области видимости? (это обьявление верхнего уровня и у него нету protected.) 
#### Null safety.
- Можно ли в Kotlin все равно получить Null Pointer.Как обеспечить безопасность вызова Java кода из Kotlin кода.
#### Data классы
- для чего служат и какие возможности есть по сравнению с обычным классом? какие методы появляются? equals, hashcode, toString,copy.
- какие требования для создания data класса.(хотя бы 1 параметр. в первичный конструктор)
- мультидекларации(destructuring declarations,позволяют распаковать единое составное значение и использовать его для инициализации нескольких переменных) и функции component
#### Делегаты
- в чем особенность делегатов свойств?
- 
### Коллекции
- Что вы обычно используете (ArrayList или LinkedList) для adapter ? Почему? Как происходит вставка в середину конец списка
- Предложите эффективный алгоритм удаления нескольких рядом стоящих элементов из середины списка, реализуемого ArrayList.
-  Является ли List в Kotlin immutable-коллекцией?
- Как устроена hashmap и как можно потерять элемент в hashmap? (пример кода)
- Роль equals и hashCode в HashMap?
- Какая оценка временной сложности выборки элемента из HashMap? Гарантирует ли HashMap указанную сложность выборки элемента?
- Как и когда происходит увеличение количества корзин в HashMap?
- В каком случае может быть потерян элемент в HashMap?
- Почему нельзя использовать byte[] в качестве ключа в HashMap?

### Структуры
- корень иерархии классов в kotlin и отличие от object и какие методы доступны. тип отсутствующего значения Unit,Nothing(не завершается)
- data классы : зачем и как работает деконструкция?(компоненты)
- система типов в котлин : Чем any отличается от object? есть в ли котлине примитивные типы?
- модификаторы open,final,abstract в kotlin и их отличия от Java
 - модификаторы видимости : в котлин по дефолту public, а в Java пакет,internal только в kotlin, в котлин можно обьявить модификатор private к обьявлениям верхнего уровня.(видны только в файле где определены)
 - High order function . Что такое функции высшего порядка.
 (функции,которые приномают другие функции в аргументах  и/или возвращают их)
 Пример,list.filter{x>0}
 -  
``` java 
    fun main() {
    (0..5).map{ if (it==2) error("!!!") else it } .forEach{ println(it) }
    }
 ```
- локальный и нелокальный возврат значения из функции,цикла
- inline, no-inline
- reified , есть ли в java схожая функциональность
почему нет?

- 
### Coroutines

- виды диспатчеров и можно ли создать свой диспатчер
- в чем отличие coroutineContext от Job,что еще входит в coroutineContext
- Что такое Structured concurrency
- отменяется ли парент джоб при падении дочерней? всегда?
 #### Создание дочерней корутины
Давайте посмотрим, как связь между корутинами реализована под капотом. Для этого подробно разберем процесс создания и запуска дочерней корутины внутри родительской. Этот процесс состоит из следующих этапов:
1. **создание контекста дочерней корутины**  
2. создание джоба дочерней корутины  
3. **создание связи с родительской корутиной**  
4. запуск дочерней корутины (создание Continuation и его отправка в диспетчер)

- Критическая секция в корутинах.
на самом деле вызов suspend запрещен внутри synchronized 
поток бросает корутину,и идет выполнять другую, пока корутина не разблокируется, при этом освобождая критическую секцию
**как в котлине сделать крит. секцию?**


#### Создание связи с родительской корутиной
Job дочерней корутины достает Job родителя (из newContext), вызывает его метод attachChild и передает туда себя. Родитель создает объект ChildHandleNode, и не только оставляет его себе, но и отправляет его же обратно в дочерний Job, как результат вызова метода attachChild.

Этот объект и является связью. Он хранится в обоих джобах - родительском и дочернем. Для родителя это способ узнать, что есть незавершенные дочерние корутины. А дочерней он нужен, чтобы разорвать связь, когда работа завершена.

### OS specific
- **Что такое Looper?**

## Дизайн задача

- Design задачу: требуется засетить вью в активити, по клику на кнопку "push me", отсчитывается 5 секунд и текст "hello world" поменяется на "goodbuy world".верстка дана, нужно сделать примерный псевдокод
- Пишем код для uber. Моно репа или микрорепа и какие критерии выбора?




 ## Блок вопросов по Java.  
- в чем отличие внутренних и вложенных классов.
- порядок инициализации полей
- базовый класс Object
- модификатор final
- вложенные и внутренние классы https://habr.com/ru/post/439648/ 
- Equals and hashcode

- Допустим мы правильно определили метод `equals` в нашем классе, а метод `hashCode` решили оставить как он есть в классе `Object`. Что будет? 
-Тогда с точки зрения метода `equals` два объекта будут логически равны, в то время как с точки зрения метода `hashCode` они не будут иметь ничего общего. И, таким образом, помещая некий объект в хэш-таблицу, мы рискуем не получить его обратно по ключу.  
Например, так:
``` java 
Map<Point, String> m =  new  HashMap<>(); 
m.put(new  Point(1,  1), “Point  A”); 
// pointName == null
  String pointName = m.get(new  Point(1,  1));
```
``` java
 

```
## Многопоточность. 
- как можно задать поток в Java
- что такое race condition и как его избежать.
- счетчик значения в многопоточной среде : какими средствами JVM мы можем гарантировать
- потокобезопасные коллекции и как устроены?ConcurrentHashMap.
- deadlock - livecoding
- ввиды ссылок в Java
- как работает сборка мусора

## Android.  
- основные компоненты андройд
- **Может ли приложение быть запущено в нескольких процессах?**
https://t.me/AndroidSobes/4
- **Приоритеты процессов**
https://t.me/AndroidSobes/5
- **Activity: Как пережить поворот экрана?**
https://t.me/AndroidSobes/8
- **Нужно ли думать о сохранении состояния, если приложение поддерживает только портретную ориентацию?**
- https://t.me/AndroidSobes/9
- стыдные вопросы про ЖЦ
#### Components
- **Что такое и для чего используется BroadcastReceiver?**
- **Какие способы регистрации BroadcastReceiver вы знаете? Чем они отличаются?**
- **Что такое AIDL?**

#### Lifecycle
- **В каком случае onDestroy вызовется без onPause и onStop?** https://t.me/AndroidSobes/291
- 
### Фрагмент
- ЖЦ https://t.me/AndroidSobes/18, отличие от активити,onAttach, onDetach.
- Зачем такие специфичные callbacks.
- Могут ли не вызываться onCreate() и onDestroy()
- Как можем сохранять данные при пересоздании фрагмента? структуры из безнес логики?viewmodel,retain.
- **Метод FragmentManager.commit() – синхронный или нет?**
https://t.me/AndroidSobes/15
- **Что такое Activity State Loss Exception? Для чего нужен commitAllowingStateLoss()? (1/2)** https://t.me/AndroidSobes/15
- жизненный цикл фрагмента elye: чем ЖЦ фрагмента отличается от ЖЦ активити,гарантируется ли onStart у фрагмента после onStart  
- как фрагмент и viewmodel переживают смену конфигураций(какие есть виды смены)
- Как ViewModel переживает пересоздание фрагмента?
- Для чего нужен метод Fragment.setRetainInstance()?
https://t.me/AndroidSobes/193
- setRetainInstance() может быть использован только на фрагментах, не добавленных в backstack. Почему?
-  **Является ли ViewModel заменой onSaveInstanceState()?** , переживает ли viewmodel смерть процесса
и как обеспечивается сохранение стейта viewmodel при смене конфигурации
https://t.me/AndroidSobes/207
- commit allowStateLoss
- **Как объединить несколько LiveData?** https://t.me/AndroidSobes/200
- **Какие трансформации возможны на LiveData?** https://t.me/AndroidSobes/199

- Что такое контест и чем отличаются контексты? 
**Чем отличается activity Context от application Context?**
https://t.me/AndroidSobes/21

### Jetpack
- **В чем разница между Data Binding и View Binding библиотеками?** (https://t.me/AndroidSobes/186).
- repeatOnLifecycle vs launchWhenStarted
*Prefer collecting flows using the `repeatOnLifecycle` API instead of collecting inside the `launchWhenX` APIs. As the latter APIs suspend the coroutine instead of cancelling it when the `Lifecycle` is `STOPPED`, upstream flows are kept active in the background, potentially emitting new items and wasting resources.*

### Другое

 - **Что такое Parcelable?** https://t.me/AndroidSobes/109

- платформозависимые коллекции? где и когда
**Что такое SparseArray?**
https://t.me/AndroidSobes/107
https://t.me/AndroidSobes/97
https://proandroiddev.com/all-you-need-to-know-about-arraymap-sparsearray-49759c2ecbf9
  

  
## Архитектура.
- SOLID.Примеры из Kotlin
https://medium.com/the-android-caf%C3%A9/solid-principles-the-kotlin-way-ff717c0d60da
=> Java Singleton implementation: Double check locking vs private static field. а есть ли в котлине реализация ,а потокозависимая? а какой порядок инициализации гарантируется?
- люди делают большой отчет целый день и в конце рабочего дня нажимают кнопку загрузить и отчет(1 большой файл) начинает загружаться,интернет не быстрый , отчеты весят гигабайты, начинают грузить , кладут телефон в карман и все.
Требования: декаомпозировать задачу для меня джуна , ты лид. на какие моменты обратить внимание.Android 5.0. Уточнения welcome. battery optimizedб проблемы , ограничения. Система не любит большие файлы
- Смоделировать архитектуру того, как бы следил за интернетом в приложении.  
https://gist.github.com/esh1n/78c5b840fb8d738c29d8f0995b67d454#file-i-internetconnectionobserver-java

## Задачки на Алгоритмы
- Реверс односвязного списка
https://www.baeldung.com/java-reverse-linked-list


> Written with [StackEdit](https://stackedit.io/).