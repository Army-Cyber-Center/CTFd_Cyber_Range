# Pixo Theme — Event Branding (git-native, pre-setup)

รูป branding ทุกตัวถูก wire แบบ **"DB ก่อน → ถ้าไม่มีค่อย fallback ไปโฟลเดอร์ git"**
โฟลเดอร์ pre-setup อยู่ที่: **`static/img/brand/`**

> แต่ละ event: แก้/วางทับรูปใน `static/img/brand/` แล้ว commit — clone ไปก็ใช้ได้ทันที
> ถ้า event ไหนอยากใช้รูปเฉพาะกิจ ก็อัปผ่าน Admin > Config ได้ (DB จะ override ให้เอง)

## ลำดับความสำคัญของแต่ละรูป

| รูป | DB (อัปผ่าน Admin > Config) | Fallback (โฟลเดอร์ git) | wire ที่ |
|---|---|---|---|
| โลโก้ navbar | `ctf_logo` | `static/img/brand/logo.png` | `templates/components/navbar.html` |
| Favicon | `ctf_small_icon` | `static/img/brand/favicon.png` | `templates/base.html` |
| Cover/Hero (หน้า home) | `ctf_banner` | `static/img/brand/cover.png` | `templates/page.html` |
| พื้นหลัง login/register | _(ไม่มี DB field)_ | `static/img/brand/login-bg.png` | `templates/login.html`, `templates/register.html` |

- **logo / favicon / cover**: ถ้ามีค่าใน DB → ใช้ DB, ไม่มี → ใช้ไฟล์ในโฟลเดอร์
- **login-bg**: CTFd ไม่มี config ใน DB สำหรับพื้นหลัง login → เป็น **folder-only** (เปลี่ยนได้ที่ไฟล์เท่านั้น)
- ค่า default ปัจจุบัน = ตรา **Army Cyber Center** (ดึงมาจาก ctf.rtacyber.club / RTA CTF 2026)
- `login-bg.png` ใช้โลโก้ไปก่อน — แนะนำหารูป **กว้างๆ (banner)** มาแทนเพื่อให้พื้นหลังสวยกว่า (style เป็น `background-size: cover`)
- `brand/boss.png` = ภาพ portrait ผู้บังคับบัญชา (ไม่ได้ wire ใน template) เอาไปแทรกใน content หน้า home เองได้

## ⚠️ Cover/Hero: กันรูปซ้ำ
ตอนรัน **setup wizard** ครั้งแรก CTFd จะ **ฝัง `<img>` banner ลงใน content ของหน้า home** (เก็บใน DB Page)
ถ้าปล่อยไว้ hero ของธีมจะซ้ำกับรูปใน content → ให้เลือกทำอย่างใดอย่างหนึ่ง:
- **(แนะนำ)** ไป Admin > Pages > แก้หน้า home ให้เหลือ **เฉพาะข้อความ** (ลบ `<img>` ออก) แล้วปล่อยให้ธีม render cover ให้
- หรือถ้าจะใช้ banner จาก content เอง ก็ลบ/คอมเมนต์ hero block ใน `templates/page.html`

## Workflow ต่อ event
```
git clone <repo> ctfd-<event>
cd ctfd-<event>
# วางรูปทับใน CTFd/themes/pixo/static/img/brand/  (logo.png / favicon.png / cover.png / login-bg.png)
docker compose up -d
# Admin > Config > Themes > เลือก "pixo" > Update
# (ออปชัน) หน้า home: Admin > Pages > ทำให้เป็น text-only
```

## หมายเหตุ
- Hero แสดงเฉพาะหน้า `/` (เช็คด้วย `request.path`) ไม่เลอะ custom page อื่น
- พื้นหลัง login ใช้ inline `style` (ไม่ต้อง build CSS) ปรับ `background-size`/`background-position` ได้ในไฟล์ template
- **ข้อความ/เนื้อหา** หน้า home เป็น CTFd "Page" เก็บใน DB (ไม่ใช่ git) — ถ้าอยากเก็บทั้งงานเป็น baseline ใช้ `export.py`/`import.py`
