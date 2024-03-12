
```
[localhsot]$ telnet localhost 25

.
.
.
220 mail2.naver.com ESMTP Postfix
ehlo localhost
250 ETRN
250 DSN
250 VERY
mail from:1234@naver.com
250 2.1.5 OK
rcpt to: test@naver.com
250 2.1.5 OK
data
345 End data with <CR><LF><CR><LF>
subject : mail test
bodybodybody
.
250 2.0.0 OK queued as 
```
