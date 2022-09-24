# WIZNET CODE FOR LED
# Wifi Controlled Led Code
Code to be implemented on Wiznet Pico
```
import time
import network
import uasyncio as asyncio
from machine import Pin

# Hardware definitions
pin = Pin(25, Pin.OUT, value=0)

# Configure your WiFi SSID and password
ssid = '////id////'
password = '////password////'

check_interval_sec = 0.25

wlan = network.WLAN(network.STA_IF)


# The following HTML defines the webpage that is served
html = """<!DOCTYPE html><html>
<head><meta name="viewport" content="width=device-width, initial-scale=1">
<link rel="icon" href="data:,">
<style>html { font-family: Helvetica; display: inline-block; margin: 0px auto; text-align: center;}
.button { background-color: #4CAF50; border: 2px solid #000000;; color: white; padding: 15px 32px; text-align: center; text-decoration: none; display: inline-block; font-size: 16px; margin: 4px 2px; cursor: pointer; }
.buttonRed { background-color: #d11d53; border: 2px solid #000000;; color: white; padding: 15px 32px; text-align: center; text-decoration: none; display: inline-block; font-size: 16px; margin: 4px 2px; cursor: pointer; }
text-decoration: none; font-size: 30px; margin: 2px; cursor: pointer;}
</style></head>
<body><center><h1>DEMO</h1></center><br><br>
<form><center>
<center> <button class="button" name="LED" value="ON" type="submit">LED ON</button>
<br><br>
<center> <button class="buttonRed" name="LED" value="OFF" type="submit">LED OFF</button>
<br><br>
<center> <button class="button" name="DOOR" value="DOWN" type="submit">Door DOWN</button></center>
</center></form>
<br><br>
<br><br>
<p>Last command issued was %s<p></body></html>
"""

def blink_led(frequency = 0.5, num_blinks = 3):
    for _ in range(num_blinks):
        led.on()
        time.sleep(frequency)
        led.off()
        time.sleep(frequency)

def control_door(cmd):
    if cmd == 'on':
        pin.on()
        
    if cmd == 'off':
        pin.off()
        
        
async def connect_to_wifi():
    wlan.active(True)
    wlan.config(pm = 0xa11140)  # Diable powersave mode
    wlan.connect(ssid, password)

    # Wait for connect or fail
    max_wait = 10
    while max_wait > 0:
        if wlan.status() < 0 or wlan.status() >= 3:
            break
        max_wait -= 1
        print('waiting for connection...')
        time.sleep(1)

    # Handle connection error
    if wlan.status() != 3:
        blink_led(0.1, 10)
        raise RuntimeError('WiFi connection failed')
    else:
        blink_led(0.5, 2)
        print('connected')
        status = wlan.ifconfig()
        print('ip = ' + status[0])


async def serve_client(reader, writer):
    print("Client connected")
    request_line = await reader.readline()
    print("Request:", request_line)
    # We are not interested in HTTP request headers, skip them
    while await reader.readline() != b"\r\n":
        pass
    
    # find() valid garage-door commands within the request
    request = str(request_line)
    cmd_up = request.find('LED=ON')
    cmd_down = request.find('DOOR=DOWN')
    cmd_stop = request.find('LED=OFF')
    print ('LED=ON => ' + str(cmd_on)) # show where the commands were found (-1 means not found)
    print ('LED=OFF => ' + str(cmd_off))

    stateis = "" # Keeps track of the last command issued
    
    # Carry out a command if it is found (found at index: 8)
    if cmd_stop == 8:
        stateis = "Led : OFF"
        print(stateis)
        control_door('stop')
        
    elif cmd_up == 8:
        stateis = "Led : ON"
        print(stateis)
        control_door('on')
    
    response = html % stateis
    writer.write('HTTP/1.0 200 OK\r\nContent-type: text/html\r\n\r\n')
    writer.write(response)

    await writer.drain()
    await writer.wait_closed()


async def main():
    print('Connecting to WiFi...')
    asyncio.create_task(connect_to_wifi())

    print('Setting up webserver...')
    asyncio.create_task(asyncio.start_server(serve_client, "0.0.0.0", 80))

    while True:
        await asyncio.sleep(check_interval_sec)


try:
    asyncio.run(main())
finally:
    asyncio.new_event_loop()
```
