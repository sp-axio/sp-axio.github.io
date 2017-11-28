## Preparing Axio Builder and ESP8266(Wi-Fi).
* ESP-01(ESP8266) connect as below.

<img src="https://cloud.githubusercontent.com/assets/24871079/25421283/0bcb21f8-2a97-11e7-9a80-09a5e0b249ec.png" width="480" height="300" />

## Preparing the mbedtls server.
* Download [mbedtls](https://github.com/ARMmbed/mbedtls.git) and compile.
* Run the 'programs/ssl/ssl_server2'.
* 'ssl_server2' print message as below.
  ```
  mbedtls.git/programs/ssl$ ./ssl_server2
  . Seeding the random number generator... ok
  . Loading the CA root certificate ... ok (0 skipped)
  . Loading the server cert. and key... ok
  . Bind on tcp://*:4433/ ... ok
  . Setting up the SSL/TLS structure... ok
  . Waiting for a remote connection ...
```

## Preparing the mbedtls client.
* Download [Mbedtls_ESP8266_for_Axio](https://github.com/sp-axio/Mbedtls_ESP8266_for_Axio.git) as zip file.
* In the arduino IDE, use the following procedure to add downloaded zip file.
> * menu > Sketch > Include Library > Add .zip Library... > select 'Mbedtls_ESP8266_for_Axio.zip' and click 'OK' button.
* Open Mbedtls example as following procedure.
> * menu > File > Examples > Mbedtls_ESP8266_for_Axio-master > Examples > Mbedtls_ESP8266_Client

## Run the mbedtls client.
* Modify the following values in the example code to suit your development environment.
> * ssid and password of your router to mySSID/myPSK.
> * IP Address of your mbedtls server to destServer.
* Verify/Compile and Upload to Axio-Builder.
* Open 'Serial Monitor' and check the result.
```
    BESP8266 Shield Present
    Mode set to station
    Connecting to SecurityPlatform
    Connected to: SecurityPlatform
    My IP: 192.168.122.14

    Press any key to connect client.

    Start Mbedtls client
    try to connect to server...
    connect success!
    SSL connect success!
    Write to SSL server..
    Read from SSL Server...
    ================== received begin =========
    HTTP/1.0 200 OK
    Content-Type: text/html

    <h2>mbed TLS Test Server</h2>
    <p>Successful connection using: TLS-ECDHE-ECDSA-WITH-AES-256-CBC-SHA</p>

    ================== received done =========
    disconnect SSL connection
```