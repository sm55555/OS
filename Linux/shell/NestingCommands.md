# NestingCommands

Command 치환

- 명령어의 결과를 치환하여 실행

NestingCommands

```
$(Commands)
`Commands`
```

```
~$ date
~$ 'Today is $(date)'
~$ 'Today is date'
~$ "Today is $(date +%Y%m%d)"
```
