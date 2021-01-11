# log filtering

### using xml

<QueryList>
  <Query Id="0" Path="Security">
    <Select Path="Security">*[System[(EventID=4624)]] and
*[EventData[Data[@Name='TargetDomainName'] and (Data='inhauh')]]
</Select>
  </Query>
</QueryList>


https://onehundredpanda.blogspot.com/2017/08/windows-event-log-xml-custom-view.html 참고
