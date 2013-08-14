# ``flap`` - утилита для прослушивания unix pipe
Утилита позволяет прослушивать данные, проходящие по пайпу в настоящий момент.
![Overview](http://share.nologin.ru/img/flap-overview600.png)

## Usage
```
Usage: flap (-s|-c) /path/to/socket.sock
        -s: server mode
        -c: client mode (read-only)
```

## Режим сервера
Если указано опция ``-s``, то программа создаёт unix-сокет по указанному пути и
принимает всё входящие подключения. Каждому подключению (клиенту) она пересылает
все данные, проходящие через пайп. Если клиент по каким-то причинам не успевает
получать данные, то часть данных может потеряться, т.к. ``flap`` намеренно не
блокирует основной поток данных. Таким образом, можно не опасаться, что медленный
клиент затормозит передачу данных.

## Режим клиента
Если указано опция ``-c``, то программа просто подключается к указанному unix-сокету
и читает из него в ``STDIN``. В настоящий момент, вместо ``flap -c``
можно использовать любую утилиту, умеющую работать в unix-сокетами, например, `nc`
или `socat`.
