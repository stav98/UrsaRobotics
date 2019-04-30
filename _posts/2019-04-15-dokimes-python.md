---
layout: post
title:  "Δοκιμές αναγνώρισης φωνητικών εντολών"
---
<div style="text-align: justify;">
 <p>Σκεφτήκαμε ότι θα ήταν πολύ χρήσιμο, όταν είμαστε μέσα στο σπίτι να δίνουμε φωνητικές εντολές οι οποίες αναγνωρίζονται και εκτελείται η επιθυμητή ενέργεια. Το σύστημα μας απαντάει για την εξέλιξη της εντολής με φωνή T.T.S. Η υλοποίηση είναι πρακτικά απλή αρκεί να τοποθετήσουμε μικρόφωνα σε όλους τους εσωτερικούς χώρους του σπιτιού.</p>
 <p>Η αναγνώριση γίνεται online με το API Speech to Text της Google ή με όποιο άλλο θέλουμε. Θα θέλαμε να δοκιμάσουμε το Sphinx το οποίο είναι offline αναγνώριση φωνής αλλά έχουμε τον περιορισμό του χρόνου. Η απαντήσεις Text to Speech μπορεί να είναι online ή offline. Στην περίπτωση offline η φωνή δεν είναι τόσο φυσική.</p>
 <p>Το πρόγραμμα έχει γραφτεί σε Python 3.x και στην πραγματικότητα αφού γίνει η αναγνώριση των εντολών, μετά στέλνει ένα μήνυμα στον MQTT broker.</p>
 <p>Ακολουθεί video με δοκιμές από διαφορετικά πρόσωπα.</p>
 <center>
  <iframe width="560" height="315" src="https://www.youtube.com/embed/v0Mc70XVSyY" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
 </center>
 <a href="{{ "./index.html" | relative_url }}">Αρχική</a>
</div>
