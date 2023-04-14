# [Співбесіда з Go. 200+ запитань для Junior, Middle, Senior](https://dou.ua/lenta/articles/interview-questions-go-developer/)

## Junior

### Software engineering

<details>
<summary><b>1. Які бувають області пам’яті програми? У чому їхні особливості та відмінності?</b></summary>

Стек (Stack) це область пам'яті, де зберігаються локальні змінні та адреси повернення функцій. Стек працює за принципом (Last-In-First-Out, LIFO).

Куча (Heap) це область пам'яті, в якій зберігаються об'єкти, створені в програмі. Куча має динамічний розмір та керується операторами виділення та звільнення пам'яті.

Глобальна область (Global Area) це область пам'яті, в якій зберігаються глобальні змінні та функції.

Статична область (Static Area) це область пам'яті, в якій зберігаються статичні змінні та функції.

Константна область (Constant Area) це захищена від змін область пам'яті, в якій зберігаються константи, такі як рядки та числа.
</details>

<details>
<summary><b>2. Розкажіть, що ви знаєте про HTTP-протокол, які складові частини запиту? Які статус-коди знаєте, які групи можна виділити?</b></summary>

HTTP — це протокол передачі даних прикладного рівня, який використовується для передачі веб-сторінок, зображень, відео та інших даних між веб-клієнтом та веб-сервером.

HTTP-запит складається з трьох основних частин:

1. стартовий рядок ("Метод URI HTTP/Версія" для запиту та "HTTP/Версія Статус-код Опис" для відповіді);  
2. заголовки;  
3. тіло повідомлення, що містить дані запиту, запитаний ресурс або опис проблеми, якщо запит не виконано.

Коди статусу:

- 1хх — інформаційний: запит прийнятий, продовжуй процес.
- 2хх — успіх: дія була успішно передана, зрозуміла, та прийнята.
- 3хх — перенаправлення: наступні дії мають бути успішно виконані для реалізації запиту.
- 4хх — помилка клієнта: запит містить синтаксичні помилки або не може бути виконаний.
- 5хх — помилка сервера: сервер не зміг виконати правильно сформований запит.

Найбільш поширені статуси:

- 200 OK — запит виконано успішно.
- 301 Moved Permanently — ресурс переміщено.
- 403 Forbidden — доступ до запитаного ресурсу заборонений.
- 404 Not Found — ресурс не знайдений.
- 503 Service Unavailable — сервіс недоступний.

Методи:

OPTIONS — Повертає методи HTTP, які підтримуються сервером. Цей метод може служити для визначення можливостей вебсервера.

GET — Запитує вміст вказаного ресурсу. Запитаний ресурс може приймати параметри, які передаються в рядку URI. Згідно зі стандартом HTTP, запити типу GET вважаються ідемпотентними — багаторазове повторення одного і того ж запиту GET повинне приводити до однакових результатів (за умови, що сам ресурс не змінився за час між запитами). Це дозволяє кешувати відповіді на запити GET. Якщо назва ресурсу не вказана (у URI наявні лише схема та доменне ім'я), то вебсервер повертає індекс директорії вебсервера.

HEAD — Аналогічний методу GET, за винятком того, що у відповіді сервера відсутнє тіло. Це корисно для витягання метаінформації, заданої в заголовках відповіді, без пересилання всього вмісту. Зокрема, клієнт чи проксі, перевіривши заголовок Last-Modified: (останній час модифікації), таким чином може переконатися, що сторінка на сервері не змінилася від часу попереднього запиту.

POST — Передає призначені для користувача дані (наприклад, з HTML-форми) заданому ресурсу. Наприклад, в блогах відвідувачі зазвичай можуть вводити свої коментарі до записів в HTML-форму, після чого вони передаються серверу методом POST, і він поміщає їх на сторінку. При цьому передані дані (у прикладі з блогами — текст коментаря) включаються в Тіло запиту (Request body). На відміну від методу GET, метод POST не вважається ідемпотентним, тобто багаторазове повторення одних і тих же запитів POST може повертати різні результати (наприклад, після кожного відправлення коментаря з'являтиметься одна копія цього коментаря).

PUT — Завантажує вказаний ресурс на сервер.

PATCH — Завантажує певну частину ресурсу на сервер.

DELETE — Видаляє вказаний ресурс.

TRACE — Повертає отриманий запит так, що клієнт може побачити, що проміжні сервери додають або змінюють в запиті.

CONNECT — Для використання разом з проксі-серверами, які можуть динамічно перемикатися в тунельний режим SSL.
</details>

<details>
<summary><b>3. Назвіть та опишіть будь-який патерн програмування (на ваш вибір). Коли його доцільно використовувати та чому?</b></summary>
</details>

<details>
<summary><b>4. Що таке процеси та потоки в операційній системі? Опишіть їхній взаємозв’язок у контексті виконання програми.</b></summary>
Процес — завантажена в пам'ять і готова до виконання програма, яка складається з коду, даних і інших системних ресурсів, таких як відкриті файли та канали.

Потік (thread) — базовий об'єкт, якому операційна система розподіляє час центрального процесора.

Виконання процесу починається зі стартового потоку. Надалі він може породжувати інші потоки. Ресурси процесу доступні всім його потокам. Кожен потік використовує структуру даних, для збереження контексту виконання, у той час, коли в нього віднімається процесор. У контекст входять регістри процесора, перемінні оточення, стеки ядра і користувача. Усі потоки одного процесу спільно використовують його віртуальний адресний простір.

Процесорний час розподіляється по черзі між потоками, а не між процесами.
</details>

<details>
<summary><b>5. Що таке шаблон проєктування (design pattern)?</b></summary>
Шаблони проєктування — ефективні способи вирішення задач проєктування програмного забезпечення. Об'єктно-орієнтований шаблон найчастіше є зразком вирішення проблеми і відображає відношення між класами та об'єктами, без вказівки на те, як буде зрештою реалізоване це відношення.

Типи шаблонів «Банди чотирьох» (Gang of Four, GOF, Erich Gamma, Richard Helm, Ralph Johnson, John Vlissides), опубліковані в 1991 р. в книзі «Design Patterns — Elements of Reusable Object-Oriented Software»

- Основні шаблони
- Твірні шаблони
  - Абстрактна фабрика (Abstract Factory)
  - Будівник (Builder)
  - Впровадження залежностей (Dependency Injection)
  - Одинак (Singleton)
  - Прототип (Prototype)
  - Фабричний метод (Factory Method)
  - Отримання ресурсу є ініціалізація (Resource Acquisition Is Initialization)
  - Відкладена ініціалізація (Lazy initialization)
  - Пул об'єктів (Object pool)
  - Мультитон (Multiton pattern)
- Структурні шаблони
  - Адаптер (Adapter)
  - Декоратор (Decorator)
  - Замісник (Proxy)
  - Компонувальник (Composite)
  - Міст (Bridge)
  - Легковаговик (Flyweight)
  - Фасад (Facade)
  - Модуль
- Шаблони поведінки
  - Відвідувач (Visitor)
  - Інтерпретатор (Interpreter)
  - Ітератор (Iterator)
  - Команда (Command)
  - Ланцюг обов'язків (Chain of Responsibility)
  - Посередник (Mediator)
  - Точка входу (Front controller)
  - Спостерігач (Observer)
  - Стан (State)
  - Стратегія (Strategy)
  - Знімок (Memento)
  - Шаблонний метод (Template Method)
- Шаблони паралельних операцій (конкурентного програмування)
  - Активний об'єкт (Active Object)
  - Ігнорування (Balking pattern)
  - Бар'єр (Barrier)
  - Подвійна перевірка замка (Double-checked locking)
  - Охороняєме призупинення (Guarded suspension)
  - Ведучий/підпорядкований (Leaders/followers pattern)
  - Об'єкт-монітор (Monitor Object)
  - Реактор (Reactor pattern)
  - Багато читачів/один дописувач (Readers write lock pattern)
  - Планувальник (Scheduler pattern)
  - Пул потоків (Thread pool pattern)
  - Зберігання в межах потоку (Thread-local storage)
</details>

<details>
<summary><b>6. Які знаєте алгоритми сортування?</b></summary>
</details>

<details>
<summary><b>7. Що таке Big-O notation?</b></summary>
</details>

<details>
<summary><b>8. Які відмінності між unit-тестом та інтеграційним тестом?</b></summary>
</details>

<details>
<summary><b>9. Що таке mock і для чого його використовують?</b></summary>
</details>

<details>
<summary><b>10. Що таке SDLC? Які етапи й навіщо вони потрібні?</b></summary>
</details>

<details>
<summary><b>11. Що таке SOLID?</b></summary>
</details>

<details>
<summary><b>12. Що таке MVC?</b></summary>
</details>

<details>
<summary><b>13. Що таке DBMS? Яка різниця між СУБД та базою даних?</b></summary>
</details>

<details>
<summary><b>14. Які бувають типи баз даних?</b></summary>
</details>

<details>
<summary><b>15. Що таке Docker?</b></summary>
</details>


### Бази даних

<details>
<summary><b>16. Опишіть ACID-властивості реляційних баз даних.</b></summary>
</details>
<details>
<summary><b>17. Є таблиця в реляційній БД зі 100 тисячами рядків. SELECT-запит з такої таблиці триває час *t*. Як зміниться час запиту, якщо кількість рядків буде один мільйон? Які є варіанти, залежно від запиту/таблиці?</b></summary>
</details>
<details>
<summary><b>18. Для чого використовують індекси в базах даних і завдяки чому (яким структурам даних) вони працюють?</b></summary>
</details>
<details>
<summary><b>19. З якими NoSQL-базами даних працювали? Які їхні переваги над реляційними базами?</b></summary>
</details>

### Go

<details>
<summary><b>20. На вашу думку, у чому перевага Go перед іншими мовами?</b></summary>
</details>
<details>
<summary><b>21. Що таке горутини й навіщо вони?</b></summary>
</details>
<details>
<summary><b>22. Що таке GOROOT і GOPATH?</b></summary>
</details>
<details>
<summary><b>23. Які типи даних використовуються в Go?</b></summary>
</details>
<details>
<summary><b>24. Що робить функція ``init()``? Наведіть приклади, де її варто використовувати. Наведіть приклади, коли варто уникати.</b></summary>
</details>
<details>
<summary><b>25. Поясніть різницю між помилкою і панікою.</b></summary>
</details>
<details>
<summary><b>26. Як відловлювати паніки?</b></summary>
</details>
<details>
<summary><b>27. Як отримати теперішній час?</b></summary>
</details>
<details>
<summary><b>28. Що таке iota?</b></summary>
</details>
<details>
<summary><b>29. Яка різниця між слайсом і масивом?</b></summary>
</details>
<details>
<summary><b>30. З яких частин складається змінна типу slice?</b></summary>
</details>
<details>
<summary><b>31. Як працює append?</b></summary>
</details>
<details>
<summary><b>32. Що таке len і capacity в slice?</b></summary>
</details>
<details>
<summary><b>33. Що таке пакети?</b></summary>
</details>
<details>
<summary><b>34. Що таке інтерфейси і як вони працюють?</b></summary>
</details>
<details>
<summary><b>35. Для чого потрібні інтерфейси в Golang?</b></summary>
</details>
<details>
<summary><b>36. Що таке тип даних string?</b></summary>
</details>
<details>
<summary><b>37. Чим відрізняються лапки в Go (подвійні, одинарні, зворотні): ``""``,``''``, ``\`\```?</b></summary>
</details>
<details>
<summary><b>38. Що таке rune?</b></summary>
</details>
<details>
<summary><b>39. Чи може змінна типу string приймати nil-значення?</b></summary>
</details>
<details>
<summary><b>40. Чи можна повернути з функції кілька значень?</b></summary>
</details>
<details>
<summary><b>41. Що відбувається під час конкатенації рядків?</b></summary>
</details>
<details>
<summary><b>42. Як ефективно склеїти кілька рядків?</b></summary>
</details>
<details>
<summary><b>43. Як записати в файл?</b></summary>
</details>
<details>
<summary><b>44. Що таке структура?</b></summary>
</details>
<details>
<summary><b>45. Що буде, якщо викликати ``log.Fatal``?</b></summary>
</details>
<details>
<summary><b>46. Поясніть різницю між конкурентністю і паралельністю?</b></summary>
</details>
<details>
<summary><b>47. Як оголосити відкладений виклик?</b></summary>
</details>
<details>
<summary><b>48. Що таке канал? Які типи каналів ви знаєте? Для чого вони потрібні?</b></summary>
</details>
<details>
<summary><b>49. Яка різниця між буферизованим і небуферизованим каналами?</b></summary>
</details>
<details>
<summary><b>50. Що буде, якщо читати із закритого каналу? Що буде, якщо писати у закритий канал?</b></summary>
</details>
<details>
<summary><b>51. Як перевірити, що змінна типу map має збережене значення для певного ключа?</b></summary>
</details>
<details>
<summary><b>52. Які стандартні env-змінні в Go?</b></summary>
</details>
<details>
<summary><b>53. Яка різниця між value & pointer receiver?</b></summary>
</details>
<details>
<summary><b>54. Як зробити type assertion?</b></summary>
</details>
<details>
<summary><b>55. Як та навіщо робити type assertion?</b></summary>
</details>
<details>
<summary><b>56. Як написати benchmark?</b></summary>
</details>
<details>
<summary><b>57. В якому порядку виконуються кейси в select?</b></summary>
</details>

### Практичні завдання

<details>
<summary><b>58. Реалізувати алгоритм двійкового пошуку елемента у слайсі.</b></summary>
</details>
<details>
<summary><b>59. Є [код](https://play.golang.org/p/a-JIesxdCQ7). Що виведеться на екран? Що потрібно зробити, щоб побачити запропонований висновок Foo1 і Foo2?</b></summary>
</details>
<details>
<summary><b>60. Є [код](https://play.golang.org/p/6CiZvQp7r3t). Що виведеться на екран? Як вивести на екран літери?</b></summary>
</details>
<details>
<summary><b>61. Поміняйте місцями значення двох змінних без тимчасової допоміжної змінної.</b></summary>
</details>
<details>
<summary><b>62. Оберніть slice у зворотному порядку.</b></summary>
</details>
<details>
<summary><b>63. Перемістіть усі zero values у кінець масиву.</b></summary>
</details>

## Middle

### Software engineering

<details>
<summary><b>1. У чому переваги та недоліки використання protobuf у порівнянні з JSON?</b></summary>
</details>
<details>
<summary><b>2. Назвіть деякі з принципів 12-factor-app. Для чого використовують graceful shutdown?</b></summary>
</details>
<details>
<summary><b>3. Що таке dependency injection? А dependency inversion?</b></summary>
</details>
<details>
<summary><b>4. У вас є ssh-доступ на Linux-сервер, де запущено вебсервер. З сервером періодично відбуваються незаплановані рестарти. Сервер записує логи у файли (розмір лог-файлу &gt; 10 Mb). Які *nix-команди ви можете використати, щоб проаналізувати проблему?</b></summary>
</details>
<details>
<summary><b>5. Як працює TLS handshake?</b></summary>
</details>
<details>
<summary><b>6. Яка різниця між TCP & UDP? В якій ситуації UPD краще?</b></summary>
</details>
<details>
<summary><b>7. Розкажіть у найдрібніших деталях, що відбувається, коли клієнт посилає запит на сервер, а сервер цей запит отримує.</b></summary>
</details>
<details>
<summary><b>8. Що таке Clean Architecture? Наведіть приклад.</b></summary>
</details>
<details>
<summary><b>9. Що таке оперативна пам’ять?</b></summary>
</details>
<details>
<summary><b>10. Як різниця між stack & heap?</b></summary>
</details>
<details>
<summary><b>11. Для чого потрібні Docker та Kubernetes?</b></summary>
</details>
<details>
<summary><b>12. Розкажіть про абстракції Kubernetes, з якими працювали?</b></summary>
</details>
<details>
<summary><b>13. Що таке Pod? Як він влаштований?</b></summary>
</details>
<details>
<summary><b>14. Розкажіть про Data structures: stack, queue, linked list, trie, balanced tree.</b></summary>
</details>

### Бази даних

<details>
<summary><b>15. Які шляхи пошуку повільних SELECT-запитів у RDBMS? Які способи пришвидшення таких запитів?</b></summary>
</details>
<details>
<summary><b>16. Що таке нормальні форми бази даних?</b></summary>
</details>
<details>
<summary><b>17. Що таке індекси? Які їхні недоліки?</b></summary>
</details>
<details>
<summary><b>18. Які структури даних можуть використовуватися в індексах баз даних? Як вони працюють?</b></summary>
</details>
<details>
<summary><b>19. Яка різниця між foreign & primary key?</b></summary>
</details>
<details>
<summary><b>20. Поняття міграції у контексті баз даних. У чому переваги підходу з міграціями?</b></summary>
</details>
<details>
<summary><b>21. Що таке реплікація даних? Які варіанти реплікації існують для баз, з якими ви працювали?</b></summary>
</details>
<details>
<summary><b>22. Яка різниця між SQL і NoSQL?</b></summary>
</details>
<details>
<summary><b>23. Які типи NoSQL баз даних ви знаєте? Наведіть приклади. Яка між ними різниця?</b></summary>
</details>
<details>
<summary><b>24. Що таке колонкова БД? Переваги та недоліки.</b></summary>
</details>
<details>
<summary><b>25. Що таке документоорієнтована БД? Переваги та недоліки.</b></summary>
</details>
<details>
<summary><b>26. Розкажіть про роботу з key-value базами даних (бажано з власного досвіду).</b></summary>
</details>
<details>
<summary><b>27. З якими типами даних Redis у вас є практичний досвід? Назвіть приклади, коли їх доцільно використовувати.</b></summary>
</details>

### Go

<details>
<summary><b>28. Якими бібліотеками Go ви користувалися для доступу до RDBMS? Які у них позитивні та негативні сторони?</b></summary>
</details>
<details>
<summary><b>29. Для чого використовують Context? Які є варіанти скасовування контекстів?</b></summary>
</details>
<details>
<summary><b>30. Якими способами можна виключити (приховати) поля структури при JSON-серіалізації?</b></summary>
</details>
<details>
<summary><b>31. Назвіть примітиви пакету sync стандартної бібліотеки. Яке призначення та приклади застосування ``sync.WaitGroup``?</b></summary>
</details>
<details>
<summary><b>32. Яка різниця між Mutex та RWMutex?</b></summary>
</details>
<details>
<summary><b>33. Які є способи зупинити N горутин, запущених одночасно (наприклад, worker pool)?</b></summary>
</details>
<details>
<summary><b>34. Що таке замикання функцій?</b></summary>
</details>
<details>
<summary><b>35. Поясніть різницю між switch і select?</b></summary>
</details>
<details>
<summary><b>36. Які є способи дістати дані з JSON?</b></summary>
</details>
<details>
<summary><b>37. Як у Go реалізовані конструкції циклів?</b></summary>
</details>
<details>
<summary><b>38. Як влаштований тип map?</b></summary>
</details>
<details>
<summary><b>39. Який порядок перебору map?</b></summary>
</details>
<details>
<summary><b>40. Що таке серіалізація? Де вона застосовується?</b></summary>
</details>
<details>
<summary><b>41. Чи можна використовувати nil для ініціалізації змінної?</b></summary>
</details>
<details>
<summary><b>42. Чи можна задати місткість map? Чи можна отримати місткість map?</b></summary>
</details>
<details>
<summary><b>43. Як дізнатися кількість символів у рядку?</b></summary>
</details>
<details>
<summary><b>44. Що таке кодогенерація і для чого вона потрібна?</b></summary>
</details>
<details>
<summary><b>45. Чим відрізняється goroutine від OS thread?</b></summary>
</details>
<details>
<summary><b>46. Як і для чого використовують ``io.Reader`` і ``io.Writer``?</b></summary>
</details>
<details>
<summary><b>47. Як перетворити ``[]io.ReadWriter`` на ``[]io.Reader``?</b></summary>
</details>
<details>
<summary><b>48. Як вказати головній горутині очікувати завершення роботи всіх робочих горутин?</b></summary>
</details>
<details>
<summary><b>49. Чи завжди буде швидше передача Pointer як аргументу функції?</b></summary>
</details>
<details>
<summary><b>50. Що таке варіативна змінна функції? Як працювати з цією змінною?</b></summary>
</details>
<details>
<summary><b>51. Як працювати з пакетом internal?</b></summary>
</details>
<details>
<summary><b>52. Як працює імпорт через крапочку і чому це погана практика?</b></summary>
</details>
<details>
<summary><b>53. Як працює імпорт через підкреслення?</b></summary>
</details>
<details>
<summary><b>54. Що таке ``defer()``?</b></summary>
</details>
<details>
<summary><b>55. Як працювати з goto?</b></summary>
</details>
<details>
<summary><b>56. Що таке ``reflect.DeepEqual()`` і ``reflect.TypeOf()``?</b></summary>
</details>
<details>
<summary><b>57. Як розпарсити час?</b></summary>
</details>
<details>
<summary><b>58. Як порівняти дві дати?</b></summary>
</details>
<details>
<summary><b>59. Що таке вказівник і як з ним працювати?</b></summary>
</details>
<details>
<summary><b>60. Як перевірити, чи змінна імплементує інтерфейс?</b></summary>
</details>
<details>
<summary><b>61. Що таке embedding?</b></summary>
</details>
<details>
<summary><b>62. Опишіть кроки процесу тестування.</b></summary>
</details>
<details>
<summary><b>63. Як писати тести? Що таке табличні тести?</b></summary>
</details>
<details>
<summary><b>64. Що таке memory leak? Які є способи його виявлення? Як його позбутися?</b></summary>
</details>
<details>
<summary><b>65. Що таке race condition? Які є способи його виявлення? Як його позбутися?</b></summary>
</details>

### Практичні завдання

<details>
<summary><b>67. Реалізувати перевірку на слова на анаграму. Написати тест і бенчмарк. Оцінити складність розробленого алгоритму.</b></summary>
</details>
<details>
<summary><b>68. Є [код](https://play.golang.org/p/-3o2gp3enIG). Що виведеться на екран? Чому?</b></summary>
</details>
<details>
<summary><b>69. Є [код](https://play.golang.org/p/qwC_nJNFdEy). Чи можна передбачити, що виведеться на екран? Чому?</b></summary>
</details>
<details>
<summary><b>70. Реалізуйте Stack (LIFO).</b></summary>
</details>
<details>
<summary><b>71. Реалізуйте linked list.</b></summary>
</details>
<details>
<summary><b>72. Задача про суму підмножини (Subset Sum Problem). Дано: множина позитивних цілих чисел і значення sum. Визначте, чи існує підмножина даної множини з сумою, яка дорівнює значенню sum.  </b></summary>
</details>
``Input: set [] = { 3 , 34 , 4 , 12 , 5 , 2 }, sum = 9``  
``Output: True``

## Senior

### Software engineering

<details>
<summary><b>1. Що таке процес і потік? Як вони пов’язані між собою? Чи мають різні процеси чи потоки доступу до однієї області пам’яті?</b></summary>
</details>
<details>
<summary><b>2. Які інструменти зазвичай використовують для збору метрик і логів? Як працює Prometheus?</b></summary>
</details>
<details>
<summary><b>3. Як працює docker під капотом?</b></summary>
</details>
<details>
<summary><b>4. Як працює load balancer під капотом?</b></summary>
</details>
<details>
<summary><b>5. Для чого потрібні черги?</b></summary>
</details>
<details>
<summary><b>6. Що таке CQRS?</b></summary>
</details>
<details>
<summary><b>7. Які архітектури програмного забезпечення ви знаєте?</b></summary>
</details>
<details>
<summary><b>8. Яка різниця між мікросервісами та монолітом? Які є переваги та недоліки?</b></summary>
</details>
<details>
<summary><b>9. Як побудувати міжсервісну транзакцію?</b></summary>
</details>
<details>
<summary><b>10. Що таке розподілені транзакції? Як реалізувати?</b></summary>
</details>
<details>
<summary><b>11. Які проблеми вирішує патерн Saga?</b></summary>
</details>
<details>
<summary><b>12. Як реалізувати аутентифікацію в мікросервісній архітектурі?</b></summary>
</details>
<details>
<summary><b>13. Що таке Event Sourcing?</b></summary>
</details>
<details>
<summary><b>14. Сформулюйте CAP-теорему.</b></summary>
</details>
<details>
<summary><b>15. Розкажіть про Raft Consensus Algorithm.</b></summary>
</details>
<details>
<summary><b>16. У чому різниця між імперативною і декларативною парадигмою програмування? Наведіть приклади мов.</b></summary>
</details>

### Бази даних

<details>
<summary><b>17. Для чого потрібні графові бази даних?</b></summary>
</details>
<details>
<summary><b>18. Якщо точкові дані прив’язані до часу, які бази даних варто використовувати для збереження цих даних?</b></summary>
</details>
<details>
<summary><b>19. Що таке Materialized View? У чому відмінність від звичайного View?</b></summary>
</details>
<details>
<summary><b>20. Що таке ACID? Прокоментуйте, як ACID реалізований в PostgreSQL.</b></summary>
</details>
<details>
<summary><b>21. Яка різниця між BASE та ACID?</b></summary>
</details>
<details>
<summary><b>22. Назвіть рівні ізоляції транзакцій?</b></summary>
</details>
<details>
<summary><b>23. Досвід оптимізації бази. Які інструменти використовували?</b></summary>
</details>
<details>
<summary><b>24. Що таке шардинг? Які види є?</b></summary>
</details>
<details>
<summary><b>25. Як працює master-slave реплікація?</b></summary>
</details>
<details>
<summary><b>26. Як працюють індекси? Як вибрати індекси в таблицях?</b></summary>
</details>
<details>
<summary><b>27. Розкажіть про optimistic та pessimistic locking.</b></summary>
</details>

### Go

<details>
<summary><b>28. За що відповідає змінна GOMAXPROCS? Яке її значення за замовчуванням?</b></summary>
</details>
<details>
<summary><b>29. Хто відповідає за планування горутин? Розкажіть про алгоритм роботи планувальника. Навіщо він потрібен, якщо вже й так є системні потоки?</b></summary>
</details>
<details>
<summary><b>30. Розкажіть про алгоритм роботи garbage collector. Mark and sweep, Reference counting та оптимізації алгоритму в мові Go. Що таке stop the world?</b></summary>
</details>
<details>
<summary><b>31. Які види багатозадачності ви знаєте? Який з них використовують у Go?</b></summary>
</details>
<details>
<summary><b>32. Для чого потрібна рефлексія? У чому різниця між рефлексією та кодогенерацією?</b></summary>
</details>
<details>
<summary><b>33. У чому різниця між value та reference типом? Назвіть декілька прикладів у мові Go.</b></summary>
</details>
<details>
<summary><b>34. Як зупинити горутину?</b></summary>
</details>
<details>
<summary><b>35. Як в Go реалізується спадкування?</b></summary>
</details>
<details>
<summary><b>36. Що таке lvalue і rvalue?</b></summary>
</details>
<details>
<summary><b>37. Яке у slice zero value?</b></summary>
</details>
<details>
<summary><b>38. Як вбудувати стандартний профайлер у свій застосунок?</b></summary>
</details>
<details>
<summary><b>39. Що таке map-reduce? Як його реалізувати в Go?</b></summary>
</details>
<details>
<summary><b>40. Як в Go працює префіксний інкремент/декремент?</b></summary>
</details>
<details>
<summary><b>41. Що буде, якщо перетворити в JSON-об’єкт, структура якого містить поля з малими літерами в назвах?</b></summary>
</details>
<details>
<summary><b>42. Як перервати for/switch або for/select?</b></summary>
</details>
<details>
<summary><b>43. Як можна оптимізувати виконання великої кількості послідовних операцій читання або запису?</b></summary>
</details>
<details>
<summary><b>44. Чи можна викликати метод у вказівника (pointer) на структуру, якщо він дорівнює nil?</b></summary>
</details>
<details>
<summary><b>45. Що буде при спробі запису в закритий канал?</b></summary>
</details>
<details>
<summary><b>46. Що таке взаємне блокування (deadlock)?</b></summary>
</details>
<details>
<summary><b>47. У чому особливість nil-каналів?</b></summary>
</details>
<details>
<summary><b>48. У яких випадках варто використовувати м’ютекси, а не канали, та навпаки?</b></summary>
</details>
<details>
<summary><b>49. Що таке білд-теги?</b></summary>
</details>
<details>
<summary><b>50. Як реалізувати LRU cache?</b></summary>
</details>
<details>
<summary><b>51. Що таке SSA-представлення?</b></summary>
</details>
<details>
<summary><b>52. Що ви знаєте про роботу з плагінами на Go?</b></summary>
</details>
<details>
<summary><b>53. Що таке аліаси типів?</b></summary>
</details>
<details>
<summary><b>54. Що таке падінги в структурах і на що вони впливають?</b></summary>
</details>
<details>
<summary><b>55. Що таке escape-аналіз?</b></summary>
</details>
<details>
<summary><b>56. Яка різниця між стеком і купою?</b></summary>
</details>
<details>
<summary><b>57. Що нам дає пакет unsafe?</b></summary>
</details>
<details>
<summary><b>58. Чи можна змінити певний символ у рядку? А за допомогою пакета unsafe?</b></summary>
</details>
<details>
<summary><b>59. Як працювати з рефлексією і що ми можемо з нею зробити?</b></summary>
</details>
<details>
<summary><b>60. Як під капотом виглядають слайси й мапи?</b></summary>
</details>
<details>
<summary><b>61. Як працювати з ``copy()``?</b></summary>
</details>
<details>
<summary><b>62. Як працювати з sync.Pool і [sync.Map](https://l.facebook.com/l.php?u=http%3A%2F%2Fsync.Map%2F%3Ffbclid%3DIwAR0IRDk_3BRFwVxRcE0uuDiDriYFAB-vmhE1kPgf-v4pAu-WVSAqs3RquBg&h=AT2u89KulT3y4yWcAEDgMTLEKrYnDjKrjAxEX6ycQ9dAB2T-Bzbvcph3lXrW-c1-uwxT24bKzuE1Y_rBdl3iNBYs8njT3uo8X3QJ4nqGhY7md3GKjNHy0lxtdvjTdtZtB2FIwy_scz0)? Які підводні камені вони мають?</b></summary>
</details>
<details>
<summary><b>63. Розкажіть про канкаренсі-патерни в Go.</b></summary>
</details>
<details>
<summary><b>64. Як у Go реалізована арифметика вказівників?*</b></summary>
</details>

### Практичні завдання

<details>
<summary><b>65. Побудувати архітектуру бекенду для оренди самокатів типу Kiwi чи Bolt. Які мікросервіси будуть? Які мови та інструменти? Який клауд-провайдер? Що варто використати як інфраструктуру? Які бази даних та шини повідомлень?</b></summary>
</details>
<details>
<summary><b>66. Уявімо, що ви провідний розробник на проєкті, як би ви розподілили ролі в команді із 5 людей для найефективнішої роботи?</b></summary>
</details>
<details>
<summary><b>67. Є [код](https://play.golang.org/p/QSajZuzP-GN). Чому ``err! = nil``?</b></summary>
</details>
<details>
<summary><b>68. Вам дають ssh на сервер і просять полагодити вебзастосунок, який «впав». Інформації про сервер і сервіси немає. Які команди ви будете використовувати, щоб зібрати інформацію, знайти та усунути проблему?</b></summary>
</details>
<details>
<summary><b>69. Реалізуйте двійкову структуру даних дерева пошуку в Go.</b></summary>
</details>
<details>
<summary><b>70. Знайдіть максимальну суму шляху в трикутнику. (Подано числа у формі трикутника, починаючи з верхньої частини трикутника і рухаючись до сусідніх чисел у рядку внизу, знаходимо максимальну загальну кількість зверху вниз.)</b></summary>
</details>
