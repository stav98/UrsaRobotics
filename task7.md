---
layout: default
---
<div style="text-align: justify;">
 <H1>Προγραμματισμός ελεγκτή</H1>
 <center>
  <a href="{{ "/assets/images/programing1.jpg" | relative_url }}" onclick="return hs.expand(this)" class="highslide" target="_self">
   <img src="{{ "/assets/images/programing1_small.jpg" | relative_url }}" alt="Μεγένθυση" title="Μεγένθυση" style="float: center; margin: 5px; border: 1px solid #000000; width: 350px;">
  </a>
 </center>
 <p>Δύο μαθητές της Γ’ τάξης ασχολήθηκαν με τον προγραμματισμό του ελεγκτή. Εδώ έχουμε δύο διαφορετικούς μικροελεγκτές με ξεχωριστά προγράμματα στο καθένα. Αρχικά να αναφέρουμε τα απαραίτητα εργαλεία προγραμματισμού που πρέπει να εγκατασταθούν στο Raspberry Pi.</p>
 <h3>Arduino Nano</h3>
 <p>Για τον προγραμματισμό του Arduino θα χρειαστούμε μόνο το Arduino IDE v1.8.9 έκδοση 32bit για επεξεργαστές αρχιτεκτονικής ARM. Για να ανεβάζουμε το sketch στο Arduino Nano πρέπει να συνδέσουμε το καλώδιο USB σε μια ελεύθερη USB θύρα του Raspberry. Μετά την ολοκλήρωση των δοκιμών και της εκσφαλμάτωσης, το καλώδιο μπορεί να αποσυνδεθεί.</p>
 <p>Ο κώδικας για το Arduino βρίσκεται <a href="https://github.com/stav98/UrsaRobotics_SmartHome/blob/master/arduino/I2C_SLAVE/I2C_SLAVE.ino" target="_code">εδώ</a>.</p>
 <h3>Node-MCU ESP-8266</h3>
 <p>Για τον προγραμματισμό του Node-MCU σε Micropython, αρχικά πρέπει να σβήσουμε τον διερμηνευτή της LUA μέσα από την Flash και να εγκαταστήσουμε την Micropyton σύμφωνα με τις <a href="https://github.com/stav98/UrsaRobotics_SmartHome/blob/master/micropython/%CE%95%CE%B3%CE%BA%CE%B1%CF%84%CE%AC%CF%83%CF%84%CE%B1%CF%83%CE%B7%20micropython.pdf" target="_blank">οδηγίες</a>. Επιπλέον θα χρειαστούμε ένα text editor, εμείς χρησιμοποιήσαμε το Geany για Raspberry στο οποίο παραμετροποιήσαμε τις εντολές του μενού Build για επέκταση αρχείου .py ώστε να ανεβάζει τον κώδικα στο module Node-MCU, πατώντας π.χ. shift+F8. Επίσης για εκτύπωση μηνυμάτων και εκσφαλμάτωση θα χρειαστούμε ένα πρόγραμμα τερματικού όπως το Putty για Raspberry. Επίσης απαιτείται η Python 3.x που είναι εγκατεστημένη στο Raspberry. Η python χρησιμοποιείται από το εργαλείο ampy και το esptool τα οποία είναι γραμμένα σε Python. Και εδώ θέλουμε το καλώδιο USB να είναι συνδεμένο με το Raspberry, για το ανέβασμα του κώδικα και εκσφαλμάτωση. Μετά την ολοκλήρωση της ανάπτυξης, το καλώδιο μπορεί να αποσυνδεθεί.</p>
 <p>Αν θέλουμε να κάνουμε την ανάπτυξη από σύστημα με Windows τότε υπάρχει το EsPy το οποίο είναι ολοκληρωμένο IDE για Micro Python.</p>
 <p>Ο κώδικας της micropython έχει χωριστεί σε τέσσερα (4) αρχεία .py για ευκολότερη διαχείριση. Τα αρχεία είναι:</p>
  <ol>
   <li>Αρχείο ορισμών <a href="https://github.com/stav98/UrsaRobotics_SmartHome/blob/master/micropython/src/definitions.py" target="_code">definitions.py</a>.</li>
   <li>Αρχείο συναρτήσεων <a href="https://github.com/stav98/UrsaRobotics_SmartHome/blob/master/micropython/src/functions.py" target="_code">functions.py</a>.</li>
   <li>Έτοιμη βιβλιοθήκη με τον κώδικα ελέγχου του αισθητήρα πίεσης, υγρασίας και θερμοκρασίας <a href="https://github.com/stav98/UrsaRobotics_SmartHome/blob/master/micropython/src/bme280.py" target="_code">bme280.py</a>.</li>
   <li>Αρχείο με τον κυρίως κώδικα <a href="https://github.com/stav98/UrsaRobotics_SmartHome/blob/master/micropython/src/main.py" target="_code">main.py</a>.</li>
  </ol>
 <p>Επίσης υπαρχει το αρχείο upload το οποίο πρέπει να το κάνουμε εκτελέσιμο +x και ανεβάζει τον κώδικα στο Node-MCU</p>
 {% highlight bash %}
  #!/bin/sh
  FILESIZE=$(stat -c%s "$1")
  echo ==== Uploading to board file $1 with size $FILESIZE bytes. ====
  ampy -p /dev/ttyUSB0 put $1 $2
  echo 'OK'
  exit 0
 {% endhighlight %}
 <p>Και πρέπει στο geany από το μενού 'Κατασκευή (Build)' - 'Ρύθμιση εντολών κατασκευής' να προσθέσουμε τις εντολές με την κόκκινη επισήμανση.</p>
 <center>
  <a href="{{ "/assets/images/geany_config.png" | relative_url }}" onclick="return hs.expand(this)" class="highslide" target="_self">
   <img src="{{ "/assets/images/geany_config_small.png" | relative_url }}" alt="Μεγένθυση" title="Μεγένθυση" style="float: center; margin: 5px; border: 1px solid #000000; width: 350px;">
  </a>
 </center>
 <p>Μέσα στο main.py υπάρχει ο κώδικας σύνδεσης με το WiFi. Εμείς κάναμε τις δοκιμές με στατικές διευθύνσεις IP και σύνδεση του ESP8266 ως Station. Αυτό μπορεί να συνδεθεί σε οποιοδήποτε Access Point το οποίο είναι συνδεδεμένο με το οικιακό LAN.</p>
{% highlight python linenos %}
#--------------------------------------------------------------------------------
#Αρχικοποίηση WiFi για STATION
#--------------------------------------------------------------------------------
sta_if = network.WLAN(network.STA_IF)
ap_if = network.WLAN(network.AP_IF)
ap_if.active(False)
if not sta_if.isconnected():
    print('Connect to WiFi as client ...')
    sta_if.active(True)
    sta_if.connect('YOUR SSID', 'YOUR WPA2 KEY')
    while not sta_if.isconnected():
        pass
#Αν το βάλω έχω στατική IP, αλλιώς δυναμική
sta_if.ifconfig(('192.168.42.121','255.255.255.0','192.168.42.5','192.168.42.5'))
df.hostIP = sta_if.ifconfig()
print('[Setup IP address:', df.hostIP[0], ']')
{% endhighlight %}
 <p>Βέβαια υπάρχει και η δυνατότητα να λειτουργήσει και ως AP, αρκεί να βγάλουμε εκτός λειτουργίας των παραπάνω κώδικα βάζοντας στην αρχή και το τέλος ''', και να χρησιμοποιήσουμε τον παρακάτω.</p>
{% highlight python linenos %}
#--------------------------------------------------------------------------------
#Αρχικοποίηση WiFi για AP
#--------------------------------------------------------------------------------
network.phy_mode(1) #3Mbps για 1=b και 8-10Mbps για 2=g. Μέτρηση με iperf από σταθμό σε σταθμό
print('[Set phy mode to 802.11b :',network.phy_mode())
sta_if = network.WLAN(network.STA_IF)
sta_if.active(False) #Σε περίπτωση που είναι active το station mode και το τραβάει στο κανάλι του router
ap_if = network.WLAN(network.AP_IF)
ap_if.active(True)
#ap_if.config(essid=df.ESSID, authmode=network.AUTH_WPA_WPA2_PSK, password="abweweweweewcdef1", channel=13)
ap_if.config(essid=df.ESSID, authmode=network.AUTH_OPEN, password="", channel=df.CHANNEL)
#print(ap_if.status())
if ap_if.active():
    # Query params one by one
    print('[Set wifi in AP mode with ESSID:', ap_if.config('essid'), ']')
    print('[Set channel no:', ap_if.config('channel'), ']')
#Αν το βάλω έχω στατική IP, αλλιώς δυναμική
ap_if.ifconfig(('192.168.51.100','255.255.255.0','192.168.51.10','192.168.51.10'))
df.hostIP = ap_if.ifconfig()
print('[Setup IP address:', df.hostIP[0], ']')</span>
{% endhighlight %}


 <a href="./index.html">Αρχική</a>
</div>
