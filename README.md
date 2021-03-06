# Содержание
  1. [Введение](#Введение)
  0. [Ценности](#Ценности)
  0. [Принципы](#Принципы)
  0. [Общие правила](#Общие-правила)
  0. [Правила разделения бизнес-логики](#Правила-разделения-бизнес-логики)
  0. [Работа с файлами](#Работа-с-файлами)
  0. [Работа с переменными](#Работа-с-переменными)
  0. [Логические переменные и методы](#Логические-переменные-и-методы)
  0. [Работа с массивами](#Работа-с-массивами)
  0. [Работа со строками](#Работа-со-строками)
  0. [Работа с неймспейсами](#Работа-с-неймспейсами)
  0. [Работа с методами](#Работа-с-методами)
  0. [Возврат результата работы метода](#Возврат-результата-работы-метода)
  0. [Работа с классами](#Работа-с-классами)
  0. [Работа с объектами](#Работа-с-объектами)
  0. [Комментирование кода](#Комментирование-кода)
  0. [Работа с исключениями](#Работа-с-исключениями)
  0. [Работа с внешним хранилищем данных](#Работа-с-внешним-хранилищем-данных)
  0. [Особенности Pull Request (PR)](#Особенности-pull-request-pr)
  0. [Работа с литералами](#Работа-с-литералами)
  0. [Работа с условиями](#Работа-с-условиями)
  0. [Использование chain-объектов](#Использование-chain-объектов)
  
## **Введение**

Этот документ содержит правила написания кода (Code Conventions). 

Code Conv — это правила, которые нужно соблюдать при написании кода. 
Мы различаем Code Style и Code Conv. Для нас Code Style — это внешний вид кода. 
То есть расстановка отступов, запятых, скобок и прочего. 
А Code Conv — это смысловое содержание кода. 
Правильные алгоритмы действий, правильные по смыслу названия переменных и методов, правильная композиция кода. 
Соблюдение Code Style легко проверяется автоматикой. 
А вот проверить соблюдение Code Conv в большинстве случаев может только человек.

Данные требования должны использоваться при написании любого кода. Они же используются как чек-лист при Code Review.

## **Ценности**
Главная цель Code Conv — сохранение низкой стоимости разработки и поддержки кода на длинной дистанции.

Основные ценности, помогающие достичь этой цели:

**Читаемость**

Код должен легко читаться, а не легко записываться. 
Это значит, что такие вещи как синтаксический сахар (если он направлен на ускорение записи, а не дальнейшего чтения кода) вредны.
Обратите внимание, что быстродействие кода не является ценностью, поэтому не самый оптимальный цикл, но удобный для понимания, будет лучше, чем быстрый, но сложный. 
В общих случаях не нужно экономить переменные, буквы для их названий, оперативную память и так далее.

**Вандалоустойчивость**

Код надо писать так, чтобы у разработчика, который с ним будет работать, 
было как можно меньше возможности внести ошибку. 
Например, покрывайте тестами не только краевые условия, но и кейсы, которые могут появиться в результате доработок кода и рефакторинга.

## **Принципы**

Принципы — это способы соблюдения описанных выше ценностей. Они чуть более детальны, содержат основные методологии разработки и подходы, которыми мы руководствуемся. 

Код должен быть:

- Понятным, явным. Явное лучше, чем неявное.
- Очень важно писать в коде комментарии, что происходит и зачем. Когда делаешь ревью кода, это очень ускоряет процесс и помогает обнаружить логические ошибки.
- Код должен быть безопасным. Нужно помнить о таких вещах как [XSS](https://ru.wikipedia.org/wiki/%D0%9C%D0%B5%D0%B6%D1%81%D0%B0%D0%B9%D1%82%D0%BE%D0%B2%D1%8B%D0%B9_%D1%81%D0%BA%D1%80%D0%B8%D0%BF%D1%82%D0%B8%D0%BD%D0%B3), [SQL injection](https://ru.wikipedia.org/wiki/%D0%92%D0%BD%D0%B5%D0%B4%D1%80%D0%B5%D0%BD%D0%B8%D0%B5_SQL-%D0%BA%D0%BE%D0%B4%D0%B0)...    
- Должен стремиться к соблюдению принципов [KISS](https://ru.wikipedia.org/wiki/KISS_(%D0%BF%D1%80%D0%B8%D0%BD%D1%86%D0%B8%D0%BF)), [SOLID](https://ru.wikipedia.org/wiki/SOLID_(%D0%BE%D0%B1%D1%8A%D0%B5%D0%BA%D1%82%D0%BD%D0%BE-%D0%BE%D1%80%D0%B8%D0%B5%D0%BD%D1%82%D0%B8%D1%80%D0%BE%D0%B2%D0%B0%D0%BD%D0%BD%D0%BE%D0%B5_%D0%BF%D1%80%D0%BE%D0%B3%D1%80%D0%B0%D0%BC%D0%BC%D0%B8%D1%80%D0%BE%D0%B2%D0%B0%D0%BD%D0%B8%D0%B5)), [DRY](https://ru.wikipedia.org/wiki/Don%E2%80%99t_repeat_yourself), [GRASP](https://ru.wikipedia.org/wiki/GRASP)
- Код должен быть таким, чтобы его можно было автоматически отрефакторить в IDE (например, Find usages и Rename в PHPStorm). То есть должен быть слинкован типизацией и PHPDoc'ами
- Последовательным. Код должен читаться сверху вниз. Читающий не должен держать что-то в уме, возвращаться назад и интерпретировать код иначе. 
- Должен иметь минимальную [цикломатическую сложность](https://ru.wikipedia.org/wiki/%D0%A6%D0%B8%D0%BA%D0%BB%D0%BE%D0%BC%D0%B0%D1%82%D0%B8%D1%87%D0%B5%D1%81%D0%BA%D0%B0%D1%8F_%D1%81%D0%BB%D0%BE%D0%B6%D0%BD%D0%BE%D1%81%D1%82%D1%8C)

## **Общие правила**

### 📖 Не должны использоваться специфичные функции какой-то версии PHP, если их можно избежать
Это упростит миграцию кода на новую версию языка. Часто в новой версии языка удаляются какие-либо функции или изменяется их работа. Чем меньше идет завязки на язык и его версию, тем лучше.

Специфичные функции всегда лучше использовать через функции-обёртки внутри проекта. Тогда в случае миграции придется исправлять одно место, а не тысячу.

Как понять, можно ли использовать встроенную в PHP функцию или нет?

- Если эта функция уже используется повсеместно в проекте, значит, её можете использовать и вы. Например, это может быть `explode`/`implode`. Если эти функции будут изменены в новой версии PHP, то в любом случае придется переделать много кода и делать это будет автоматика.

- Если эта функция не используется или используется только через обёртку в специализированном сервисе, то и вы использовать её можете только через обёртку (добавляется при необходимости).

Плохо:
```php
$result = mb_substr($string, 0, $length)."...";
```

Хорошо:
```php
$result = StringHelper::truncate($this->description, 300, '...'));
```

**[⬆ наверх](#Содержание)**

## **Правила разделения бизнес-логики**

### 📖 Сервисы/Компонент
Сервис – это класс без состояния, содержащий бизнес-логику. Данные для обработки сервис получает либо в виде параметров публичных методов, либо других сервисов. 

Сервис не может использовать в качестве источника данных глобальные переменные или окружение:

Плохо:
```php
class User {

    public function loadUsers() {
        $path = getenv('DATA_PATH'); // так нельзя!
        // ...
    }
}
```

Хорошо:
```php
class User {

    public function loadUsers($path) {
    
    }
}
```
Однако, это правило не работает, если получение данных из внешних источников — единственная бизнес-логика сервиса.

### 📖 Контроллеры
Контроллер принимает и обрабатывает запросы. Он получает параметры на вход, запрашивает данные из моделей/сервисов и возвращает представление.

### 📖 Модели
Модель — простой объект со свойствами, не содержащий никакой сложной бизнес-логики, кроме геттеров и сеттеров (сложную бизнесс логику можно выносить в компоненты). 
Геттер — метод, позволяющий получить какую-то информацию из внутреннего состояния объекта. Это не обязательно поле, как оно есть. Он может брать значения нескольких полей и делать простые манипуляции с ними (не запрашивая внешней продуктовой бизнес-логики). Сеттер — аналогично может изменять внутреннее состояние одного или нескольких полей без запросов «наружу».

Условный упрощенный пример:

```php
class Bill {
    public $id;
    public $sum;
    public $isPaid;
    public $paidDate
    // ...
    
    public function markAsPaid(\DateTime $paymentDate) {
        $this->isPaid = true;
        $this->paidDate = $paymentDate;
    }
}
```

### 📖 Представления/Шаблоны

no info yet

**[⬆ наверх](#Содержание)**

## **Работа с файлами**

no info yet

**[⬆ наверх](#Содержание)**

## **Работа с переменными**

### 📖 Название переменных должно соответствовать содержанию
Нельзя писать короткие названия, например `$c`. Нельзя назвать переменную `$day` и хранить в ней массив статистических данных за этот день.

### 📖 Часто упоминаемые объекты именуются одинаково во всем проекте

Плохо:
```php
$customer = new User();
$client = new User();
$object = new User();
```

Хорошо:
```php
$user = new User();
```

### 📖 Признак объекта добавляется к названию
Если это отфильтрованный по какому-то признаку проект, то признак добавляется к названию. Например, `$unpaidProject`.

### 📖 Переменные, отражающие свойства объекта, должны включать название объекта

Плохо:
```php
$project = new Project();
$name = $project->name;
$project = $project->name;
```

Хорошо:
```php
$project = new Project();
$projectName = $project->name;
```

### 📖 Переменные по возможности должны называться на корректном английском

Плохо:
```php
$usersStored = [];
```

Хорошо:
```php
$storedUsers = [];
```

Исключение: сгруппированные по некому признаку поля или константы. В этом случае можно использовать префикс.

```php
class ProjectInfo {
    const STATUS_READY   = 1;
    const STATUS_BLOCKED = 2;

    public $billingIsPaid;
    public $billingPaidDate;
    public $billingSum;
}
```

### 📖 Каждая переменная должна быть объявлена на новой строке

Плохо:
```php
$foo = false; $bar = true;
```

Хорошо:
```php
$foo = false;
$bar = true;
```

### 📖 Запрещено использовать результат операции присваивания

Плохо:
```php
$foo = $bar = strlen($someVar);
```

Хорошо:
```php
$bar = strlen($someVar);
$foo = $bar;
```


Плохо:
```php
$this->_callSomeFunc($bar = strlen($foo));
```

Хорошо:
```php
$bar = strlen($foo);
$this->_callSomeFunc($bar);
```


Плохо:
```php
if (strlen($foo = json_encode($bar)) > 100) {
    // ...
}
```

Хорошо:
```php
$foo = json_encode($bar);
if (strlen($foo) > 100) {
    // ...
}
```


**[⬆ наверх](#Содержание)**

## **Логические переменные и методы**

### 📖 Названия boolean методов и переменных должны содержать глагол `is`, `has` или `can`

Переменные правильно называть, описывая их содержимое, а методы — задавая вопрос. Если переменная содержит свойство объекта, следуем правилу [признак объекта добавляется к названию](#Признак-объекта-добавляется-к-названию).

Плохо:
```php
$valid = $user->valid();
```

Хорошо:
```php
$isUserValid = $user->isValid();
```


### 📖 Запрещены отрицательные логические названия

Плохо:
```php
if ($project->isInvalid()) {
    // ...
}
if ($project->isNotValid()) {
    // ...
}
if ($accessManager->isAccessDenied()) {
    // ...
}
```

Хорошо:
```php
if (!$project->isValid()) {
    // ...
}
if (!$accessManager->isAccessAllowed()) {
    // ...
}
if ($accessManager->canAccess()) {
    // ...
}
```

### 📖 Не используйте boolean переменные (флаги) как параметры функции
Флаг в качестве параметра это признак того, что функция делает больше одной вещи, нарушая [принцип единственной ответственности (Single Responsibility Principle или SRP)](https://ru.wikipedia.org/wiki/%D0%9F%D1%80%D0%B8%D0%BD%D1%86%D0%B8%D0%BF_%D0%B5%D0%B4%D0%B8%D0%BD%D1%81%D1%82%D0%B2%D0%B5%D0%BD%D0%BD%D0%BE%D0%B9_%D0%BE%D1%82%D0%B2%D0%B5%D1%82%D1%81%D1%82%D0%B2%D0%B5%D0%BD%D0%BD%D0%BE%D1%81%D1%82%D0%B8). Избавляйтесь от них, выделяя код внтури логических блоков в отдельные ветви выполнения.

Плохо:
```php
function someMethod() {
    // ...
    $projectNotificationIsEnabled = $notificationManager->isProjectNotificationEnabled($project);
    storeUser($user, $projectNotificationIsEnabled);
}

function storeUser(User $user, $isNotificationEnabled) {
    // ...
    if ($isNotificationEnabled) {
        notify('new user');
    }
}
```

Хорошо:
```php
function someMethod() {
    // ...
    storeUser($user);
    if ($notificationManager->isProjectNotificationEnabled($project)) {
        notify('new user');
    }
}

function storeUser(User $user) {
    // ...
}
```

**[⬆ наверх](#Содержание)**

## **Работа с массивами**

### 📖 Для конкатенации массивов запрещено использовать оператор `+`.
Обратите внимание, что `array_merge` все числовые ключи приводит к `int`, даже если они записаны строкой.

Плохо:
```php
return $initialData + $loadedData;
```

Хорошо:
```php
array_merge($array1, $array2)
```

### 📖 Isset проверяет наличие значения у требуемого ключа.
`isset` проверяет не ключ на его наличие, а значение этого ключа, если он есть.
Если значение null, то isset вернет false, не смотря на то что ключ присутствует.
В такой ситуации логично использовать array_key_exists


**[⬆ наверх](#Содержание)**

## **Работа со строками**

### 📖 Строки обрамляются одинарными кавычками
Двойные кавычки используются только, если:
* Внутри строки должны быть одинарные кавычки
* Внутри строки используется подстановка переменных
* Внутри строки используются спец. символы `\n`, `\r`, `\t` и т.д.

Плохо:
```php
$string = "Some string";
$string = 'Some \'string\'';
$string = "\t".'Some string'."\n";
```

Хорошо:
```php
$string = 'Some string';
$string = "Some 'string'";
$string = "\tSome string\n";
```


**[⬆ наверх](#Содержание)**


## **Работа с неймспейсами**

### 📖 Все неймспейсы должны быть подключены через `use` в начале файла. В самом коде не должно быть обратного слеша перед названием неймпейса

Плохо:
```php
$object = new \Some\Object();
```

Хорошо:
```php
use Some\Object;
$object = new Object();
```

**[⬆ наверх](#Содержание)**

## **Работа с методами**

### 📖 Должна быть использована максимально возможная типизация. Все параметры и их типы должны быть описаны в PHPDoc. Возвращаемое значение тоже.

Плохо:
```php
/**
 * @param $id
 * @param $name
 * @param $tags
 * @return mixed
 */
function storeUser($id, $name, $tags = []) {
    // ...
}
```

Хорошо:
```php
/**
 * @param int    $id
 * @param string $name
 * @param array  $tags
 * @return User
 */
function storeUser($id, $name, array $tags = []) {
    // ...
}
```

### 📖 Все возможные типы должны быть определены в PHPDoc
Наибольшую пользу это приносит при работе с массивами:

Плохо:
```php
/**
 * @param array $users
 * @param mixed $project
 * @param int   $timestamp
 * @return mixed
 */ 
public function someMethod($users, $project, $timestmap) {
    foreach ($users as $user) {
        // IDE не сможет определить тип $user
    }
    // ...
}
```

Хорошо:
```php
/**
 * @param Users[] $users
 * @param Project $project
 * @param int     $timestamp
 * @return Foo
 */
public function someMethod(array $users, Project $project, $timestmap){
    foreach ((array)$users as $user) {
        // подсказки IDE и рефакторинг работают корректно
    }
    // ...
}
```


### 📖 Название метода должно начинаться с глагола и соответствовать правилам именования переменных.

Плохо:
```php
public function items() {
    // ...
}
public function convertedDataObject(array $data) {
    // ...
}
```

Хорошо:
```php
public function getItems() {
    // ...
}
public function convertDataToObject(array $data) {
    // ...
}
```

### 📖 Методы названия, которых начинаются c `check` и `validate`, должны выбрасывать исключения и не возвращать значения

Плохо:
```php
public function validateRequestData(array $requestData) {
    if (!array_key_exists('key', $requestData)) {
        return false;
    }
    // ...
    return true;
}
```

Хорошо:
```php
public function validateRequestData(array $requestData) {
    if (!array_key_exists('key', $requestData)) {
        throw new ValidationError('Field "key" not found');
    }
    // ...
}
```

### 📖 Все методы класса по умолчанию должны быть private
Если метод используется наследниками класса, то он объявляется `protected`. Если используется сторонними классами, тогда `public`.

### 📖 Использование рекурсий допускается только в исключительном случае
Если код без рекурсии будет очень сложен для написания и понимания и при этом рекурсия гарантированно не выйдет за ограничения стека вызовов.

### 📖 Параметры в методах должны следовать в следующем порядке: обязательные → часто используемые → редко используемые
Нужно соблюдать читаемость при написании вызова.

Плохо:
```php
public function method($required, $practicallyUnused = 5, $often = [], $lessOften = null)
public function filter($value, $name, $operator) // ...$service->filter(15, "id", "=")
```

Хорошо:
```php
public function method($required, $often = [], $lessOften = null, $practicallyUnused = 5)
public function filter($name, $operator, $value) // ...$service->filter("id", "=", 15)
```

## **Возврат результата работы метода**


### 📖 Возвращаемая переменная обычно `$result`
Если у вас метод `loadUsers`, то не надо внутри метода возвращаемую переменную называть `$users`. В любом месте в методе должно быть понятно, где вы оперируете результатом, а где локальными переменными.

Плохо:
```php
function loadUsers() {
    $users = [];
    // ...
    foreach ($data as $item) {
        $users[] = new User();
    }
    return $users;
}
```

Хорошо:
```php
function loadUsers() {
    $result = [];
    // ...
    foreach ($data as $item) {
        $result[] = new User();
    }
    return $result;
}
```

### 📖 Метод должен явно отличать нормальные ситуации от исключительных
Если никакой ошибки не произошло, но отсутствует результат, то это `null` (или пустой массив), однако если все же произошла исключительная ситуация, которая не заложена системой, то должно кидаться исключение.

Плохо:
```php
function loadUsers() {
    if ($connectionError !== null) {
        return []; // потеряли ошибку, никто не узнает о проблемах с подключением
    }
    // ...
    if (count($data) === 0) {
        return [];
    }
    // ...
    return $result;
}
```

Хорошо:
```php
function loadUsers() {
    if ($connectionError !== null) {
        throw new Exception\ConnectionError();
    }
    // ...
    if (count($data) === 0) {
        return [];
    }
    // ...
    return $result;
}
```

### 📖 Метод должен придерживаться следующей структуры: Проверка параметров → Получение данных → Работа → Результат
Во время проверки параметров и получения необходимых данных метод должен возвращать соответствующее пустое значение или кидать исключение. После того как метод получил все необходимые данные и приступил к работе выход из метода крайне нежелателен. Возможны редкие исключения, облегчающие понимание и читаемость кода.

Плохо:
```php
/**
 * @return int
 */
public function someMethod() {
    $isValid = $this->_someCheck();
    if ($isValid) {
        $tmp = 0;
        $someValue = $this->_getSomeValue();
        if ($someValue > 0) {
            $tmp = $someValue;
        }
        $anotherValue = $this->_getAnotherValue();
        if ($anotherValue > 0) {
            return $tmp + $anotherValue;
        } else {
            return $someValue;
        }
    } else {
        throw new \Exception('Invalid condition');
    }
}
```

Хорошо:
```php
/**
 * @return int
 * @throws \Exception
 */
public function someMethod() {
    $result = 0;
     
    $isValid = $this->_someCheck();
    if (!$isValid) {
        throw new \Exception('Invalid condition');
    }
  
    $someValue = $this->_getSomeValue();
    if ($someValue > 0) {
        $result += $someValue;
    }
    $anotherValue = $this->_getAnotherValue();
    if ($anotherValue > 0) {
        $result += $anotherValue;
    }
    return $result;
}
```

**[⬆ наверх](#Содержание)**

## **Работа с классами**

### 📖 Трейты имеют постфикс Trait

Хорошо:
```php
trait AjaxResponseTrait {
    // ...
}
```

### 📖 Интерфейсы имеют постфикс Interface

Хорошо:
```php
interface ApplicationInterface {
    // ...
}
```

### 📖 Абстрактные классы имеют префикс Abstract

Хорошо:
```php
abstract class AbstractApplication {
    // ...
}
```

### 📖 Все свойства класса по умолчанию должны быть private
Если свойство используется наследниками класса, то оно объявляется `protected`. Если используется сторонними классами, тогда `public`.

Плохо:
```php
abstract class Loader {
    public $data = [];

    public function getData() {
        return $this->data;
    }
}
```

Хорошо:
```php
abstract class Loader {
    
    /**
     * @type array
     */
    private $cachedData = [];

    /**
     * @return array
     */
    public function getData(){
        return $this->_cachedData;
    }
}
```

### 📖 Методы и свойства в классе должны быть отсортированы по уровням видимости и по порядку использования сверху вниз
Уровни видимости: `public` -> `protected` -> `private`.

Плохо:
```php
class SomeClass {
    private $_privPropA;   
    public $pubPropA;
    protected $_protPropA;
 
    protected function _protA() {
    }
 
 
    public function pubB() {
    }
 
 
    private function _privA() {
        return $this->_protA();
    }
  
    public function pubA() {
        $this->_privA();
        return $this->pubB();
    }
}
```

Хорошо:
```php
class SomeClass {
    public $pubPropA;
    protected $_protPropA;
    private $_privPropA;
 
    public function pubA() {
        $this->_privA();
        return $this->pubB();
    }
 
    public function pubB() {
    }
 
    protected function _protA() {
    }
 
    private function _privA() {
        return $this->_protA();
    }
}
```

**[⬆ наверх](#Содержание)**

## **Работа с объектами**

### 📖 Статические вызовы можно делать только у самого класса. У экземпляра можно обращаться только к его свойствам и методам

Плохо:
```php
$type = $user::TYPE;
```

Хорошо:
```php
$type = User::TYPE;
```

**[⬆ наверх](#Содержание)**

## **Комментирование кода**

### 📖 Вынужденные хаки должны быть помечены комментариями
Лучше соблюдать одинаковый формат в рамках проекта

Хорошо:
```php
function loadUsers() {
    $result = $repository->loadUsers();
    // hack: status field was removed from storage 
    foreach ($result as $user) {
        $user->status = 'active';
    }
    // hack end
    return $result;
}
```

### 📖 Готовые алгоритмы, взятые из внешнего источника, должны быть помечены ссылкой на источник

Хорошо:
```php
/**
 * @see https://en.wikipedia.org/wiki/Quicksort
 */
function quickSort(array $arr) {
    // ...
}
```

### 📖 При разработке прототипа допустимо помечать участки кода @todo

Хорошо:
```php
function loadUsers() {
    $result = $repository->loadUsers();
    // @todo: delete the hack when field will be restored
    // hack: status field was removed from storage
    foreach ($result as $user) {
        $user->status = 'active';
    }
    // hack end
    return $result;
}
```

**[⬆ наверх](#Содержание)**

## **Работа с исключениями**
### 📖 На каждом уровне бизнес-логики (проект, компонент, библиотека) должно быть абстрактное базовое исключение

### 📖 Исключения сторонних библиотек должны быть перехвачены сразу
Далее либо обработаны, либо на их основании должно бросаться свое исключение.

Хорошо:
```php
namespace Service\Facebook;

use Exception;
use FacebookAds;

public function function requestData() {
    // ...
    try {
        $objects = $facebookAds->requestData($params);
    } catch (FacebookAds\Exception\Exception $e) {
        throw new Exception\ExternalServiceError("Facebook error: {$e->getMessage()}");
    }
    //..
}
```

### 📖 По умолчанию тексты исключений не должны показываться пользователю
Они предназначены для логирования и отладки. Текст исключения можно показать пользователю, если оно явно для этого предназначено: например, реализует интерфейс `HumanReadableInterface`.

```php
interface HumanReadableInterface {
    
    /**
     * @return string
     */
    public function getUserMessage(): string;
}

public function handleException(\Throwable $exception) {
    if ($exception instanceof HumanReadableInterface) {
        echo $exception->getUserMessage();
        return;
    }
    // ...
}
```

**[⬆ наверх](#Содержание)**

## **Работа с внешним хранилищем данных**

### 📖 Нельзя делать запросы к внешнему хранилищу внутри цикла с заведомо большим кол-вом итераций
Пример: запросы к базе в цикле. Как правило это можно оптимизировать.  

### 📖 Для каждой записи в хранилище должно быть понятна дата ее создания
То есть должна быть колонка `created_at`. Или должен быть зависимый объект (связь 1 к 1), у которого есть такая колонка. Редактируемые записи должны иметь и дату редактирования: `updated_at`.

**[⬆ наверх](#Содержание)**

## **Особенности Pull Request (PR)**
### 📖 PR должен содержать как можно меньше строк кода
Любая атомарная часть кода должна выделяться в отдельную подзадачу и отдельный PR.

### 📖 Нельзя смешивать перенос методов в другие классы и места и последующий рефакторинг между собой
Перенос методов в другие классы и места должны быть выделены в отдельный PR. Последующий рефакторинг после переноса тоже должен быть в отдельном PR.

### 📖 В случае большого PR — ответственность за долгий просмотр несет сам разработчик, сделавший такой PR
Нормальный объем кода — 0-300 строк в зависимости от его сложности. PR заглушек и архитектуры может содержать много формального кода, который легко быстро проверить. PR же конкретного метода может содержать много сложностей даже в 10 строчках. 

### 📖 Нельзя накапливать изменения в какой-то своей ветке и потом делать большой PR в master
Все что можно смержить в master без последствий (даже если это еще не готовый результат, а только заглушки или часть, но они скрыты от юзеров и никому не мешают), должен мержиться в master и PR должен создаваться в master.

### 📖 В Pull Request не должно попадать кода, не относящегося к задаче
Также не должно быть забытых комментариев, бессмысленных переносов строк и прочего "строительного мусора". Каждое изменение, которое вы предлагаете сделать в master-ветке, должно так или иначе относиться к решению поставленной вам задачи.

**[⬆ наверх](#Содержание)**

## **Работа с литералами**

### 📖 Назначение всех числовых литералов должно быть понятным из контекста
Они должны быть или вынесены в переменную или константу, или сравниваться с переменной, или передаваться на вход методу с понятной сигнатурой. В коде должен присутствовать в явном виде ответ: `за что отвечает это число и почему оно именно такое?`

Плохо:
```php
if ($object->status === 1) {
    // ...
}
```

Хорошо:
```php
if ($object->status === self::STATUS_DELETED) {
    // ...
} 
```

**[⬆ наверх](#Содержание)**

## **Работа с условиями**

### 📖 В условном операторе должно проверяться исключительно `boolean` значение

Плохо:
```php
if (count($userProjects)) {
    // ...
}
if ($project) {
    // ...
}
```

Хорошо:
```php
if ($isResponseError) { // $isResponseError = true
    // ...
}
if ($response->isError()) { // isError method returns boolean
    // ...
}
if (count($userProjects) > 0) {
    // ...
}
```

### 📖 В сравнении не boolean переменных используется строгое сравнение с приведением типа (===), автоматическое приведение и нестрогое сравнение не используются

Плохо:
```php
if ($project) {
    // ...
}
if ($request->postData('sum') == 100) {
    // ...
}
if (!$request->postData('sum')) {
    // ...
}
if (!$bill->comment) {
    // ...
}
```

Хорошо:
```php
if ($project === null) { // $project is an object
    // ...
}
if ((int)$request->postData('sum') === 100) {
    // ...
}
if ($bill->comment === '') {
    // ...
}
```

#### 📖 Не надо сравнивать `boolean` с `true`/`false`
Это нарушает запрет на бесполезный код.

Плохо:
```php
if ($bill->isPaid() == true) {
    // ...
}
if ($bill->isPaid() !== false) {
    // ...
}
if (!$bill->isPaid() === true) {
    // ...
}
if (!(!$bill->isPaid() === true)) {
    // ...
}
if ((bool)$phone->is_external === true) {
    // ...
}
```

Хорошо:
```php
if ($bill->isPaid()) {
    // ...
}
```

### 📖 Проверять переменные надо на наличие позитивного вхождения, а не отсутствие негативного
Если вам нужна строка, то проверять надо на то, что переменная является строкой. Не надо проверять на то, что она не является числом или чем-то еще. Перечислять все возможные варианты, чем переменная не должна быть, значит повышать риск ошибки и усложнять поддержку кода.

Плохо:
```php
if (!is_numeric($value) && !is_object($value)) {
    // ...
}
```

Хорошо:
```php
if (is_string($value) && $value !== '') {
    // ...
}
```

### 📖 Если вы используете встроенную функцию PHP, которая возвращает `0`, `1` и, возможно, `false`, то при возможности результат ее работы используем в условии как `bool` без дополнительных сравнений
Это не касается случая, когда вам нужно отделить два разных результата между собой, например отдельно отработать `0` и `false`.

Плохо:
```php
if (preg_match($pattern, $subject) === 1) {
    // ...
}
if (!strpos($search, $text)) {
    // ...
}
```

Хорошо:
```php
if (preg_match($pattern, $subject)) { 
    // handle success
}
if (!preg_match($pattern, $subject)) {
    // handle not success
}
if (preg_match($pattern, $subject) === false) {
    // handle error
}
if (strpos($search, $text) === false) {
    // handle not success
}
```

**[⬆ наверх](#Содержание)**

## **Использование chain-объектов**
### 📖 Метод с большим количеством необязательных параметров (А) может быть заменен chain-объектом
Метод с большим количеством необязательных параметров (А) может быть заменен chain-объектом.
В объекте конструктор принимает все обязательные параметры, а все необязательные реализуются сеттерами без глагола set (только существительное), возвращающими текущий объект (chaining методов). Метод-глагол у объекта один без параметров, он завершает использование объекта и выполняет действие, которое должен был выполнить метод А.

**Был метод:**
```php
function send($method, $url, $body = null, $headers = null, $retries = 1, $timeout = 300) {}
```

**Должен замениться на chain-объект:**
```php
public function __construct($method, $url) {
    // ...
}

public function body($body) {
    return $this;
}
// остальные методы с необязательными параметрами

public function send();
```

**Новый объект используется так:**
```php
new $sender($method, $url)->body($body)->retries(10)->timeout(25)->send();
```
