# คู่มือการติดตั้ง Technitium DNS บน Ubuntu 22.04 LTS

คู่มือนี้จะแนะนำขั้นตอนการติดตั้ง Technitium DNS Server บนระบบปฏิบัติการ Ubuntu 22.04 LTS

---

## 1. อัปเดต Repository ให้เป็นแพตช์ล่าสุด

```bash
sudo apt update && sudo apt upgrade -y
```

> **คำอธิบาย:**
>
> - `sudo apt update`: ดึงข้อมูลแพ็คเกจล่าสุดจาก repository
> - `sudo apt upgrade -y`: อัปเกรดแพ็คเกจทั้งหมดที่สามารถอัปเกรดได้ โดย `-y` จะเป็นการตอบตกลงโดยอัตโนมัติ

---

## 2. ติดตั้ง Technitium DNS Server

ใช้สคริปต์การติดตั้งอย่างเป็นทางการจาก Technitium เพื่อดำเนินการติดตั้ง Technitium DNS Server

```bash
curl -sSL https://download.technitium.com/dns/install.sh | sudo bash
```

> **คำอธิบาย:**
>
> - `curl -sSL https://download.technitium.com/dns/install.sh`: ดาวน์โหลดสคริปต์การติดตั้งจาก URL ที่กำหนด
> - `| sudo bash`: ส่งผลลัพธ์ของสคริปต์ที่ดาวน์โหลดมาไปยัง `bash` เพื่อเรียกใช้งานด้วยสิทธิ์ผู้ดูแลระบบ (`sudo`)

โปรดรอจนกว่ากระบวนการติดตั้งจะเสร็จสมบูรณ์ ซึ่งอาจใช้เวลาสักครู่ขึ้นอยู่กับความเร็วอินเทอร์เน็ตและประสิทธิภาพของระบบ

---

## 3. เข้าสู่หน้าเว็บจัดการ Technitium DNS

เมื่อการติดตั้งเสร็จสิ้น คุณสามารถเข้าถึงหน้าเว็บจัดการของ Technitium DNS ได้ผ่านเว็บบราวเซอร์ โดยใช้ IP Address ของเครื่องเซิร์ฟเวอร์ Ubuntu ของคุณ และพอร์ต `5380`

เปิดเว็บบราวเซอร์แล้วพิมพ์ URL ต่อไปนี้:

```
http://<ip_address>:5380
```

![technitium-setup-1](/assets/image/technitium-setup-1.png)

> **ตัวอย่าง:** หาก IP Address ของเซิร์ฟเวอร์ของคุณคือ `192.168.1.100` ให้พิมพ์ `http://192.168.1.100:5380` ในเว็บบราวเซอร์ของคุณ
