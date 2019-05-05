---
layout: default
---
<div style="text-align: justify;">
 <H1>Αναγνώριση ομιλίας και φωνητικών εντολών</H1>
 <p>Ενώ είχαμε ξεκινήσει τον σχεδιασμό του έργου, προσπαθούσαμε να σκεφτούμε τρόπους χειρισμού των συσκευών όταν καθόμαστε στον καναπέ ή είμαστε ξαπλωμένοι, χωρίς να πρέπει να πάρουμε το κινητό ή να πάμε σε κάποιο πίνακα ελέγχου. Τότε ο Θόδωρος έριξε την ιδέα της ομιλίας, και μας φάνηκε εφικτή η υλοποίησή της. Ασχοληθήκαμε αρκετά μ’ αυτό το κομμάτι, αλλά πιστεύουμε ότι θέλει ακόμη πολλές βελτιώσεις.</p>
 <p>Στο παρακάτω σχήμα βλέπουμε τον τρόπο διασύνδεσης όλων των προγραμμάτων μέσω του πρωτοκόλλου mqtt. Στη πραγματικότητα το MQTT Message Bus είναι το σύνολο των εντολών subscribe και publish μεταξύ των προγραμμάτων και του broker.</p>
 <center>
  <a href="{{ "/assets/images/software_interconnection.png" | relative_url }}" onclick="return hs.expand(this)" class="highslide" target="_self">
   <img src="{{ "/assets/images/software_interconnection_small.png" | relative_url }}" alt="Μεγένθυση" title="Μεγένθυση" style="float: center; margin: 5px; border: 1px solid #000000; width: 400px;">
  </a>
 </center>
 <p>Από την πλευρά του hardware, πρέπει να βάλουμε μια USB κάρτα ήχου ή μια USB κάμερα με μικρόφωνο επειδή το Raspberry δεν διαθέτει συσκευή ηχογράφησης. Από την πλευρά του λογισμικού χρησιμοποιήσαμε την έτοιμη βιβλιοθήκη <a href="https://github.com/Uberi/speech_recognition" target="_blank">SpeechRecognition</a> για την online μηχανή αναγνώρισης της Google. Η βιβλιοθήκη αυτή υποστηρίζει και offline αναγνώριση φωνής με το πακέτο <a href="https://cmusphinx.github.io/wiki/" target="_blank">CMUSphinx</a>, αλλά δεν προλάβαμε να ασχοληθούμε με αυτό.</p>
 <p>Πρέπει να εγκατασταθούν τα ακόλουθα πακέτα:</p>
 <ul>
  <li><pre>sudo apt-get install libportaudio0 libportaudio2 libportaudiocpp0 portaudio19-dev</pre><br>Σε άλλα συστήματα ίσως χρειαστεί το flac: <pre>sudo apt-get install flac</pre></li>
  <li><pre>sudo pip3 install pyaudio</pre></li>
  <li><pre>sudo pip3 install SpeechRecognition</pre></li>
 </ul>
 <p>Αρχικά σκεφτήκαμε να ακούει συνεχώς τον χώρο, αλλά με οποιαδήποτε φασαρία ή θόρυβο προσπαθεί να αναγνωρίσει την ομιλία απαντώντας με την έκφραση αστοχίας “<i>Δεν κατάλαβα τι είπες.</i>”. Έπειτα σκεφτήκαμε να ενεργοποιούμε την ακρόαση ομιλίας σφυρίζοντας, χτυπώντας παλαμάκια ή λέγοντας μια λέξη κλειδί. Γι’ αυτό χρησιμοποιήσαμε την βιβλιοθήκη <a href="https://github.com/bishoph/sopare" target="_blank">sopare</a> ώστε μετά να καλεί το SpeechRecognition. Και πάλι τα αποτελέσματα δεν ήταν ικανοποιητικά. Τελικά κάναμε ότι και στα smart phones, δηλαδή πριν μιλήσουμε πατάμε σύντομα το εφεδρικό κουμπί στο J2 (ακροδέκτες 7 & 8). Αν το πατήσουμε παρατεταμένα παίζει ραδιόφωνο. Τότε το <a href="https://github.com/stav98/UrsaRobotics_SmartHome/blob/master/python/src/tts.py" target="code">tts.py</a> μας ειδοποιεί με την φράση “<i>Σας ακούω</i>”. Την δημοσίευση mqtt του ελεγκτή την ακούει και το πρόγραμμα <a href="https://github.com/stav98/UrsaRobotics_SmartHome/blob/master/python/src/speech_recogn.py" target="code">speech_recogn.py</a> το οποίο μπαίνει σε κατάσταση ακρόασης και αποκωδικοποίησης των φωνητικών εντολών. Αν γίνει επιτυχής αποκωδικοποίηση τότε δημοσιεύει το αντίστοιχο mqtt topic και γυρίζει σε κατάσταση αναμονής, δηλαδή περιμένει να ξαναπατήσουμε το κουμπί. Την επιβεβαίωση της εκτέλεσης αναλαμβάνει το tts.py το οποίο μας ειδοποιεί με φωνή για την ενέργεια. Αν δεν γίνει σωστή αναγνώριση, περιμένει 20sec και γυρίζει πάλι σε κατάσταση αναμονής.</p>
 <p>Στην γραμμή 91 δηλώνουμε τον αριθμό της συσκευής ηχογράφισης στην παράμετρο device_index:</p>
 <pre> with sr.Microphone(device_index=2) as source:</pre>
 <p>Για να βρούμε τον αριθμό της συσκευής εκτελούμε το αρχείο <a href="https://github.com/stav98/UrsaRobotics_SmartHome/blob/master/python/src/test.py" target="code">test.py</a> :</p>
 {% highlight python %}
  import speech_recognition as sr
  for index, name in enumerate(sr.Microphone.list_microphone_names()):
    print("Microphone with name \"{1}\" found for `Microphone(device_index={0})`".format(index, name))
 {% endhighlight %}
 <p>Μετά την εκτέλεση εμφανίζει κάτι παρόμοιο:</p>
 {% highlight bash %}
  Python 3.5.3 (default, Sep 27 2018, 17:25:39)
  [GCC 6.3.0 20170516] on linux
  Type "copyright", "credits" or "license()" for more information.
  >>>
  ==================== RESTART: /home/pi/smarthome/test.py ====================
  Microphone with name "bcm2835 ALSA: - (hw:0,0)" found for `Microphone(device_index=0)`
  Microphone with name "bcm2835 ALSA: IEC958/HDMI (hw:0,1)" found for `Microphone(device_index=1)`
  Microphone with name "USB Device 0x471:0x307: Audio (hw:1,0)" found for `Microphone(device_index=2)`
  Microphone with name "sysdefault" found for `Microphone(device_index=3)`
  Microphone with name "dmix" found for `Microphone(device_index=4)`
  Microphone with name "default" found for `Microphone(device_index=5)`
  >>>
 {% endhighlight %}
 <p>Για να ξεκινήσει η ακοκωδικοποίηση απαιτείται μια λέξη 'κλειδί' που στην περίπτωσή μας είναι η λέξη <b>'ΣΠΙΤΙ'</b>. Δεν έχει σημασία η σειρά των λέξεων, αρκεί να υπάρχουν οι σωστές λέξεις μέσα στην πρόταση. Δηλαδή καταλαβαίνει το ίδιο καλά αν πούμε '<i>Σπίτι πες μου την εξωτερική θερμοκρασία</i>' ή αν πόυμε '<i>Πες μου την εξωτερική θερμοκρασία στο σπίτι</i>'. Και στις δύο περιπτώσεις ανιχνεύει τις λέξεις Σπίτι, Εξωτερική και Θερμοκρασία.</p>
 <p>Τέλος το πρόγραμμα speech_recogn.py περιέχει τμήμα με τον κώδικα του tts.py ώστε να μας δίνει πληροφορίες όπως θερμοκρασίες, ώρα κλπ. Όπως και στα δύο προηγούμενα προγράμματα (tts.py και radio.py), αν θέλουμε να εκτελείται κατά την εκκίνηση του Raspberry, τότε πρέπει να το κάνουμε εκτελέσιμο και να το δηλώσουμε στο /etc/rc.local.</p>
 <center>
  <iframe width="560" height="315" src="https://www.youtube.com/embed/v0Mc70XVSyY" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
  <p><small>Δοκιμές αναγνώρισης με διαφορετικές φωνές μαθητών</small></p>
 </center>
 <br>
 <a href="./index.html">Αρχική</a>
</div>
