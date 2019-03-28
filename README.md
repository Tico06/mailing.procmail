# mailing.procmail
Simple mailing list with procmail and email aliases

This procmail script helps to setup and secure mailing lists defined with email aliases (/etc/aliases). This script has been developped against a Fedora 28, sendmail 8.15, procmail 3.22.

The initial need was to secure a email aliases to avoid spam to be relayed from my email server to the alias members. No automation for subscription or wathever.

mailing.procmail installation:

1/ Create a user to manage the mailing lists
root $> useradd mailing

2/ Copy mailing.procmailrc and procmailrc.sample in ~mailing/
root $> cp procmailrc.sample mailing.procmailrc ~mailing/
root $> chown mailing:mailing ~mailing/procmailrc.sample ~mailing/mailing.procmailrc

3/ Create .procmailrc and update vars accordingly to your mailing lists. Vars are documented in mailing.procmailrc
root $> cp procmailrc.sample .procmailrc
root $> vim .procmailrc
MAILDIR="${HOME}/.mail"

##### Vars for mailing.procmailrc ## test_list ##
LIST="user1@domain.com,user2@other.com,user.three@otherdomain.net"
LIST_NAME="test_list"
LIST_LIB="Testing mailing list"
LIST_REFUSED="This is an automatic answer.
You are not authorized to post on ${LIST_NAME}@mydomain.com.
Your email won't be read."

#LOGFILE="${HOME}/${LIST_NAME}.procmail.log"

INCLUDERC=${HOME}/mailing.procmailrc



##### Vars for mailing.procmailrc ## sillages ##
LIST_NAME="my_list"
INCLUDERC=/home/john/.config/procmail/${LIST_NAME}rc

LOGFILE="${HOME}/${LIST_NAME}.procmail.log"

INCLUDERC=${HOME}/mailing.procmailrc

### Send the email to root if not distributed at this point
:0
! root
:wq
------------------------------------------------------

mailing lists members, label and refused message could be manage by end users at the time the corresponding vars are in files with read access.

4/ Create an alias for each mailing list in /etc/aliases
root $> vim /etc/aliases
test_list:      mailing
my_list:        mailing
:wq

--------------------------------------------------------
root $> newaliases
