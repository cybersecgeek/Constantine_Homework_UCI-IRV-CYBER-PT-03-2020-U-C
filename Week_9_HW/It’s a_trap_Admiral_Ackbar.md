Mission 1




The Resistance (starwars.com) is able to send emails but unable to receive any because asltx.l.google.com is a valid record and  asltx.2.google.com is not.



---------------------------------------------------------------------------
Mail eXchanger 	Priority 
------------------------------
aspmx2.googlemail.com 	10
alt1.aspx.l.google.com 	5
alt2.aspmx.l.google.com 	5
aspmx3.googlemail.com 	10
aspmx.l.google.com 	1
---------------------------------------------------------------------------




Mission 2

v=spf1 a mx mx:smtp.secureserver.net include:aspmx.googlemail.com ip4:104.156.250.80 ip4:45.63.15.159 ip4:45.63.4.215

The new ip (45.23.176.21) is not included in the SFP records.
This is why the emails are going to the [:::spam::::] folder.

<!----
      Now I am hungry and want some SPAM.
      pause()
      Well we can't have everything...
      Will check the Cantina later. -
                                    ---->

Correct records:

v=spf1 a mx mx:smtp.secureserver.net include:aspmx.googlemail.com ip4:104.156.250.80 ip4:45.63.15.159 ip4:45.63.4.215 ip4:45.23.176.21




Mission 3
