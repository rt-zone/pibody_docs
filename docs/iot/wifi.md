---
title: WiFi
canonical: wifi
class_name: WiFi
category: iot
interface: UART
ports: []
built_in: true
prompt_note: "WiFi connection (connect/get_time)"
---
# WiFi
The WiFi module allows connecting the PiBody to the internet over a Wi-Fi network. It provides functions to retrieve IoT-related information such as time, weather, exchange rates, and location.

---
## Basic usage

---
### `WiFi()`
To create a WiFi object, call `WiFi()`.

**Returns:**
    Return a ``WiFi`` object.
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
- `timeout (int | None)` - optional. Seconds to wait before raising an error. Default is **20s**

```python
wifi.connect("network_name", "password")
```

---
### `.get_time(gmt, formatted) -> string | dict`
With this method, you can find out the current time from the internet. You can specify the time zone as an argument; however, by default, the value is set to **+5 (Kazakhstan time)**.

**Args:**

- `gmt (int | None)` - time zone. By default, it is **+5**
- `formatted (bool | None)` - if **True**, return formatted string with time data 

```python
data = wifi.get_time(gmt=5)
print(data)
```

---
### `.get_currency(from_currency, to_currency) -> float`
Returns the exchange rate. In the arguments, you can specify which currency to convert from and to. By default, the rate is set from USD to KZT.

**Args:**

- `from_currency (string | None)` - source currency code. By default, it is **USD**
- `to_currency (string | None)` - target currency code. By default, it is **KZT**

```python
data = wifi.get_currency(from_currency="USD", to_currency="KZT")
print(data)
```

---
### `.get_temperature(city) -> float`
This method allows you to know the current outdoor temperature. You can specify the city whose weather temperature you want to know; by default, the city is set to Astana.

**Args:**

- `city (string | None)` - city name. By default, it is **Astana**

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

**Returns**:
    List of ``(ssid, rssi)`` tuples for each visible network.

```python
data = wifi.scan()
print(data)
```

---
### `.is_connected() -> bool`
Return **True** if the interface is currently connected.

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
Return the current IP address, or **None** if not connected.

```python
data = wifi.ip()
print(data)
```

---
### `.status() -> dict`
Return a summary of the current connection state.

**Returns** dict with **connected**, **ip**, **ssid**, **rssi**, and **time**.

```python
data = wifi.status()
print(data)
```
