# ATOMVERSE 2.0 — ATOM FORGE (LAB 01)

โปรเจกต์ใหม่แบบ React + TypeScript + Vite + React Three Fiber/Three.js สำหรับนักเรียนเคมี ม.4

## สถานะงาน (สำคัญ)

- ✅ มีซอร์สโค้ดหน้าแรก Luminous Hybrid Lab, โมเดล Three.js, เครื่องมือควบคุม, เปรียบเทียบ A/B, 5 missions, และระบบคำนวณแยกต่างหาก
- ✅ ทดสอบตรรกะเคมีจริง 16 กรณี (ด้วย Node.js type-stripping) และผ่าน 16/16
- ⚠️ **ยังไม่ได้ Build หรือทดสอบ UI ใน browser จริง** เพราะสภาพแวดล้อมที่สร้างไฟล์ไม่สามารถเข้าถึง npm registry เพื่อดาวน์โหลด React/Three.js/Vite ได้ (`EAI_AGAIN`). จึงไม่ควรถือว่า deploy-ready จนกว่าจะ `npm install`, `npm run build` และทดลอง UI ผ่าน
- ⚠️ รองรับการลากอนุภาคจากถาดลงพื้นที่เวทีด้วย HTML drag-and-drop สำหรับ desktop; มือถือให้แตะอนุภาคหรือกด +/- (ยังไม่มี touch-drag จริง)
- ⚠️ fallback เมื่อ WebGL ใช้ไม่ได้ยังเป็นข้อความพร้อมค่าทางเคมี/ตัวควบคุม ไม่ใช่ 2D interactive scene เต็มรูปแบบ

## ติดตั้งบนเครื่อง Windows/Mac

1. ติดตั้ง **Node.js 22** (หรือ Node 20.19+)
2. แตก ZIP แล้วเปิด Terminal / PowerShell ในโฟลเดอร์ที่มี `package.json`
3. รัน:

```bash
npm install
npm test
npm run dev
```

4. เปิด URL ที่ Vite แจ้ง (ทั่วไปคือ `http://localhost:5173/`)
5. ก่อนอัปโหลด ควรทดสอบ `npm run build` ถ้าผ่านจะเกิด `dist/`

**อย่าเปิด `index.html` โดยดับเบิลคลิก** เพราะโปรเจกต์นี้ต้อง build ด้วย Vite (ต่างจากรุ่นก่อนที่เป็น HTML static)

## GitHub Pages (วิธีแนะนำ: GitHub Actions)

1. สร้าง public repository ใหม่ เช่น `atomverse-2`
2. อัปโหลด **เนื้อหาในโฟลเดอร์โปรเจกต์** ขึ้น root ของ repository: `package.json`, `index.html`, `src/`, `.github/workflows/deploy.yml` ฯลฯ
3. เปิด **Settings > Pages > Build and deployment > Source > GitHub Actions**
4. เมื่อ Push ไปที่ `main` ระบบ workflow จะติดตั้ง dependency, ทดสอบ engine, build และ deploy หากขั้นตอนใดล้มเหลวจะไม่เผยแพร่
5. URL ควรเป็น `https://<username>.github.io/atomverse-2/` ตามชื่อ repository ของตน

ตั้ง `base:'./'` ใน `vite.config.ts` เพื่อใช้ asset แบบ relative path รองรับ project pages

## วิธีเล่น

- เปิด LAB 01 (ปุ่มใหญ่หน้าแรก)
- ปรับ p⁺, n⁰, e⁻ ด้วยปุ่ม `+/-` หรือคลิกที่อนุภาคในถาดด้านล่าง (บนเดสก์ท็อปสามารถลากจากถาดมาวางบนเวทีได้)
- เปิด “เปรียบเทียบ A/B” เพื่อดูอะตอมสองตัวพร้อมกัน แล้วสลับฝั่งที่จะปรับบนแผงควบคุม
- เลือก Preset C-12, C-13, H-1, H-2, O-16, Cl-35, Cl-37
- กดหมายเลขภารกิจ 1–5, ทดลองด้วยตัวเอง ระบบตรวจสถานะ atom A/B โดยไม่ต้องพิมพ์

## ขอบเขตทางวิทยาศาสตร์

- เลขอะตอม Z = โปรตอน, เลขมวล A = โปรตอน + นิวตรอน, ประจุสุทธิ = โปรตอน − อิเล็กตรอน
- มวลไอโซโทปเป็นค่าที่แยกจากเลขมวล และแสดงเฉพาะค่าจากตารางข้อมูลที่ฝังในระบบ สำหรับไอโซโทปที่ไม่อยู่ในชุดข้อมูลแสดงว่า **ไม่มีค่าที่ตรวจสอบแล้ว** ไม่ใช้ A เป็นมวลจริง
- มวลไอโซโทปอะตอมเป็นกลางในหน่วย unified atomic mass unit (u) ตามตาราง mass datasets; ในกรณีไอออนมีความคลาดเคลื่อนเล็กน้อยจากมวลอิเล็กตรอน/พลังงานยึดเหนี่ยว ค่าในจอจึงเรียก 'มวลไอโซโทป' และไม่มีการชดเชยมวลไอออน
- ตำแหน่งโปรตอนและนิวตรอนใน 3D ถูกจัดด้วย algorithm เพื่อให้เห็นภาพ ไม่ใช่รูปร่างนิวเคลียสจริง
- ผิวทรงกลมและเส้นบาง ๆ เป็น **องค์ประกอบช่วยมองเห็นขอบเขตของแบบจำลอง** ไม่ใช่เส้นทางโคจรจริงของอิเล็กตรอน; ไม่ได้แสดง quantum orbitals หรือ electron-density solution ที่คำนวณจากสมการ Schrödinger
- จำนวนโปรตอนรองรับ Z = 1 ถึง 20 และอนุภาคอีกสองชนิดไม่เกิน 40 ต่อชนิด เป็นช่วงฝึกฝน ไม่ใช่ทุกสถานะที่สร้างจะเป็นนิวไคลด์ที่เสถียรหรือพบได้จริง

**แหล่งอ้างอิงสำหรับตรวจสอบและขยายชุดข้อมูล:**
- NIST Atomic Weights and Isotopic Compositions: https://physics.nist.gov/PhysRefData/Compositions/
- CIAAW Isotopic Abundances: https://ciaaw.org/isotopic-abundances.htm

## โครงสร้าง

```
index.html
vite.config.ts
package.json
tsconfig.json
src/
  main.tsx
  App.tsx
  styles/app.css
  components/AtomScene.tsx
  chemistry/atom.ts
tests/chemistry.test.mjs
.github/workflows/deploy.yml
```

## Next iterations (not yet complete)

1. ทำ browser E2E test ครอบคลุม mouse/touch, WebGL, mobile responsiveness
2. ตรวจและ optimize GPU performance จริงโดย profiling บนเครื่องนักเรียน
3. เพิ่ม touch drag-and-drop และ accessible keyboard drag alternatives
4. เพิ่ม fallback canvas/SVG 2D แบบ interactive เต็มรูปแบบ
5. สร้าง data validation อ้างอิง isotope mass source ที่ตรวจสอบโดยตรงทั้งชุด
6. เพิ่มการบันทึกความคืบหน้าและยกระดับการใช้เสียง/animation ให้มีความหมาย
7. ขยาย LAB 02/03/04 โดยใช้ calculation engine แยกจาก visualizations
