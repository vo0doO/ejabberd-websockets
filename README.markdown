> Это репо не поддерживается, и большая часть кода здесь, вероятно, устарела.


# Модуль Websocket для Ejabberd

Это модуль, который добавляет поддержку веб-сокетов для XMPP-сервера [ejabberd](http://www.ejabberd.im/). Это более элегантная, современная и быстрая замена Bosh.

Это реализация [проекта XMPP Over Websocket](http://tools.ietf.org/html/draft-moffitt-xmpp-over-websocket-00), предложенного Джеком Моффиттом и Эриком Кстари. Реализация Websocket основана на этой [черновой спецификации](http://tools.ietf.org/html/draft-ietf-hybi-thewebsocketprotocol-03).

** Вам необходимо использовать подходящую версию ejabberd, так как бинарная установка поставляется со старой версией erlang. **

## Установить

### Строить
<code>./build.sh</code>

### Установить
<code>cp ebin/*.beam /path/to/ejabberd/lib/ebin/</code>

### Настроить
В разделе слушателей добавьте следующую строку:

<code>{5288, ejabberd_websocket, [{request_handlers, [{["ws-xmpp"], mod_websocket}]}]},</code>

Убедитесь, что вы также добавили эту строку в <code>Modules</code>.

<code>{mod_websocket, []}</code>


## Применение

Просто подключитесь к веб-сокету с помощью API вашего браузера и отправьте через него свой XMPP-трафик.

Возможно, вам будет удобно использовать напрямую [Strophejs](https://github.com/metajack/strophejs), так как это полная библиотека XMPP на Javascript. Однако на данный момент вам придется использовать [эту ветку](https://github.com/superfeedr/strophejs), поскольку она добавляет поддержку веб-сокета в качестве базового протокола (вместо Bosh).

Чтобы настроить соединение:
<код>
// WS_SERVICE должен быть http://host.tld:5288/ws-xmpp в зависимости от выбранной вами конфигурации.
соединение = новый Strophe.Connection({протокол: новый Strophe.Websocket(WS_SERVICE)});
</код>


## СДЕЛАТЬ

Самое «срочное» — это предусмотреть в этом модуле резервные механизмы. Например, поддержка [socket.io](http://socket.io/) была бы замечательной, поскольку у erlang есть своя [реализация](https://github.com/yrashk/socket.io-erlang). Не стесняйтесь раскошелиться и сделать его лучше!

## Спасибо

При поддержке [Superfeedr](http://superfeedr.com). Особая благодарность [Натану](http://unclenaynay.com/) за его прекрасную работу, [Джеку](http://metajack.im/) за помощь.

## Лицензия

См. [License.markdown](./ejabberd-websockets/blob/master/License.markdown).
