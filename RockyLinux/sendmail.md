

telnet localhost 25


ehlo localhost


mail from:1234@naver.com

rcpt to: test@naver.com

250 2.1.5 OK

data
345 End data with <CR><LF><CR><LF>
subject : mail test
bodybodybody
.
250 2.0.0 OK queued as 
