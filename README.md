# flutter DevContainer

Basic empty app with DevContainer (test purposes).

## Linter & formatter

The code can be formatted with the following command:
```bash
dart fix --apply . && dart format .
```

## DevContainer

> The current configuration of `DevContainer` has currently only be tested for linux OS.  
> Also, it is quite new and some improvement could be made.

The provided `DevContainer` contains _android sdk 34_ and an already existing virtual device.  
The device should first be run from the `AVDManaged` extension (or command line)
to easily be taken by the flutter extension (otherwise, the web version will be launched).

### DevContainer - physical device

It is possible to use a physical device while running the code inside the container.  
The only (known as this point) requirements are to have the `adb` util in the host and to known the IP address of the device (and to be accessible).

#### DevContainer - physical device (host)

First, the device should be connect to the host, with, of course, the USB debug option.
It should then be listed in the devices of the host:
```bash
adb devices
```

With a result similar to:
```text
List of devices attached
<device-id>	device
```

Then, "make the device accessible through IP",
with the following command (`<port>` is generally 5555):
```bash
adb -d tcpip <port>
```

#### DevContainer - physical device (container)

Finally, in the container, connect to the device with:
```bash
adb connect <your-device-ip>:<port>
```
> It should ask for authorization in the device.


`adb devices` should give a result similar to:
```text
List of devices attached
<your-device-ip>:<port>	device
```

It can now be used by flutter as a regular android device.
If the device is sufficiently recent (Android >= 11) and/or has _WiFi debug_ capability,
the USB cable can even be removed.

> However, be aware that it connects through the network,
> so it is slower than a direct USB cable (at least for the first build).