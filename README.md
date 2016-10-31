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

Hash里的key即MQTT的Client

日志如下：

    1471869172: New connection from 10.0.2.217 on port 1883.
    1471869172: New client connected from 10.0.2.217 as abc7a4cc3534b8e56b877b4cd0c1e3a0e532615fdf91de5ac79c895011f002ff (c1, k60).
    1471869172: Updating client abc7a4cc3534b8e56b877b4cd0c1e3a0e532615fdf91de5ac79c895011f002ff to online
    1471869172: Sending CONNACK to abc7a4cc3534b8e56b877b4cd0c1e3a0e532615fdf91de5ac79c895011f002ff (0, 0)
    1471869207: Socket error on client abc7a4cc3534b8e56b877b4cd0c1e3a0e532615fdf91de5ac79c895011f002ff, disconnecting.
    1471869207: Updating client abc7a4cc3534b8e56b877b4cd0c1e3a0e532615fdf91de5ac79c895011f002ff to offline
    
## 过期时间

在传输消息中会通过获取json数据格式中expired_at字段来判断消息是否过期，如果过期的话会忽略推送消息。

    1472023902: payload: {
    	"expired_at":	1472023605,
    	"message":	"hello!"
    }
    1472023902: Expire at: 1472023605, Current timestamp: 1472023902
    1472023902: The message has already expired!

## 设备在线

设备在线会存储在Redis的mqtt键里使用HASH存储，通过HMGET来同时获取多个设备是否在线

## Redis配置

mosquitto.conf增加了redis配置

    redis_host 127.0.0.1
    redis_port 6379
    redis_auth doordu
