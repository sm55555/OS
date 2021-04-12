# 이벤트 뷰어 로그 필터링

### xml을 사용하는 로그 필터링

![image](https://user-images.githubusercontent.com/38831314/114356053-20fb8700-9bab-11eb-8542-ee7ba2faedab.png)

현재 로그 필터링 클릭

![image](https://user-images.githubusercontent.com/38831314/114355966-06c1a900-9bab-11eb-993f-dbb006cbf036.png)

```
<QueryList>
  <Query Id="0" Path="Security">
    <Select Path="Security">*[System[(EventID=4624)]] and
*[EventData[Data[@Name='TargetDomainName'] and (Data='test')]]
</Select>
  </Query>
</QueryList>
```

System의 EventID 4624를 검색하고 EventData의 DataName의 TargetDomainName을 검색하고 Date가 test인 것을 찾아내는 XML이다.


[참고 URL]
https://onehundredpanda.blogspot.com/2017/08/windows-event-log-xml-custom-view.html 참고
