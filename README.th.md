# Codex with ChatGPT

> ChatGPT คิดและวางแผน ส่วน Codex ลงมือทำ

[English](README.md) | **ภาษาไทย**

> [!IMPORTANT]
> **มีปัญหาใช่ไหม?** ลองบอก Codex ว่า **“Update Codex with ChatGPT”** แล้วลองใหม่ก่อน การอัปเดตเป็นเวอร์ชันล่าสุดช่วยแก้ปัญหาที่พบบ่อยได้ส่วนใหญ่

## โปรเจกต์นี้แก้ปัญหาอะไร

หลายคนมี ChatGPT Plus/Pro อยู่แล้ว แต่ใช้ ChatGPT Web สำหรับการวางแผนและรีวิวโค้ดไม่เต็มที่ ขณะเดียวกัน Codex ต้องใช้โควตาหรือเครดิตสำหรับงานคิด วางแผน และตรวจงาน

โปรเจกต์นี้จึงแยกหน้าที่ดังนี้:

- **ChatGPT Web**: ทำความเข้าใจปัญหา วางแผน และรีวิว
- **Codex**: แก้ไฟล์ รัน shell, git และ tests

ไม่ต้องใช้ API key และไม่ทำ reverse proxy ให้ ChatGPT แต่ใช้ ChatGPT Web อย่างเป็นทางการร่วมกับ MCP bridge แบบอ่านอย่างเดียว

## มันคืออะไร

`Codex with ChatGPT` เปลี่ยน ChatGPT Web ให้เป็น “สมองสำหรับวางแผนและรีวิว” ของเซสชัน Codex โดยสิทธิ์ในการลงมือทำยังอยู่กับ Codex ทั้งหมด

ChatGPT จะไม่สามารถแก้ไฟล์หรือรันคำสั่งในเครื่องได้โดยตรง แต่จะอ่านข้อมูลที่จำเป็นจาก workspace ปัจจุบันผ่าน MCP connector แบบ read-only เช่น ไฟล์ที่เกี่ยวข้อง ผลค้นหา git diff และบันทึกการทดสอบ

> หมายเหตุด้านความเป็นส่วนตัว: โปรเจกต์นี้ไม่มีขั้นตอนอัปโหลดทั้ง repository เป็นก้อน แต่ข้อมูลที่ ChatGPT ขออ่าน เช่น source code, diff หรือผลค้นหา จะถูกส่งไปให้ ChatGPT เพื่อวิเคราะห์ตามปกติ อย่าใช้กับ repository ที่มี secret หรือข้อมูลอ่อนไหวโดยไม่ตรวจสอบนโยบายก่อน

## ติดตั้งแบบวางครั้งเดียว

ถ้าไม่คุ้นกับ git, Node หรือ terminal สามารถคัดลอกข้อความด้านล่างไปให้ Codex ได้:

```text
ช่วยติดตั้งและตั้งค่า “Codex with ChatGPT” ให้ฉันแบบอัตโนมัติทั้งหมด
ฉันไม่ใช่ผู้ใช้สายเทคนิค ให้จัดการทุกอย่างเอง:

1. ตรวจสอบสภาพแวดล้อม ต้องมี git และ Node.js >= 20 ถ้าขาดให้ติดตั้งเอง
   (macOS ใช้ Homebrew, Windows ใช้ winget) และติดตั้ง cloudflared ด้วย
2. ดาวน์โหลด repository จาก https://github.com/XiaoDuoYa/codex-with-chatgpt
   ไว้ที่ ~/codex-with-chatgpt ถ้ามีอยู่แล้วให้ git pull เพื่ออัปเดต
3. เข้าโฟลเดอร์แล้วรัน `corepack pnpm install` จากนั้น `corepack pnpm build`
4. ติดตั้ง Codex Skill โดยคัดลอก skill/SKILL.md ไปที่
   ~/.codex/skills/codex-with-chatgpt/SKILL.md และแก้บรรทัด
   “The codex-with-chatgpt checkout lives at:” ให้เป็น path จริงของ checkout
5. ตั้งค่าครั้งแรกตาม workflow “first-time setup” ใน SKILL.md
   (รัน c2c setup เปิด ChatGPT connector ด้วยเบราว์เซอร์ในตัว และกรอกรหัสจับคู่)
   ห้ามเปิดเบราว์เซอร์ภายนอกสำหรับขั้นตอน ChatGPT
6. เรียกฉันเฉพาะเมื่อจำเป็นต้อง login เข้า ChatGPT/Cloudflare, ทำ CAPTCHA,
   หรือทำ 2FA และให้บอกฉันทีละหนึ่งขั้นตอนเท่านั้น
7. เมื่อตั้งค่าเสร็จ ให้แสดง checklist และยืนยันว่า file-read test ผ่าน
   ถ้ามีปัญหาให้ลองแก้เองก่อน
```

Skill จะตรวจสอบ GitHub วันละครั้ง หากมีเวอร์ชันใหม่จะอัปเดตตัวเอง และสามารถบอก Codex ว่า **“Update Codex with ChatGPT”** ได้ทุกเมื่อ

## ติดตั้ง → ตั้งค่า → ใช้งานแบบ manual

1. ติดตั้ง Codex Skill โดยคัดลอกโฟลเดอร์ `skill/` ไปที่ `~/.codex/skills/codex-with-chatgpt/`
2. บอก Codex ว่า: **“Set up Codex with ChatGPT.”**
3. ใช้งานตามปกติ เช่น: **“Use Codex with ChatGPT to implement XXX.”**

หลังตั้งค่าสำเร็จ ควรเห็นประมาณนี้:

```text
Codex with ChatGPT

✓ ตรวจพบโปรเจกต์แล้ว
✓ Workspace Bridge เริ่มทำงานแล้ว
✓ สร้างการเชื่อมต่อที่ปลอดภัยแล้ว
✓ เชื่อมต่อ ChatGPT แล้ว
✓ ทดสอบอ่านไฟล์ผ่าน

พร้อมใช้งาน
```

สิ่งที่อาจต้องทำเองมีเพียงการ login เข้า ChatGPT และการ login Cloudflare หากต้องการใช้ hostname แบบคงที่

สำหรับ workspace ใหม่ ระบบอาจขอให้สร้าง ChatGPT Project หนึ่งครั้ง ให้ตั้งชื่อเหมือน workspace และเลือก **project-only memory** เพื่อไม่ให้ความจำของโปรเจกต์อื่นปะปนกัน

### hostname แบบคงที่ (ตัวเลือกเสริม)

ค่าเริ่มต้นใช้ Cloudflare Quick Tunnel ซึ่งสร้างที่อยู่ชั่วคราว ที่อยู่นี้อาจเปลี่ยนเมื่อ bridge restart และระบบจะต้องลบแล้วสร้าง connector ของ workspace นี้ใหม่

ถ้ามี Cloudflare account และมี domain อยู่บน Cloudflare สามารถเลือก hostname แบบคงที่ เช่น `c2c-<project>.your-domain.com` ได้ โดย login และอนุญาต Cloudflare ครั้งแรก หลังจากนั้น connector จะใช้งานต่อได้ง่ายขึ้นเมื่อ restart

ถ้าไม่ต้องการใช้ Cloudflare domain ก็ใช้ temporary address ได้ ฟีเจอร์เหมือนกัน แต่อาจต้องซ่อม connector เมื่อที่อยู่เปลี่ยน

Credential จะเก็บในโฟลเดอร์ state ของระบบปฏิบัติการ ไม่ได้เก็บไว้ใน project

## ทำงานอย่างไร

```text
             ┌───────────────────────────┐
             │       ChatGPT Web         │
             │    คิด / วางแผน / รีวิว    │
             └──────────┬──────────▲─────┘
                        │          │
               MCP     │          │ Computer Use
              data     │          │ control messages (<1 KB)
                        ▼          │
             ┌─────────────────────┐
             │      C2C Bridge     │   HTTP เฉพาะ loopback
             │    MCP read-only    │   OAuth 2.1 + pairing code
             │   OAuth + pairing   │   Cloudflare Quick Tunnel
             │   tunnel manager    │
             └──────────┬──────────┘
                        │ read-only
                        ▼
             ┌─────────────────────┐          ┌─────────────────────┐
             │   Local Workspace   │◀─────────│    Codex Harness    │
             └─────────────────────┘ แก้/git │ shell / tests / fix  │
                                              └─────────────────────┘
```

### Control plane

Codex และ ChatGPT แลกเปลี่ยนข้อความสถานะขนาดเล็ก เช่น:

`INIT → PLAN → EXECUTED → REVIEW → DONE`

ข้อความควบคุมจะไม่ใส่ diff, log หรือเนื้อหาไฟล์ลงไปโดยตรง

### Data plane

ChatGPT อ่านข้อมูลที่ต้องการผ่าน MCP tools แบบ read-only จำนวน 9 รายการ:

- `workspace_info`
- `list_directory`
- `read_file`
- `search_workspace`
- `git_status`
- `git_diff`
- `test_status`
- `execution_summary`
- `execution_output`

### Independent review

หลัง Codex ลงมือทำ ChatGPT จะอ่าน git diff และ test records ผ่าน MCP เพื่อรีวิวผลจริง ไม่เชื่อเพียงข้อความว่า “tests ผ่านทั้งหมด”

## โมเดลความปลอดภัย

- **อ่านอย่างเดียวโดยโครงสร้าง**: ไม่มี tool สำหรับเขียน ลบ รัน shell หรือ commit
- **หนึ่ง workspace ต่อหนึ่งขอบเขต**: token แต่ละชุดผูกกับ workspace เดียว
- **ป้องกัน path escape**: ตรวจ canonical realpath และ block `../`, absolute path และ symlink escape
- **ป้องกันไฟล์อ่อนไหว**: `.env*`, private key, SSH credential และ cloud credential ถูกปฏิเสธโดยค่าเริ่มต้น (`.env.example` ได้รับอนุญาต)
- **URL อย่างเดียวใช้ไม่ได้**: MCP endpoint สาธารณะต้องผ่าน OAuth 2.1, PKCE และ token ที่ถูกต้อง
- **pairing code ใช้ครั้งเดียว**: มีอายุสั้น จำกัดจำนวนครั้ง และถูกทำลายหลังใช้งาน
- **จำกัดปริมาณข้อมูล**: file read, search และ git diff มีขนาดและ pagination limit

Workspace content ต้องถือเป็นข้อมูลที่ไม่น่าเชื่อถือ README, comment หรือ diff ที่เป็น prompt injection ไม่สามารถเพิ่มสิทธิ์ MCP ได้ แต่ยังอาจทำให้โมเดลเสนอแผนที่ไม่ปลอดภัย ดังนั้น Codex และผู้ใช้ควรตรวจแผนก่อนให้ทำงานกับโปรเจกต์สำคัญ

ดู threat model ฉบับเต็มได้ที่ [docs/security.md](docs/security.md)

## สำหรับนักพัฒนา

```bash
pnpm install
pnpm build          # สร้าง dist/ และเปิดใช้คำสั่ง c2c
pnpm test           # Vitest

c2c setup           # bridge + tunnel + pairing code ในคำสั่งเดียว
c2c sandbox-allow   # เพิ่ม state directory เข้า Codex sandbox
c2c status
c2c doctor
c2c pair
c2c unpair
c2c logs
c2c stop
```

ข้อกำหนด:

- Node.js >= 20
- git
- `cloudflared` สำหรับ public connection

ถ้า network บล็อก QUIC ให้ตั้งค่า:

```bash
C2C_TUNNEL_PROTOCOL=http2
```

จากนั้น restart bridge

เอกสารเพิ่มเติม:

- [Architecture](docs/architecture.md)
- [Protocol](docs/protocol.md)
- [Security](docs/security.md)
- [Troubleshooting](docs/troubleshooting.md)

## โครงสร้างโปรเจกต์

```text
src/
  bridge/     HTTP server แบบ loopback, port recovery, admin API
  mcp/        MCP tools แบบ read-only
  auth/       OAuth 2.1, PKCE, dynamic registration, refresh rotation
  pairing/    pairing code, CSPRNG, TTL, rate limits
  workspace/  path containment, sensitive-file policy, search, git
  tunnel/     TunnelProvider และ Cloudflare Quick/Named Tunnel
  execution/ execution records สำหรับ review loop
  process/    daemon lifecycle
  cli/        คำสั่ง c2c
skill/        Codex Skill ซึ่งเป็น UX หลัก
tests/        unit และ integration tests
docs/         architecture / protocol / security / troubleshooting
```

## สถานะและข้อจำกัดความรับผิดชอบ

โปรเจกต์นี้เป็น V1 และมีการตรวจสอบ end-to-end สำหรับ bridge, OAuth + pairing, public tunnel, ChatGPT connector setup และ first-run flow ตามเอกสารของ repository

**นี่เป็น community project ที่ไม่เป็นทางการ ไม่ได้ affiliated กับ OpenAI และไม่ได้รับการรับรองจาก OpenAI**

## License

[MIT](LICENSE)
