# คู่มือการตั้งค่า Technitium DNS Server

คู่มือนี้จะแนะนำขั้นตอนการตั้งค่า **Technitium DNS Server** หลังจากติดตั้งเสร็จสมบูรณ์ เพื่อให้สามารถใช้งานเป็น DNS Server ได้อย่างมีประสิทธิภาพ

---

## 1\. เข้าสู่หน้าเว็บจัดการ Technitium DNS

เปิดเว็บบราวเซอร์ของคุณแล้วเข้าสู่หน้าเว็บจัดการของ Technitium DNS Server โดยใช้ IP Address ของเครื่องเซิร์ฟเวอร์ และพอร์ต `5380`

```
http://<ip_address>:5380
```

> **ตัวอย่าง:** หาก IP Address ของเซิร์ฟเวอร์คือ `192.168.1.100` ให้เข้าถึงที่ `http://192.168.1.100:5380`

---

## 2\. ตั้งค่าทั่วไป (General Settings)

การตั้งค่าในส่วนนี้จะช่วยกำหนดข้อมูลพื้นฐานของ DNS Server ของคุณ

- ไปที่เมนู **`Settings`** \> **`General`**

  - **แก้ไข DNS Server Domain:**

    - ระบุชื่อโดเมนที่คุณต้องการให้ DNS Server นี้ใช้ เช่น `ns1.ctsurin.local`
    - นี่คือชื่อ **FQDN (Fully Qualified Domain Name)** ของ DNS Server ของคุณ

![technitium-dns-1](/docs/assets/image/technitium-dns-1.png)

- **ตั้งค่า Zone Defaults:**

  - เลื่อนหน้าจอลงมาที่หัวข้อ **`Zone Defaults`**
  - **ติ๊กเครื่องหมาย ☑️ ที่ช่อง `Use SOA Serial Date Scheme`** เพื่อให้ Technitium จัดการ Serial Number ของ SOA Record โดยใช้รูปแบบวันที่ ซึ่งช่วยในการจัดการ Zone Files ได้ง่ายขึ้น

![technitium-dns-2](/docs/assets/image/technitium-dns-2.png)

- เมื่อตั้งค่าเสร็จแล้ว **เลื่อนลงมาที่ล่างสุด** แล้วคลิกปุ่ม **`Save Settings`** เพื่อบันทึกการเปลี่ยนแปลง

---

## 3\. ตั้งค่าหน้าเว็บ (Web Service Settings)

การตั้งค่าในส่วนนี้จะช่วยเพิ่มความปลอดภัยให้กับการเข้าถึงหน้าเว็บจัดการผ่าน HTTPS

- ไปที่เมนู **`Settings`** \> **`Web Service`**

  - **เปิดใช้งาน HTTPS และการ Redirect:**
    - **ติ๊กเครื่องหมาย ☑️ ที่ช่อง `Enable HTTPS`** เพื่อเปิดใช้งานการเชื่อมต่อที่เข้ารหัส
    - **ติ๊กเครื่องหมาย ☑️ ที่ช่อง `Enable HTTP to HTTPS Redirection`** เพื่อบังคับให้การเชื่อมต่อ HTTP ถูกเปลี่ยนเส้นทางไปยัง HTTPS โดยอัตโนมัติ
    - **ติ๊กเครื่องหมาย ☑️ ที่ช่อง `Use A Self Signed TLS Certificate When TLS Certificate File Path is Unspecified`** เพื่อให้ Technitium สร้าง Self-Signed Certificate สำหรับ HTTPS โดยอัตโนมัติ หากคุณยังไม่ได้ระบุไฟล์ Certificate ของตัวเอง

![technitium-dns-3](/docs/assets/image/technitium-dns-3.png)

- เมื่อตั้งค่าเสร็จแล้ว **เลื่อนลงมาที่ล่างสุด** แล้วคลิกปุ่ม **`Save Settings`** เพื่อบันทึกการเปลี่ยนแปลง

---

## 4\. ตั้งค่า Forwarders

การตั้งค่า Forwarders จะช่วยให้ DNS Server ของคุณสามารถสอบถามชื่อโดเมนที่ไม่รู้จักจาก DNS Server ภายนอกได้

- ไปที่เมนู **`Settings`** \> **`Proxy & Forwarders`**

![technitium-dns-4](/docs/assets/image/technitium-dns-4.png)

- **เพิ่ม DNS ภายนอกในหัวข้อ `Forwarders`:**
  - ในช่องว่าง ให้ระบุ IP Address ของ DNS Server ภายนอกที่คุณต้องการใช้ เช่น
    - `1.1.1.1` (Cloudflare Public DNS)
    - `1.0.0.1` (Cloudflare Public DNS)
  - คุณสามารถเพิ่มได้หลายรายการ โดยแต่ละรายการจะถูกใช้เป็นตัวเลือกสำรอง หากรายการแรกไม่สามารถตอบสนองได้

![technitium-dns-5](/docs/assets/image/technitium-dns-5.png)

- เมื่อตั้งค่าเสร็จแล้ว **เลื่อนลงมาที่ล่างสุด** แล้วคลิกปุ่ม **`Save Settings`** เพื่อบันทึกการเปลี่ยนแปลง
