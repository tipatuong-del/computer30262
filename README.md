[README.md](https://github.com/user-attachments/files/34409859/README.md)
# Python Learning Platform — ว30262

เว็บไซต์ภาษาไทยสำหรับนักเรียน ม.4 มีบทเรียน 7 หน่วย 77 หัวข้อ แบบฝึก 30 ข้อ และการรัน Python ด้วย Pyodide Web Worker

## เริ่มใช้งาน

ต้องเปิดผ่านเว็บเซิร์ฟเวอร์ ไม่ใช่เปิดไฟล์ index.html ด้วย file:// เพราะ Web Worker และการโหลด Pyodide อาจถูกบล็อก

```bash
cd python_learning_platform
python -m http.server 8000
```

เปิด http://localhost:8000 ในเบราว์เซอร์ที่เชื่อมอินเทอร์เน็ต หรืออัปโหลดไฟล์ `index.html`, `style.css`, `app.js`, `data.js`, `worker.js` ไปยัง static hosting ที่รองรับ HTTPS เช่น GitHub Pages หรือ Netlify

## การจัดเก็บและข้อจำกัด

- เก็บโปรไฟล์ สถานะการยืนยันกิจกรรม โค้ด และผลผ่านแบบฝึกใน LocalStorage ของเบราว์เซอร์ปัจจุบันเท่านั้น
- คะแนน Google Forms และเกม Canva ไม่ถูกดึงมา ระบบแสดงเฉพาะสถานะยืนยันด้วยตนเอง
- ไม่มีระบบลงชื่อเข้าใช้ ฐานข้อมูลกลาง หรือ Teacher Dashboard สำหรับนักเรียนหลายคน
- การตรวจโค้ดใช้ผลลัพธ์จาก Test Cases ที่กำหนด (ไม่ใช่การตรวจทุกกรณีที่เป็นไปได้)
- ใช้ Pyodide CDN สำหรับ Python Runtime และจำกัดเวลารัน 8 วินาที; การโหลดครั้งแรกอาจใช้เวลานานและเกิด timeout บนเครือข่ายช้า
- หากต้องใช้ในการวิจัยอย่างเป็นทางการ ควรทดสอบความถูกต้องของโจทย์/กรณีทดสอบ การเข้าถึง และการเก็บหลักฐานเพิ่มเติม

## โครงสร้าง

- `data.js`: บทเรียน 77 หัวข้อ แบบฝึก 30 ข้อ และลิงก์ภายนอก
- `app.js`: UI, Navigation, Progress, การตรวจคำตอบ และ LocalStorage
- `worker.js`: Pyodide Runtime ใน Worker เพื่อจำกัดเวลารัน
- `style.css`: Responsive UI

## ขั้นต่อไปสำหรับใช้งานหลายคน

เพิ่มระบบยืนยันตัวตนและฐานข้อมูล Firebase/Supabase พร้อมสิทธิ์ครู/นักเรียน กำหนด RLS หรือ Security Rules และเชื่อม Google Forms/Sheets ผ่าน API ที่ได้รับอนุญาต หลีกเลี่ยงการเก็บข้อมูลส่วนบุคคลที่ไม่จำเป็น
