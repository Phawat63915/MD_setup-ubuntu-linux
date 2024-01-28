### Enable SSH Root Login
ตั้งค่าเพื่อให้สามารถเข้าใช้งานผ่าน SSH ด้วย Root ได้

1. แก้ไขไฟล์ `sshd_config`
```bash
sudo vi /etc/ssh/sshd_config
```
2. เพิ่มบรรทัดใหม่นี้ ที่ `/etc/ssh/sshd_config` ว่า `PermitRootLogin yes` ที่บรรทัดใหม่หรือสุดท้าย
```/etc/ssh/sshd_config
PermitRootLogin yes
```

3. set password root
เปลี่ยนเป็น root
```
sudo -i
```
ตั้งรหัสผ่าน พิมคำสั่งแล้ว ใส่รหัสที่จะตั้ง 2 ครั้ง
```
passwd
```

4. Restart sshd service
```
systemctl restart sshd
```

```
service sshd restart
```