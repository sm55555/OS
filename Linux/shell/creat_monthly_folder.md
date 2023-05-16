
### 월별로 폴더 생성 방법

```
#!/bin/bash

TDATE1=`date +%Y%m --date '1 months ago'`
TDATE2=`date +%Y-%m --date '1 months ago'`

mkdir $TDATE1
mv *$TDATE1* $TDATE1
mv *$TDATE2* $TDATE1
```

#### 수행 전

<img src="https://user-images.githubusercontent.com/38831314/111945531-3ab22d00-8b1d-11eb-881f-0d7d35ea035f.png">

#### 수행 후

<img src="https://user-images.githubusercontent.com/38831314/111945819-b01dfd80-8b1d-11eb-931a-04c4dbe584dd.png">

