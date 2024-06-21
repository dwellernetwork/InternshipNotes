Toad for Oracle is the tool we will use.

select * from INTEGRATION_AUTOMATIONS_TBL order by ins_date deac

εχει πεσει ενα: 
COMSOTE_ONE_NOTIFICATION_MODIFY_OTE (this is the worklsit task name)

ο client ειναι ο ΟΤΕ (η σταθερη) . cosmote_one ειναι ενα πακετο με σταθερο κινητο σε ενα.
οταν πας και αλλαξεις συμβολαιο στη σταθερη, και κανεις τροποποιηση στα benefit, επειδη εχουν κινητο και σταθερο, επηρεαζονται και τα δυο μαζι.
Αλλα ο initiator απλα το γραφει σταθερη, εξου και το client_ote.

Εχουμε 50 με θεμα soft bundling not found. 

SOFT BUNDLING NOT FOUND ()

select * from KD_WORKLIST_ISSUE JEE where TASK_NAME_SYSTEM = ' COSMOTE_ONE_NOTIFICATION_MODIFY.OTE" where extracted_issue like "SOFT BUNDLING NOT FOUND" .     
	- εχουμε 50 matches. 

SECT AS_CI_REQUEST_ABORT (phone number here) from dual;
	DO NOT ABORT REQUEST  
		-Αυτο ειναι που θα κανουμε σε καθε ενα απο αυτα. 

for x in (select request_id from ws_requests where blablabla 

dbms_output.put_line (v_output || ' '||x.request_id);

-end loop;

end;