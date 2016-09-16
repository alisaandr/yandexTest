
# HTTP
## Краткое описание
HTTP (_hyper-text transfer protocol - Протокол передачи гипертекста_) - широко распространённый протокол прикладного уровня передачи данных, изначально предназначенный для передачи гипертекстовых документов (то есть документов, которые могут содержать ссылки перехода к другим документам).
## Устройство протокола
Основой протокола является модель "клиент-сервер". 
- Клиент – приложение, которое инициирует соединение и посылает запрос (чаще всего браузер).
- Сервер – программное обеспечение, принимающее запросы от клиентов и обрабатывающее их.
![N|Solid](http://www.javatpoint.com/images/http.JPG)

Основным объектом манипуляции в HTTP является ресурс, на который указывает URI (Uniform Resource Identifier) в запросе клиента. Обычно такими ресурсами являются хранящиеся на сервере файлы, но ими могут быть логические объекты или что-то абстрактное. Особенностью протокола HTTP является возможность указать в запросе и ответе способ представления одного и того же ресурса по различным параметрам: формату, кодировке, языку и т. д. (в частности, для этого используется HTTP-заголовок). Именно благодаря возможности указания способа кодирования сообщения, клиент и сервер могут обмениваться двоичными данными, хотя данный протокол является текстовым. 

HTTP представляет собой протокол запросов-откликов. Клиент посылает на сервер `HttpRequest`. Сервер обрабатывает его и посылает клиенту в ответ `HttpResonse`.
Оба в форме Http-сообщений.
## Формат HTTP-Сообщения
Каждое HTTP-сообщение состоит из трех частей, которые передаются в указанном порядке: 

### Cтартовая строка
Cтартовая строка (англ. starting line)– определяет тип сообщения. Стартовые строки различаются для запроса и ответа. Строка запроса выглядит так: 
__``Метод URI HTTP/Версия``__ .

_Пример:_

 GET /wiki/HTTP HTTP/1.0
 
 Здесь:
- Метод (англ. Method) — название запроса, одно слово заглавными буквами (см. ниже)
- URI — определяет путь к запрашиваемому документу
- Версия (англ. Version) — пара разделённых точкой цифр.
 
Стартовая строка ответа сервера имеет следующий формат: __`HTTP/Версия КодСостояния Пояснение`__

 _Пример:_
 
HTTP/1.0 200 OK 

Здесь:

 - _Версия_ — пара разделённых точкой цифр, как в запросе;
 - _Код состояния (англ. Status Code)_ — три цифры. По коду состояния определяется дальнейшее содержимое сообщения и поведение клиента;
 - _Пояснение (англ. Reason Phrase)_ — текстовое короткое пояснение к коду ответа для пользователя. Никак не влияет на сообщение и является необязательным.

### Заголовки
 Заголовки (англ. headers) – характеризуют тело сообщения, параметры передачи и прочие сведения.
 Все заголовки разделяются на четыре основных группы:

-  _General Headers («Основные заголовки»)_ — могут включаться в любое сообщение клиента и сервера;

- _Request Headers («Заголовки запроса»)_ — используются только в запросах клиента;

- _Response Headers («Заголовки ответа»)_ — только для ответов от сервера;

- _Entity Headers («Заголовки сущности»)_ — сопровождают каждую сущность сообщения.

Именно в таком порядке рекомендуется посылать заголовки получателю.
 
 (для более подробной информации смотри [rfc2616_headers](https://tools.ietf.org/html/rfc2616#section-4.2), [rfc.rus_headers](http://novopromo.ru/http/rfc2068/26.html) )

_Пример:_

Server: Apache/2.2.11 (Win32) PHP/5.3.0

Last-Modified: Sat, 16 Jan 2010 21:16:42 GMT

Content-Type: text/plain; charset=windows-1251

Content-Language: ru

В примере выше каждая строка представляет собой один заголовок. При этом то, что находится до первого двоеточия, называется именем (англ. name), а что после неё — значением (англ. value).

### Тело сообщения
Тело сообщения (англ. message body) – непосредственно данные сообщения, отделенные от заголовков пустой строкой. Заголовки и тело сообщения могут отсутствовать, но стартовая строка является обязательным элементом, так как указывает на тип запроса/ответа [rfc2616_body](https://tools.ietf.org/html/rfc2616#section-4.3), [rfc.rus_body](http://novopromo.ru/http/rfc2068/27.html)

## Методы 
Процедура, выполняемая над ресурсом (get, put, head, post, delete, trace и т.д.) Регистр учитывается. Каждый сервер обязан поддерживать как минимум методы `GET` и `HEAD`.
Метод `GET` позволяет получать любую информацию (в форме объекта), идентифицированную запрашиваемым URI (Request-URI).
Метод `HEAD` идентичен `GET`, за исключением того, что сервер НЕ ДОЛЖЕН возвращать в ответе тело сообщения. Этот метод может использоваться для получения метаинформации об объекте запроса без непосредственной пересылки тела объекта.
Метод `POST` предназначен для запроса, при котором веб-сервер принимает данные, заключенные в тело сообщения, для хранения. Он часто используется для загрузки файла или представления заполненной веб-формы.
 Подробнее: [rfc2616](https://tools.ietf.org/html/rfc2616#section-5.1.1), [rus.rfc2616](https://novopromo.ru/http/rfc2068/32.html)

## Коды ошибок
Код состояния является частью первой строки ответа сервера. Он представляет собой целое число из трёх цифр. Первая цифра указывает на класс состояния. Клиент узнаёт по коду ответа о результатах его запроса и определяет, какие действия ему предпринимать дальше. Набор кодов состояния является стандартом, и они описаны в соответствующих документах RFC
### 1xx	Информационный. 
Информирование о процессе передачи.
Сами сообщения от сервера содержат только стартовую строку ответа и, если требуется, несколько специфичных для ответа полей заголовка. 
### 2xx Успех.
Информирование о случаях успешного принятия и обработки запроса клиента. В зависимости от статуса, сервер может ещё передать заголовки и тело сообщения.
### 3xx	Перенаправление. 
Сообщает клиенту, что для успешного выполнения операции необходимо сделать другой запрос (как правило по другому URI). Из данного класса пять кодов 301, 302, 303, 305 и 307 относятся непосредственно к перенаправлениям (редирект). Адрес, по которому клиенту следует произвести запрос, сервер указывает в заголовке Location. При этом допускается использование фрагментов в целевом URI.
### 4xx	Ошибка клиента.
Указание ошибок со стороны клиента. При использовании всех методов, кроме HEAD, сервер должен вернуть в теле сообщения гипертекстовое пояснение для пользователя.
### 5xx	Ошибка сервера.

Информирование о случаях неудачного выполнения операции по вине сервера. Для всех ситуаций, кроме использования метода HEAD, сервер должен включать в тело сообщения объяснение, которое клиент отобразит пользователю.
## Пример диалога HTTP

_Запрос клиента:_

GET /wiki/страница HTTP/1.1

Host: ru.wikipedia.org

User-Agent: Mozilla/5.0 (X11; U; Linux i686; ru; rv:1.9b5) Gecko/2008050509 Firefox/3.0b5
Accept: text/html

Connection: close

(пустая строка)  

_Ответ сервера:_

HTTP/1.1 200 OK 

Date: Wed, 11 Feb 2009 11:20:59 GMT

Server: Apache

X-Powered-By: PHP/5.2.4-2ubuntu5wm1

Last-Modified: Wed, 11 Feb 2009 11:20:59 GMT

Content-Language: ru

Content-Type: text/html; charset=utf-8

Content-Length: 1234

Connection: close

(пустая строка)

(далее следует запрошенная страница в HTML)
 
## Источники

 <http://novopromo.ru/http/rfc2068/>
 
  <https://tools.ietf.org/html/rfc2616>
  
 <https://ru.wikipedia.org/wiki/HTTP>
 
 <http://solod.zz.mu/edu/inet/11_HTTP/11_http_lect.pdf>
 
