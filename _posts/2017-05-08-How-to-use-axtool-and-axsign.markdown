---
layout: post
title:  "How to use Axtool and Axsign"
date:   2017-05-08 15:20:47 +0900
categories: jekyll update
---


## Axtool
Axtool is a program for communicating with the Axio Builder on the host.
The usage of axtool is as follows.
```
Syntax
axtool [option] SERIAL_PORT
Option:
  -b FILE : Update the second bootloader.
  -f FILE : Update the firmware.
  -i FILE : Install a certificate.
  -d FILE : Delete a certificate. FILE is a private key.
  -s      : Second Bootloader Version.
  -v      : Axtool Version.
  -h      : Help.
```
SERIAL_PORT specifies the name of the USB COM device of the recognized board. (Ex /dev/ttyUSB0, COM3)

### Generate and use custom certificate
The authentication algorithm uses prime256v1 among the elliptic curves.
Currently, the certificate type is not supported for signature verification, but is used simply as a public key.
If the EC prime256v1 key pair does not yet exist and is for testing purposes, you can generate 'Elliptic Curve Key Pair'.
* Generate Private Key (Curve: prime256v1)

```openssl ecparam -genkey -name prime256v1 -noout -out private.pem```
* Generate Public Key

```openssl ec -in private.pem -pubout -out public.pem```

To verify that the firmware has not been forgery during Axio Builder boots, the firmware must be signed and the certificate must be installed on the board.
The certificate can only be downloaded once, and if there is a certificate on the board, it must be removed and then downloaded again.
* Remove certificate

```axtool -d private.pem [SERIAL_PORT]```
* Download certificate

```axtool -i public.pem [SERIAL_PORT]```
 

## Axsign
Firmware must be signed to install on the board.
Axsign is a program for signing firmware.

```
Syntax
usage) axsign firmware_file private_key
       axsign -v
```