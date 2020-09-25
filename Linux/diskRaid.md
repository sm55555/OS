## RAID 0 구성

#### Linear : 디스크를 배열 형태로 단순하게 연결

mdadm --create /dev/md/linear --level linear --raid-devices=2 /dev/xvdf /dev/xvdg

#### Stripe : 데이터의 내용을 분산 저장하여 속도가 빠르게 저장  but 안정성 down

mdadm --create /dev/md/stripe --level stripe --raid-devices=2 /dev/xvdh /dev/xvdi

## RAID 1 구성

mdadm --create /dev/md/mirror --level mirror --raid-devices=2 /dev/xvdj /dev/xvdk

## RAID 5 구성

mdadm --create /dev/md/raid5 --level=5 --raid-devices=3 /dev/xvdl /dev/xvdm /dev/xvdn

## RAID 정보 보는법
mdadm --detail /dev/md/linear

## 파일 포맷
mkfs -t ext4 /dev/md/linear

마운트 진행
