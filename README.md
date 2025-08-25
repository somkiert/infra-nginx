# Infra Nginx Config

Repository นี้เก็บไฟล์ `sbh.conf` สำหรับ Nginx reverse proxy ภายใน  
ปัจจุบันใช้เพื่อ proxy ไปยัง 2 บริการหลัก:
- **/welcome** → เว็บที่พอร์ต `4001`
- **/api** → Backend API ที่พอร์ต `3002`

---

## วิธีติดตั้ง / ใช้งานครั้งแรก (บน server)

1. Clone repo
   ```bash
   sudo git clone https://github.com/DigitalHelathSBH/infra-nginx.git /opt/infra-nginx
   ```
2. ลบไฟล์ sbh.conf เดิม (ถ้ามี) แล้วทำ symlink
   ```bash
   sudo rm -f /etc/nginx/conf.d/sbh.conf
   sudo ln -s /opt/infra-nginx/sbh.conf /etc/nginx/conf.d/sbh.conf
   ```
3. ตรวจสอบและ reload nginx
   ```bash
   sudo nginx -t && sudo systemctl reload nginx
   ```
## วิธีอัปเดตเมื่อแก้ sbh.conf
1. บนเครื่องพัฒนา:
- **แก้ไฟล์** `sbh.conf` ตามต้องการ
- **commit + push ขึ้น GitHub**
   ```bash
   git add sbh.conf
   git commit -m "update sbh.conf: <อธิบายสิ่งที่แก้>"
   git push
   ```
2. บน server:
- **ดึงไฟล์ใหม่**
  ```bash
   cd /opt/infra-nginx
   sudo git pull
   ```
- **ตรวจสอบและ reload nginx**
   ```bash
   sudo nginx -t && sudo systemctl reload nginx
   ```


