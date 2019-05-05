---
layout: default
---
<div style="text-align: justify;">
 <H1>Το περιβάλλον Node-Red και η λογική του έξυπνου σπιτιού</H1>
 <p>Για να συνεργαστούν όλα τα προηγούμενα σωστά και να υπάρχει η δυνατότητα του αυτοματισμού θα χρειαστούμε το λογισμικό Node-Red. Το Node-Red είναι εγκατεστημένο στο Raspberry Pi. Εμείς εγκαθιστούμε το Dashboard και το ενεργοποιούμε ώστε να τρέχει ως υπηρεσία, σύμφωνα με τον <a href="https://github.com/stav98/UrsaRobotics_SmartHome/blob/master/node-red/Rasp_NodeRed.pdf" target="_blank">οδηγό</a>.</p>
 <p>Για να συνδεθούμε στο backend του Node-Red και να αρχίσουμε να φτιάχνουμε το διάγραμμα ροής (Flow), αρκεί να γράψουμε στον browser http://Raspberry-IP-address:1880 και θα εμφανιστεί ο επεξεργαστής διαγραμμάτων. Είναι γραφικό περιβάλλον και αριστερά έχουμε όλα τα διαθέσιμα εργαλεία, στη μέση σχεδιάζουμε το διάγραμμα και δεξιά βλέπουμε πληροφορίες, ιδιότητες και μηνύματα εκσφαλμάτωσης.</p>
 <center>
  <a href="{{ "/assets/images/node_red_flow1.png" | relative_url }}" onclick="return hs.expand(this)" class="highslide" target="_self">
   <img src="{{ "/assets/images/node_red_flow1_small.png" | relative_url }}" alt="Μεγένθυση" title="Μεγένθυση" style="float: center; margin: 5px; border: 1px solid #000000; width: 400px;">
  </a>
 </center>
 <p>Όταν τελειώσουμε και θέλουμε να δοκιμάσουμε την λειτουργία του flow, πατάμε το κουμπί Deploy πάνω δεξιά. Για να δούμε το User Interface (U.I.) ή Front end γράφουμε το url http://Raspberry-IP-address:1880/ui και εφόσον έχουμε προσθέσει controls του dashboard, τότε θα εμφανιστεί μπροστά μας.</p>
 <center>
  <a href="{{ "/assets/images/node_red_ui1.png" | relative_url }}" onclick="return hs.expand(this)" class="highslide" target="_self">
   <img src="{{ "/assets/images/node_red_ui1_small.png" | relative_url }}" alt="Μεγένθυση" title="Μεγένθυση" style="float: center; margin: 5px; border: 1px solid #000000; width: 400px;">
  </a>
 </center>
 <p>Μπορούμε στο UI να έχουμε πολλά tabs ανά κατηγορία συσκευών ή ανά χώρο του σπιτιού ή όποια άλλη οργάνωση εμείς θέλουμε. Εμείς στο δεύτερο tab έχουμε γραφήματα με τις καταγραφές κάποιων μετρήσεων.</p>
 <center>
  <a href="{{ "/assets/images/node_red_ui2.png" | relative_url }}" onclick="return hs.expand(this)" class="highslide" target="_self">
   <img src="{{ "/assets/images/node_red_ui2_small.png" | relative_url }}" alt="Μεγένθυση" title="Μεγένθυση" style="float: center; margin: 5px; border: 1px solid #000000; width: 400px;">
  </a>
 </center>
 <p>Για να δοκιμάσετε το δικό μας flow πατάμε πάνω αριστερά στις τρεις γραμμές - Import - Clipboard. Αντιγράφετε το <a href="https://raw.githubusercontent.com/stav98/UrsaRobotics_SmartHome/master/node-red/src/flow-4-5-19.txt" target="code">flow-dd-mm-yy.txt</a> στο πρόχειρο και το επικολλάτε στο πλαίσιο κειμένου και μετά πατάτε το κουμπί Import.</p>
 <p>Θα δημοσιεύσουμε μερικά φύλλα εργασίας με απλές ασκήσεις προγραμματισμού πάνω στα διαγράμματα ροής του Node-Red.</p>
 <a href="./index.html">Αρχική</a>
</div>
