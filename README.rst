uwsgitop
========

``uwsgitop`` is a top-like command that uses the uWSGI Stats Server to
monitor your uwsgi application.

To use uWSGI Stat Server simply use the ``stats`` option followed by
a valid socket address, for example::

    uwsgi --module myapp --socket :3030 --stats /tmp/stats.socket

To start monitoring your application with ``uwsgitop`` call it with
the socket address like so::

    uwsgitop /tmp/stats.socket

If you want the stats served over HTTP you will need to add
the ``stats-http`` option in uWSGI::

    uwsgi --module myapp --http :3030 --stats :3031 --stats-http

You'll now need to call uwsgitop as::

    uwsgitop http://127.0.0.1:3031


You can also use the `UWSGITOP_ADDRESS` environment variable to define a default socket or address and run uwsgitop without any arguments like this::

    export UWSGITOP_ADDRESS="/tmp/stats.socket"
    uwsgitop


Installation
------------

::

    pip install uwsgitop

Usage
-----

To display async core statistics (e.g. when using gevent) or to switch between
core statistics display mode, press ``a``. To refresh the screen super fast press ``f``,
and to quit, press ``q``.

+--------+---------------------------------------------------------------+
| Field  |  Description                                                  |
+========+===============================================================+
| WID    | Worker ID                                                     |
+--------+---------------------------------------------------------------+
| %      | Worker usage                                                  |
+--------+---------------------------------------------------------------+
| PID    | Worker PID                                                    |
+--------+---------------------------------------------------------------+
| REQ    | Number of requests the worker executed since last (re)spawn   |
+--------+---------------------------------------------------------------+
| RPS    | Requests per second                                           |
+--------+---------------------------------------------------------------+
| EXC    | Exceptions                                                    |
+--------+---------------------------------------------------------------+
| SIG    | Managed uwsgi signals                                         |
+--------+---------------------------------------------------------------+
| STATUS | Worker is busy or free to use?                                |
+--------+---------------------------------------------------------------+
| AVG    | Average request time                                          |
+--------+---------------------------------------------------------------+
| RSS    | Worker RSS (Resident Set Size, see linux memory management)   |
+--------+---------------------------------------------------------------+
| VSZ    | Worker VSZ (Virtual Memory Size, see linux memory management) |
+--------+---------------------------------------------------------------+
| TX     | How much data was transmitted by the worker                   |
+--------+---------------------------------------------------------------+
| ReSpwn | Respawn count                                                 |
+--------+---------------------------------------------------------------+
| HC     | Harakiri count                                                |
+--------+---------------------------------------------------------------+
| RunT   | How long the worker has been running                          |
+--------+---------------------------------------------------------------+
|LastSpwn| Last spawn time                                               |
+--------+---------------------------------------------------------------+

Colors
------

Lines would be displayed in different colors:

- default console text color, if the worker is idle
- ``green``, if the worker is busy
- ``magenta``, if the worker is in ``cheap`` mode
- ``yellow``, if the worker is handling an uwsgi signal
- ``blue``, if the worker is ``suspended``


Remember to enable ``memory-report`` in your uwsgi configuration to see how
much memory resources your uwsgi processes are consuming.

Further Reading
---------------

For more info on uWSGI Stats Server see https://uwsgi-docs.readthedocs.io/en/latest/StatsServer.html
