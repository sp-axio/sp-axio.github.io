---
layout: post
title:  "How to use RIOT-OS on Axio-Builder"
date:   2017-05-08 11:50:47 +0900
categories: jekyll update
---



1. Download the RIOT-OS source code from the [sp-axio github page](https://github.com/sp-axio/RIOT).

2. Go to the example directory you want to run on the Axio-Builder.

3. Compile with BOARD value as shown below.
```
$ BOARD=axio-builder-ms500 make
```

4. After signing the generated executable file, upload it to the Axio-Builder with the following command.
(Specify the serial-port of the Axio-builder board as the PORT value.)
```
$ BOARD=axio-builder-ms500 make flash PORT=/dev/ttyUSB0
```
If the upload process is successful, you will see the following message.
At this time, press the reset button of Axio-Builder.
```
### Flashing axio-builder-ms500 ###
example.bin.sig has been created.
Please reset the board.
```
After the procedure is completed, press the reset button again.
```
.....................
Download Success.
Please reset the board.
```

5. You can check the execution result at the terminal with the following command.
(Specify the serial-port of the Axio-builder board as the PORT value.)
```
$ BOARD=axio-builder-ms500 make term PORT=/dev/ttyUSB0
```

6. You can execute steps 3 ~ 5 with one command.
(Specify the serial-port of the Axio-builder board as the PORT value.)
```
$ BOARD=axio-builder-ms500 make flash term PORT=/dev/ttyUSB0
```
