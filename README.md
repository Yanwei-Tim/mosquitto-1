Eclipse Mosquitto
=================

Mosquitto is an open source implementation of a server for version 3.1 and
3.1.1 of the MQTT protocol.

See the following links for more information on MQTT:

- Community page: <http://mqtt.org/>
- MQTT v3.1.1 standard: <http://docs.oasis-open.org/mqtt/mqtt/v3.1.1/mqtt-v3.1.1.html>

Mosquitto project information is available at the following locations:

- Main homepage: <http://mosquitto.org/>
- Find existing bugs or submit a new bug: <https://github.com/eclipse/mosquitto/issues>
- Source code repository: <https://github.com/eclipse/mosquitto>

There is also a public test server available at <http://test.mosquitto.org/>

Mosquitto was written by Roger Light <roger@atchoo.org>

Master: [![Travis Build Status (master)](https://travis-ci.org/eclipse/mosquitto.svg?branch=master)](https://travis-ci.org/eclipse/mosquitto)
Develop: [![Travis Build Status (develop)](https://travis-ci.org/eclipse/mosquitto.svg?branch=develop)](https://travis-ci.org/eclipse/mosquitto)
Fixes: [![Travis Build Status (fixes)](https://travis-ci.org/eclipse/mosquitto.svg?branch=fixes)](https://travis-ci.org/eclipse/mosquitto)

## 用户上下线

增加用户上线下线状态，数据存储使用Redis，已经将hiredis整合在代码里。

配置项：
    
    redis_host 127.0.0.1
    redis_port 6379

状态存放在Redis中key为mqtt，使用Hash存储

    127.0.0.1:6379> HKEYS mqtt
    1) "test"
    127.0.0.1:6379> HKEYS mqtt
