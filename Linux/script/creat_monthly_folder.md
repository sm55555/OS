
### 월별로 폴더 생성 방법

```

#!/bin/bash


TDATE1=`date +%Y%m --date '1 months ago'`
TDATE2=`date +%Y-%m --date '1 months ago'`

cd $1
pwd
mkdir $TDATE1
mv *$TDATE1* $TDATE1
mv *$TDATE2* $TDATE1


```
