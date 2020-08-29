Step 1: Monitoring Vandalay's Web Servers


Speedtest Eval

2.

source="server_speedtest.csv" | eval ratio =  (upload_megabits / download_megabits)| table _time, ip_address,  download_megabits, upload_megabits, ratio

4.


Step 2: The Need for Speed


Based on the report created, what is the approximate date and time of the attack?

2020-02-22 14:30:00 - 2020-02-23 23:30:00


How long did it take your systems to recover?

Around 9 hours.


Step 3. Nessus


source="nessus_logs.csv" dest_ip="10.11.36.23"  severity="critical" | top severity

severity	count	percent
critical	49	100.000000

Save as > Alert 

Type: Realtime

rigger alert when
Number of Results
is greater than 0 
in 1 munute(s)



Trigger Actions > Add actions > Send Email 

					To:soc@vandalay.com.



Step 4

A bruteforce / DOS atack on the ADMINISTRATOR account was is progress on  February 21st between 9:00 am and 1:00 pm.



Step 5

Save As >  Alert

Alert type

Scheduled

Real-time

Expires
1
day(s)


--------------
Trigger Conditions

Trigger alert when
Number of Results
is greater than
15
in
1
hour(s)
Trigger
Once

Send email	
To
SOC@vandalay.com
Comma separated list of email addresses.
Show CC and BCC
Priority
Normal

Subject: Exchesive logins for ADMINISTRATOR acct.

Splunk Alert: $name$

The email subject, recipients and message can include tokens that insert text based on the results of the search. Learn More 
Message

The alert condition for '$name$' was triggered.

Type :Plain Text









