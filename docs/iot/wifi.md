---
title: WiFi
---
# WiFi
WiFi helps connect PiBody to internet via WiFi. Released functions only for several IOT needed information, lime weather, currency and etc.

---
## Basic usage

---
### `WiFi()`
To create WiFi object call `WiFi()`.

**Returns:**
    Return a class ``WiFi``.
```python
from pibody import WiFi

wifi = WiFi()
```

---
### `.connect(ssid, password, timeout) -> IfConfig`
Connect PiBody to the internet. In the method arguments, specify the network name and password.

Prints ip-address in console on successful connection.

If already connected, returns the current config immediately.

**Args:**

- `ssid (string)` - network name
- `password (string)` - network password
- `timeout (int | None)` - optional. Seconds to wait before raising an error (default 20)

```python
wifi.connect("network_name", "password")
```

---
### `.get_time(gmt, formatted)`
With this method, you can find out the current time from the internet. You can specify the time zone as an argument; however, by default, the value is set to +5 (Kazakhstan time).

**Args:**

- `gmt (int | None)` - time zone. By default is `+5`
- `formatted (bool | None)` - if `True`, return formatted string with time data 

```python
data = wifi.get_time(gmt=5)
print(data)
```

---
### `.get_currency(from_currency, to_currency)`
Returns the exchange rate. In the arguments, you can specify which currency to convert from and to. By default, the rate is set from USD to KZT.

**Args:**

- `from_currency (string | None)` - source currency code. By default is `USD`
- `to_currency (string | None)` - target currency code. By default is `KZT`

```python
data = wifi.get_currency(from_currency="USD", to_currency="KZT")
print(data)
```

---
### `.get_temperature(city)`
This method allows you to know the current outdoor temperature. You can specify the city whose weather temperature you want to know; by default, the city is set to Astana.

**Args:**

- `city (string | None)` - city name. By default is `Astana`

```python
data = wifi.get_temperature("Astana")
print(data)
```

---
### `.get_ip_info() -> dict`
Fetch public IP address and location info.

```python
data = wifi.get_ip_info()
print(data)
```

---
## Other Functions

---
### `.scan()`
Returns a list of available WiFi networks and their RSSI. RSSI is the index of signal “strength”. It is measured in negative numbers — the closer the value is to zero, the stronger the signal is considered.

```python
data = wifi.scan()
print(data)
```

---
### `.scan()`
Returns a list of available WiFi networks and their RSSI. RSSI is the index of signal “strength”. It is measured in negative numbers — the closer the value is to zero, the stronger the signal is considered.

**Returns**:
    List of ``(ssid, rssi)`` tuples for each visible network.

```python
data = wifi.scan()
print(data)
```

---
### `.is_connected() -> bool`
Return ``True`` if the interface is currently connected.

```python
data = wifi.is_connected()
print(data)
```

---
### `.disconnect()`
Disconnect from the current Wi-Fi network.

```python
wifi.disconnect()
```

---
### `.ip() -> string | None`
Return the current IP address, or ``None`` if not connected.

```python
data = wifi.ip()
print(data)
```

---
### `.status() -> dict`
Return a summary of the current connection state.

**Returns**:
    Dict with ``connected``, ``ip``, ``ssid``, ``rssi``, and ``time``.

```python
data = wifi.status()
print(data)
```
