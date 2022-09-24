# HTML CODE
## RP_MC
Code for control buttons 
```
#The following HTML defines the webpage that is served
<!DOCTYPE html><html>
<head><meta name="viewport" content="width=device-width, initial-scale=1">
<link rel="icon" href="data:,">
<style>html { font-family: Helvetica; display: inline-block; margin: 0px auto; text-align: center;}
.button { background-color: #4CAF50; border: 2px solid #000000;; color: white; padding: 15px 32px; text-align: center; text-decoration: none; display: inline-block; font-size: 16px; margin: 4px 2px; cursor: pointer; }
.buttonRed { background-color: #d11d53; border: 2px solid #000000;; color: white; padding: 15px 32px; text-align: center; text-decoration: none; display: inline-block; font-size: 16px; margin: 4px 2px; cursor: pointer; }
text-decoration: none; font-size: 30px; margin: 2px; cursor: pointer;}
</style></head>
<body><center><h1>Car Remote Controller</h1></center><br><br>
<form><center>
<center> <button class="button" name="DOOR" value="UP" type="submit">Car UP</button>
<br><br>

<center><button class="button" name="DOOR" value="DOOR" type="submit">Car LEFT</button> <button class="buttonRed" name="DOOR" value="STOP" type="submit">STOP</button><button class="button" name="DOOR" value="DOOR" type="submit">Car RIGHT</button>
<br><br>
<center> <button class="button" name="DOOR" value="DOWN" type="submit">Car DOWN</button></center>
</center></form>
<br><br>
<br><br>
<p>Last command issued was %s<p></body></html>
```
