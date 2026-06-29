# brand/ — per-event branding images

วางรูปของแต่ละงานทับไฟล์เหล่านี้ (ชื่อไฟล์ต้องตรงตามนี้):

| ไฟล์ | ใช้ที่ | ถ้ามีค่าใน DB จะ override |
|---|---|---|
| `logo.png`      | โลโก้ navbar          | `ctf_logo` (Admin > Config) |
| `favicon.png`   | favicon บน browser    | `ctf_small_icon` |
| `cover.png`     | hero หน้า home (`/`)  | `ctf_banner` |
| `login-bg.png`  | พื้นหลัง login/register | — (folder-only) |
| `boss.png`      | รูปประกอบ (ไม่ได้ wire) — เอาไปใส่ใน content หน้า home เองได้ | — |

ค่า default ปัจจุบัน = ตรา Army Cyber Center (RTA CTF 2026)

ดูรายละเอียด + ข้อควรระวังเรื่องรูปซ้ำที่ `../../../BRANDING.md`
