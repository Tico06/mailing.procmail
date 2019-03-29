# mailing.procmail
Simple mailing list with procmail and email aliases

This procmail script helps to setup and secure mailing lists defined with email aliases (/etc/aliases). This script has been developped against a Fedora 28, sendmail 8.15, procmail 3.22.

The initial need was to secure a email aliases to avoid spam to be relayed from my email server to the alias members. No automation for subscription or wathever.

mailing.procmail installation:

1/ Create a user to manage the mailing lists<br>
root $> useradd mailing

2/ Copy mailing.procmailrc and procmailrc.sample in ~mailing/<br>
root $> su - mailing/<br>
mailing $> cp procmailrc.sample mailing.procmailrc ~mailing/<br>
mailing $> chown mailing:mailing ~mailing/procmailrc.sample ~mailing/mailing.procmailrc<br>

3/ Create .procmailrc and update vars accordingly to your mailing lists. Vars are documented in mailing.procmailrc<br>
mailing $> cp procmailrc.sample .procmailrc<br>
mailing $> vim .procmailrc

mailing lists members, label and refused message could be manage by end users at the time the corresponding vars are in files with read access.

4/ Create an alias for each mailing list in /etc/aliases<br>
root $> vim /etc/aliases<br>
test_list:      mailing<br>
my_list:        mailing<br>
:wq<br>

--------------------------------------------------------<br>
root $> newaliases
