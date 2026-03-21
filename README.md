# AED Report Decoder — JIA TRAINER CENTER

ระบบถอดรหัส binary log จากเครื่อง AED (Primedic/Yuwell) แล้วสร้างรายงาน CPR ภาษาไทย

## Deploy บน Vercel

### ขั้นตอน

1. **Push ขึ้น GitHub**
   ```bash
   git init
   git add .
   git commit -m "AED Report Decoder v1"
   git remote add origin https://github.com/YOUR_USERNAME/aed-report-web.git
   git push -u origin main
   ```

2. **เชื่อม Vercel**
   - ไปที่ [vercel.com](https://vercel.com) → Sign in ด้วย GitHub
   - กด "New Project" → เลือก repo `aed-report-web`
   - กด "Deploy" → เสร็จ! ได้ลิงก์ xxx.vercel.app

3. **ต่อ subdomain (aedreport.jiacpr.com)**
   - ใน Vercel → Settings → Domains → เพิ่ม `aedreport.jiacpr.com`
   - ไปที่ DNS ของ jiacpr.com → เพิ่ม CNAME record:
     ```
     Type: CNAME
     Name: aedreport
     Value: cname.vercel-dns.com
     ```
   - รอ 5-10 นาที → เสร็จ!

## Config ที่ต้องแก้

| รายการ | ไฟล์ | ค้นหา |
|---|---|---|
| QR PromptPay | index.html | `[QR Code PromptPay]` |
| รหัสปลดล็อค | index.html | `UNLOCK_CODES` |
| เลขบัญชี | index.html | `xxx-xxx-xxxx` |

## รหัสปลดล็อค

ส่งให้ลูกค้าทาง LINE หลังตรวจสลิปแล้ว:
- `JIACPR2024` — รหัสถาวร
- `AED299` — สำหรับ Basic
- `AED499` — สำหรับ Pro
- เพิ่มรหัสใหม่ได้ใน `UNLOCK_CODES` array

## Stack

- Pure HTML + CSS + JS (ไม่มี framework)
- Claude API (Anthropic) สำหรับ decode
- Vercel สำหรับ hosting (ฟรี)
