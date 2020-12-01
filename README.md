# OLA Installation on Raspberry Pi

Start with Basic Pi Image (Full or Light)

### Updates
```
sudo apt-get update
```
```
sudo apt-get upgrade
```
```
sudo apt update
```

### Installation
```
sudo apt install ola
```

### Check the Status
```
service olad status
```
### Permissions
```
grep spi: /etc/group
```
```
sudo adduser olad spi
```
```
grep spi: /etc/group
```
### Restart
```
sudo service olad restart
```

```
sudo adduser pi olad
```

### Enabling UART

```
sudo nano /boot/config.txt
```
Change an Add
```
enable_uart=1
init_uart_clock=16000000
```

```
sudo usermod -a -G dialout pi
```

#### Enable UART Plugin
```
sudo nano /home/pi/.ola/ola-uartdmx.conf
```
Change Content to
```
enabled = true
device = /dev/ttyAMA0
/dev/ttyAMA0-break = 100
/dev/ttyAMA0-malf = 100
```
### Setup of Hardware Device
```
sudo nano /etc/init.d/olad
```
Add after line 30
```
/sbin/start-stop-daemon --start --background --make-pidfile --pidfile ✩PIDFILE --umask 0002 --chuid ✩USER --exec ✩DAEMON -- ✩DAEMON_ARGS

# set GPIO24 high (drive enable of IC1) and GPIO16 low (drive enable of IC2)
echo "24" > /sys/class/gpio/export
echo "16" > /sys/class/gpio/export
sleep 1
echo "out" > /sys/class/gpio/gpio24/direction
echo "out" > /sys/class/gpio/gpio16/direction
sleep 1
echo "1" > /sys/class/gpio/gpio24/value
echo "0" > /sys/class/gpio/gpio16/value
```



Accessible from http://xxx.xxx.xxx.xxx:9090/


##### Source:

[Dave Thwaites](https://dave.thwaites.org.uk/raspberrypi/ola-on-raspberrypi.html) ;
[Flo Edelmann](https://github.com/FloEdelmann/bachelor)

