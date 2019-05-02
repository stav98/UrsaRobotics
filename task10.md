---
layout: default
---
<div style="text-align: justify;">
 <H1>Κείμενο σε ομιλία και αναπαραγωγή μουσικής</H1>
 <p>Θεωρήσαμε απαραίτητο όταν δίνουμε μια διαταγή ή όταν αυτόματα ενεργοποιείται ή απενεργοποιείται μια συσκευή, να ακούμε στα ελληνικά ένα φωνητικό μήνυμα. Μέσα στο σπίτι υπάρχουν ηχεία ώστε να ακούμε τα μηνύματα επιβεβαίωσης ή την μουσική.</p>
 <p>Το πρόγραμμα για την ομιλία Text To Speech (T.T.S.) είναι το <a href="https://github.com/stav98/UrsaRobotics_SmartHome/blob/master/python/src/tts.py" target="code">tts.py</a> και είναι γραμμένο σε Python 3.x. Απαιτείται η εγκατάσταση του mplayer, του espeak και της βιβλιοθήκης Paho mqtt. Στην πραγματικότητα έχουμε φτιάξει ένα mqtt client το οποίο κάνει συνδρομή σε όποια topics θέλουμε να παίρνουμε ηχητική επιβεβαίωση. Τα topics, το απαιτούμενο payload καθώς και η πρόταση που θα πει υπάρχουν στο αρχείο κειμένου <a href="https://github.com/stav98/UrsaRobotics_SmartHome/blob/master/python/src/tts_topics.txt" target="code">tts_topics.txt</a>.</p>
 <p>Στην αρχή διαβάζει το αρχείο και κάνει συνδρομή στα topics. Αν θέλουμε να απενεργοποιήσουμε κάποιο αρκεί να βάλουμε μια # στην πρώτη στήλη. Στη συνέχεια ακούει για πάντα τι μεταδίδει ο broker. Αν γίνει publish σε κάποιο topic που έχει κάνει εγγραφή, τότε εξετάζει το payload και αν υπάρχει λέει το φωνητικό μήνυμα.</p>
 <p>Υπάρχουν δύο υλοποιήσεις του T.T.S. Η offline που έχει συνθετική φωνή robot voice αλλά δεν απαιτεί σύνδεση internet και έχει γρήγορη απόκριση και η online που στέλνει το κείμενο στη google και μετά αναπαράγει το αρχείο ήχου που επιστρέφει η μηχανή της google. Η δεύτερη έχει φυσική φωνή. Η επιλογή γίνεται στις γραμμές 13 και 14 αλλάζοντας την τιμή του string voice.</p>
 <p>Επειδή θέλουμε να τρέχει συνέχεια από το ξεκίνημα του Raspberry, το κάνουμε εκτελέσιμο chmod 755 tts.py και προσθέτουμε στο τέλος του /etc/rc.local την παρακάτω γραμμή πριν το exit 0:</p>
 {% highlight bash %}
  ..........
  ..........
  /home/pi/smarthome/tts.py &
  /home/pi/smarthome/radio.py &

  exit 0
 {% endhighlight %}
 <p>Επίσης δώσαμε την δυνατότητα αναπαραγωγής ραδιοφώνου με το πρόγραμμα <a href="https://github.com/stav98/UrsaRobotics_SmartHome/blob/master/python/src/radio.py" target="code">radio.py</a>. Εδώ όταν πατάμε παρατεταμένα το button (είχαμε προσθέσει και ένα εφεδρικό κουμπί στο J2 ακροδέκτες 7 και 8) αρχίζει η αναπαραγωγή μιας ραδιοφωνικής ροής (streaming). Η μουσική ακούγεται σε χαμηλότερη ένταση από την ομιλία. Αν πατήσουμε ξανά παρατεταμένα το κουμπί τότε η μουσική σταματάει. Επίσης και αυτό το πρόγραμμα ξεκινάει αυτόματα στο /etc/rc.local όπως φαίνεται παραπάνω.</p>
 <p>Αν θέλουμε να ακούσουμε άλλη ροή αρκεί να τη δηλώσουμε στο string station γραμμή 15.</p>
 <center>
   <iframe width="560" height="315" src="https://www.youtube.com/embed/2SjtGgD_fMg" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
 </center>
 <a href="./index.html">Αρχική</a>
</div>
