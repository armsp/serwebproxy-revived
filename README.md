# **serwebproxy-revived**

_serwebproxy 1.12 by : Lari Temmes (lari.temmes@gmail.com)_,
_Original author of serproxy 0.1.2 : Stefano Busti (sbusti@nildram.co.uk)_

* Checked only on Linux for now.
* Read README (the other file, not this REAMDME.md) to get an idea on what it is and does.
* Read the install file for your platform.
    - ```
        make
        sudo make install
      ```
* Run the default example.
* You will have to load the html - `index.html` - as `python -m http.server`

## **Deviations and tips to tackle them**

* My device is recognised as `/dev/ttyUSB0` or `/dev/tty/ACM0`
    - create udev rule for your board with a simlink

* I don't know how to write udev rules
    - [Writing udev rules](http://www.reactivated.net/writing_udev_rules.html). Its not that difficult.
    - See the example udev rule I wrote for my device - `100-armsp-temp.rules`

* I still don't get it
    - Open `config.c` file and make corresponding changes to the following block of code -
    ```c
    cfg_item_i cfg_int_defs[CFG_IEND] = {
        {"comm_baud", 9600},
        {"comm_databits", 8},
        {"comm_stopbits", 1},
        {"comm_port", 30},
        {"net_port", 5331},
        {"timeout", 300},
        {"net_protocol", 2}
    };

    cfg_item_s cfg_str_defs[CFG_SEND] = {
        {"comm_parity", "none"},
        {"serial_device", "/dev/ttyS0"},
        {"net_allow", "all"},
        {"net_deny", "none"}
    };
    ```


### **Issues**
1. Editing the `serwebproxy.cfg` file for configuration doesn't actually help.
2. Changing configuration in `config.c` makes the _http get request_ example work -  to some extent.
3. The _http get request_ doesn't seem to transfer any data to the serial port. However something does come across as it's recognized by the mcu.
<!-- # You can change the tty enumeration too from the config.c file -->
4. The messages don't seem to be going to the mcu however the flag seems to be triggered. 
Messages from microcontroller seem to be going to the browser.
