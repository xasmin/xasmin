# Simple pulseaudio sound server on rpi.

On muzyczny rpi:

```# apt-get install -y pulseaudio```

```# dd if=/dev/urandom of=/pa.cookie bs=256 count=1```
```# chown pulse /pa.cookie ```

```# vim /etc/pulse/system.pa```
```
  load-module module-native-protocol-tcp auth-cookie=/pa.cookie
```

```# vim /etc/rc.local```
```
  echo 0 >/sys/class/leds/led0/brightness
  echo 0 >/sys/class/leds/led1/brightness
  pulseaudio --system --realtime --disallow-module-loading --disallow-exit -D
```

On client:

```PULSE_SERVER=muzyczny PULSE_COOKIE=`pwd`/pa.cookie paplay --raw /dev/urandom  -d 1```
