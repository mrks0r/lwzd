# lwzd
This is a simple daemon that connects my heatpump LWZ403 SOL to my self-made home automation infrastructure. The primary idea was to regulate the air ventilation according to detected pollution by a particulate matter sensor, e.g. from nearby combustion heating. But then it became handy for fetching various readings, too. 

This is a private project with no intentions beyond that whatsoever. It is public so I can show it to friends. It is written in Perl because that is my favourite scripting language. 

## Status of this project

It's work in progress. Adjusting the heatpump, e.g. the fans, is not implemented yet. Other parts are mostly finished, that is the state machine for communication with the heatpump, a nifty mechanism for parsing and documenting incoming datagrams, a cron-mechanism for convenience, and the code for daemonizing. 
 
Supported heatpumps are at least the LWZ/THZ 403/404 with firmware 4.39.

## Dependencies

It needs a perl interpreter and two additional perl-modules: 

* **Device::SerialPort** for serial line communication with the heatpump, 
* and **DBI** to interact with a database.

## Run it

Just run the lwzd in debugging mode to watch it working

```
./sbin/lwzd --debug
```

or install it as a background process on your system. Therefore I suggest to link ```/usr/local/sbin/lwzd``` to your ```./sbin/lwzd``` and either deploy the provided init-script or the systemd .service file.

## Hacking

Have a look at the code, and play around.

You might send additional or different commands to the heatpump. You'd just have to set a corresponding callback with a parser. See ```perldoc -f pack``` for how the templates work.

You might add some additional periodical jobs in ```@cron```, eg for storing your reading elsewhere or for polling a datasource for instructions what to send to the heatpump. The entries are called in order.

For information about the protocol, have a look on

 * the [Homepage of Robert Penz on LWZ](https://robert.penz.name/heat-pump-lwz/) for how to build a cable to connect to your LWZ, and basic communication,
 * the [FHEM-Poject](https://fhem.de) where there is a [Module for THZ-Heatpumps](https://wiki.fhem.de/wiki/Tecalor_THZ_Heatpump) which is identical in construction to the LWZ,
 * the [SmartHomeNG Project](https://www.smarthomeng.de) that also has a [Plugin for THZ](https://github.com/smarthomeNG/plugins/tree/master/thz).

