## Preparing Axio Builder and ESP8266(Wi-Fi).
* ESP-01(ESP8266) connect as below.

<img src="https://cloud.githubusercontent.com/assets/24871079/25421283/0bcb21f8-2a97-11e7-9a80-09a5e0b249ec.png" width="480" height="300" />

## Preparing the mosquitto server.
* Download [mosquitto](https://github.com/eclipse/mosquitto.git) and compile.
* Edit mosquitto.conf
```
port 8883
cafile /home/USER/MQTT/mosquitto/certs/mqtt_ca.crt
certfile /home/USER/MQTT/mosquitto/certs/mqtt_srv.crt
keyfile /home/USER/MQTT/mosquitto/certs/mqtt_srv.key
tls_version tlsv1
```
* copy certs file from [sp-axio github](https://github.com/sp-axio/ArduinoMqtt_for_Axio/tree/master/test_certs).
* Run the 'mosquitto -c mosquitto.conf -v'.
* 'mosquitto' print message as below.
```
1513907710: mosquitto version 1.4.9 (build date 2017-12-19 16:42:27+0900) starting
1513907710: Config loaded from mosquitto.conf.
1513907710: Opening ipv4 listen socket on port 8883.
1513907710: Opening ipv6 listen socket on port 8883.
```

## Preparing the mosquitto pub/sub.
* Download  [ESP8266_for_Axio](https://github.com/sp-axio/ESP8266_for_Axio), [Mbedtls_ESP8266_for_Axio](https://github.com/sp-axio/Mbedtls_ESP8266_for_Axio) and [ArduinoMqtt_for_Axio](https://github.com/sp-axio/ArduinoMqtt_for_Axio) as zip file.
* In the arduino IDE, use the following procedure to add downloaded zip file.
> * menu > Sketch > Include Library > Add .zip Library... > select 'ESP8266_for_Axio.zip' and click 'OK' button.
> * Do the same thing for the 'Mbedtls_ESP8266_for_Axio.zip' and 'ArduinoMqtt_for_Axio-master.zip'.
* Open Mbedtls example as following procedure.
> * menu > File > Examples > ArduinoMqtt_for_Axio > Examples > ConnectTLSEsp8266WiFiClient

## Run the mbedtls client.
* Modify the following values in the example code to suit your development environment.
> * ssid and password of your router to mySSID/myPSK.
> * IP Address of your mosquitto server to destServer.
* If you want to test the pub and sub of mqtt with one client.
> MQTT_TOPIC_SUB = "test/" MQTT_ID "/sub" to MQTT_TOPIC_SUB = "test/" MQTT_ID "/pub"
* Verify/Compile and Upload to Axio-Builder.
* Open 'Serial Monitor' and check the result.
```
Connecting
success to establish the SSL connection
MQTT - Connect, clean-session: 1, ts: 13202
MQTT - Wait for message, type: 2, tm: 8757 ms
MQTT - recv Bytes:1/want:1/data:20
MQTT - recv Bytes:1/want:1/data:2
MQTT - read:2, result:2
MQTT - recv Bytes:2/want:2/data:0
MQTT - Process message, type: 2
MQTT - Keepalive interval: 12 sec
MQTT - Session is not present => reset subscription
MQTT - Subscribe, to: test/TEST-ID/pub, qos: 0
MQTT - Wait for message, type: 9, tm: 8553 ms
MQTT - recv Bytes:1/want:1/data:90
MQTT - recv Bytes:1/want:1/data:3
MQTT - read:3, result:3
MQTT - recv Bytes:3/want:3/data:0
MQTT - Process message, type: 9
MQTT - Subscribe ack received
MQTT - Publish, to: test/TEST-ID/pub, size: 13
MQTT - Yield for 30000 ms
MQTT - recv Bytes:1/want:1/data:30
MQTT - recv Bytes:1/want:1/data:1F
MQTT - read:1F, result:31
MQTT - recv Bytes:31/want:31/data:0
MQTT - Process message, type: 3
MQTT - Publish received, qos: 0
MQTT - Deliver message for: test/TEST-ID/pub
Message arrived: qos 0, retained 0, dup 0, packetid 9512, payload:[Hello World!]
```
> * ConnectEsp8266WiFiClient example publishes message 'Hello World!' to test/TEST-ID/pub topic.
