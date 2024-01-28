### Setting Network
ตั้งค่า fixip เพื่อไม่ให้ DHCP แก้ไข IP ให้เราหรือสุ่มมั่วทุกคั้งที่เราเปิดเครื่อง

1. เช็กวง IP ก่อน ดูว่าชื่อ Interface ที่เราใช้งานอยู่ ส่วนมากจะพบว่าเป็น ETH0 และ ETH1 แต่ถ้าเป็น VM อาจจะเป็น enp0s3 และ enp0s8 หรือ enp0s9 ก็ได้ และดูว่า เราได้รับ IP อะไร จาก DHCP มา

```bash
ip a
```
2. เปิดแก้ไขไฟล์ `/etc/netplan/00-installer-config.yaml`
```bash
vi /etc/netplan/00-installer-config.yaml
```
3. แก้ไขไฟล์ `/etc/netplan/00-installer-config.yaml` แก้ไข config ตามต้องการ
* **Interface:** ปกติชื่อ eth0, eth1 หรือ VM อาจเป็น enp0s3 และ enp0s8 หรือ enp0s9 คือชื่อ Interface หรืออาจเป็นชื่ออื่นๆก็ได้
* **dhcp4:** หากเป็น `true` จะได้ IP จาก DHCP หากเป็น `false` จะได้ IP จาก addresses ที่เรากำหนด
* **addresses:** กำหนด IP และ Subnet ที่เราต้องการให้เครื่องนี้ใช้งาน
* **optional:** หากเป็น `false` จะรอ Interface นี้เชื่อมต่อเส็จรก่อนจึง boot เป็น `true` คือไม่จำเป็น (**หากต้องกาารให้เครื่องเปิดเร็ว ปรับเป็น true**)
```yaml
# This is the network config written by 'subiquity'
network:
  ethernets:
    enp0s3:
      dhcp4: true
      optional: true
    enp0s8:
      dhcp4: false
      optional: true
      addresses: [192.168.56.15/24]
    enp0s9:
      dhcp4: true
      optional: true
  version: 2

```

4. เริ่มใช้การกำหนดค่าใหม่
```bash
sudo netplan apply
```

https://netplan.io/