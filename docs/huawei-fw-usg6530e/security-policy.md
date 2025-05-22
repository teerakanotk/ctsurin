# 🔐 Security Policy

Security Policy หรือนโยบายความปลอดภัย คือกฎหรือเงื่อนไขที่กำหนดขึ้นเพื่อควบคุมทราฟฟิกที่ผ่านไฟร์วอลล์ โดยระบุว่า “ใคร” (ผู้ใช้หรือระบบ) สามารถเข้าถึง “อะไร” (ทรัพยากรหรือบริการ) ได้ “เมื่อไร” และ “อย่างไร” ทั้งนี้เพื่อป้องกันการเข้าถึงโดยไม่ได้รับอนุญาต และลดความเสี่ยงจากภัยคุกคามทางไซเบอร์

---

### 🧱 Add Security Policy (การเพิ่มนโยบายความปลอดภัย)

1. เปิดเว็บเบราว์เซอร์ และล็อกอินเข้าสู่ระบบ
2. ไปที่ Policy > Security Policy > Add Security Policy

![security-policy-1](/docs/assets/security-policy-1.png)

![security-policy-2](/docs/assets/security-policy-2.png)

🛠️ 1. General Settings

- Name:
  ชื่อของนโยบาย (สูงสุด 32 ตัวอักษร) สามารถใช้ตัวอักษร, ตัวเลข, ขีดกลาง (-) และขีดล่าง (\_)
- Description:
  คำอธิบายสั้น ๆ เพื่อระบุวัตถุประสงค์ของนโยบาย
- Policy Group:
  กลุ่มของนโยบายที่ใช้จัดหมวดหมู่หรือกำหนดลำดับการทำงาน
- Tag:
  ป้ายกำกับสำหรับช่วยในการจัดการหรือค้นหา

🌐 2. Source and Destination

- Source Zone:
  โซนต้นทาง เช่น local, trust, dmz, untrust
- Destination Zone:
  โซนปลายทาง (ใช้หลักการเดียวกับ Source Zone)
- Source Address Zone:
  IP Address หรือช่วง IP ของต้นทาง
- Destination Address Zone:
  IP Address หรือช่วง IP ของปลายทาง
- VLAN ID:
  หมายเลข VLAN ที่เกี่ยวข้องกับการรับส่งทราฟฟิกในนโยบายนี้

👤 3. User and Service

- User:
  ระบุชื่อผู้ใช้ที่เกี่ยวข้องกับนโยบาย
- Access Mode:
  วิธีการเข้าถึง
- Device:
  ประเภทของอุปกรณ์ เช่น PC, Mobile
- Service:
  พอร์ตหรือโปรโตคอลที่อนุญาต เช่น TCP/80 (HTTP), TCP/443 (HTTPS)
- Application:
  ระบุแอปพลิเคชันหรือกลุ่มแอป เช่น Email, Social Media
- URL Category:
  หมวดหมู่ของเว็บไซต์ เช่น Business, Gambling, Adult
- Schedule:
  กำหนดช่วงเวลาที่นโยบายจะทำงาน เช่น วันทำงาน 09:00–17:00

✅ 4. Action

- Permit: อนุญาตให้ทราฟฟิกผ่าน
- Deny: ปฏิเสธการเข้าถึง

🧩 5. Content Security (ระบบป้องกันเชิงลึก)

- Antivirus: ตรวจจับและป้องกันไวรัส
- Intrusion Prevention: ตรวจจับ/ป้องกันการบุกรุก (IPS)
- URL Filtering: กรอง URL ที่ไม่เหมาะสม
- File Blocking: บล็อกไฟล์ตามประเภท เช่น .exe, .bat
- Data Filtering: ป้องกันข้อมูลสำคัญรั่วไหล เช่น หมายเลขบัตรประชาชน
- Application Behavior Control: ควบคุมพฤติกรรมของแอปพลิเคชัน
- Cloud Access Security Awareness (CASA): ควบคุมการเข้าถึง Cloud Service
- Email Filtering: ตรวจสอบและกรองอีเมล
- APT Defense: ป้องกันภัยคุกคามแบบ Advanced Persistent Threats
- DNS Filtering: กรอง DNS เพื่อบล็อกเว็บไซต์อันตราย

⚙️ 6. Other Options

- Record Traffic Logs:
  เปิดการบันทึก Log เพื่อเก็บข้อมูลการใช้งาน และสามารถตรวจสอบย้อนหลังได้

**Example:**

ต้องการเพิ่มนโยบายความปลอดภัยที่อนุญาตให้ `Client Ping ไปยังภายนอกได้`

**Template:**

- Name: client_icmp_untrust
- Src-Zone: trust
- Dst-Zone: untrust
- Src-Addr: 192.168.0.0/24
- Dst-Addr: 8.8.8.8/32
- Service: ICMP
- Action: Permit

![security-policy-3](/docs/assets/security-policy-3.png)

> Test: Client ใช้คำสั่ง Ping ไปยัง 8.8.8.8 หากมีการตอบกลับมาแสดงว่ากำหนดค่านโยบายสำเร็จ
