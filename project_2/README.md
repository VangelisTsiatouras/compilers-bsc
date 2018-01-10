MiniJava Semantic Analysis
---

### Compile & Execution

* __make__ : Compile
* __make clean__ : Διαγραφη .class αρχείων
* __java Main [file1] , [file2],...,[fileN]__ : Εκτέλεση

 ### Παραδοχές

 * Το type checking πραγματοποιείται σε 2 στάδια.  
   * Στο πρώτο visit αποθηκεύονται class names, fields, method names, parameters και variables μεθόδων.
     Κατά τη διαδικασία γίνεται έλεγχος αν έχουν αποθηκευτεί τα παραπάνω ήδη μέσα στο symbol table 
     π.χ. διπλότυπα declaration τερματίζουν το parsing απευθείας σε αυτό το στάδιο. Στην συνέχεια μετά το
     πέρας της αποθήκευσης της χρήσιμης πληροφοιας στη δομή του symbol table, πραγματοποιέιται ένα σειριακό
     πέρασμα στα επιμέρους πεδία της δομής για να επαληθευτούν οι τύποι που έχουν δηλωθεί αν είναι νόμιμοι.
     Με αυτό το τρόπο δηλώσεις πεδίων ή μεταβλητών και παραμέτρων μέσα σε μεθόδους με τύπους κλάσεων που 
     δεν υπάρχουν στο δωθέν κώδικα που παρσάρεται εκείνη τη στιγμή, τερματίζουν επίσης το parsing.
   * Στο δεύτερο visit πραγματοποιείται το type checking στα επι μέρους expression και statement. Γενικά ο
     τρόπος με τον οποίο υλοποιήθηκε αυτή η διαδικασία είναι μέσω της επιστροφής του τύπου (int, int[], boolean, classType)
     της εκάστοτε παράστασης που διαχειρίζεται ένας visitor την προκειμένη στιγμή. Οι τύποι αυτοί συγκεντρωνονται 
     σε ανωτέρου επιπέδου visitor (Statement visitor κυρίως) όπου πραγματοποιόυνται έλεγχοι για την νομιμότητα
     των expression που περιέχουν.
 * Για την υλοποιήση του symbol table χρειάστηκε να αναπτυχθεί μια δομή η οποία αποτελείται κυρίως απο 
   LinkedHashMaps. Πιο συγκεκριμένα είναι μια κλάσση που περιέχει Map για τις κλάσσεις, οι οποίες περιέχουν Map για field
   και methods όπου τελικά τα Map των μεθόδων περιέχουν Map απο παραμέτρους και μεταβλητές.
 * Σε περίπτωση λαθών του εισερχόμενου κώδικα εκτυπώνονται μηνύματα σχετικά με το error το οποίο βρέθηκε και το parse σταματά
   στο πρώτο λάθος χώρις να γίνει υπολογισμός V-Table.
 * Τα V-Tables αποθηκεύονται στο directory 'v-tables'.
 * Γενικά το πρόγραμμα παρσάρει σωστά όλα τα test αρχεία που έχουν δωθέι.   