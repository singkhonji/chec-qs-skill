# CHEC QS Skill — Marketplace สำหรับทีม

Marketplace สาธารณะของ Claude Code สำหรับทีม CHEC — เครื่องมือ QS งานก่อสร้าง, ประมวลผลเอกสาร, และ workflow โครงการ ติดตั้งครั้งเดียว เลือก plugin ได้ตามต้องการ

## วิธีเพิ่ม Marketplace

ใน Claude Code → Manage Plugins → Marketplaces → Add:

```bash
https://github.com/singkhonji/chec-qs-skill
```

จากนั้นไปที่แท็บ **Plugins** เพื่อดูและติดตั้ง plugin ที่มีอยู่

---

## การเพิ่ม Plugin ใหม่ (สำหรับทีม)

สมาชิกในทีมสามารถเพิ่ม plugin ได้ตามโครงสร้างนี้

### 1. สร้างโฟลเดอร์ plugin

```text
plugins/
└── ชื่อ-plugin/
    ├── .claude-plugin/
    │   └── plugin.json       ← metadata จำเป็นต้องมี
    └── skills/
        └── ชื่อ-plugin/
            └── SKILL.md      ← นิยาม skill
```

### 2. รูปแบบ plugin.json

```json
{
  "name": "ชื่อ-plugin",
  "description": "ประโยคเดียว — plugin นี้ทำอะไร",
  "author": {
    "name": "ชื่อของคุณ",
    "email": "email@example.com"
  }
}
```

### 3. รูปแบบ SKILL.md

```markdown
---
name: ชื่อ-plugin
description: >
  Claude ควรใช้ skill นี้เมื่อไหร่?
  ระบุ trigger phrases, คำสั่ง, หรือเงื่อนไขที่ควรใช้
  ยิ่ง trigger ชัดเจน ยิ่งทำงานได้แม่นยำขึ้น
---

# ชื่อ Plugin

[คำสั่งสำหรับ Claude — ต้องทำอะไรเมื่อถูก invoke]
```

**Model-invoked skill** (Claude เลือกใช้เองตาม context):
- เขียน trigger phrase ที่เป็นธรรมชาติในฟิลด์ `description`

**User-invoked slash command** (ผู้ใช้พิมพ์ `/ชื่อ-plugin`):
- เพิ่ม `argument-hint: <arg>` ใน frontmatter

### 4. ลงทะเบียนใน marketplace.json

เพิ่ม entry ใน `.claude-plugin/marketplace.json` ภายใต้ `"plugins"`:

```json
{
  "name": "ชื่อ-plugin",
  "description": "ประโยคเดียวเหมือนกับ plugin.json",
  "author": {
    "name": "ชื่อของคุณ",
    "email": "email@example.com"
  },
  "category": "productivity",
  "source": {
    "source": "git-subdir",
    "url": "https://github.com/singkhonji/chec-qs-skill.git",
    "path": "plugins/ชื่อ-plugin",
    "ref": "main"
  }
}
```

### 5. Commit และ Push

```bash
git add plugins/ชื่อ-plugin .claude-plugin/marketplace.json README.md README_TH.md
git commit -m "Add plugin: ชื่อ-plugin"
git push
```

---

## รายการ Plugin

| Plugin | คำอธิบาย |
| --- | --- |
| *(ยังไม่มี plugin — มาเป็นคนแรกที่ contribute!)* | |

---

## โครงสร้าง Repo

```text
chec-qs-skill/
├── .claude-plugin/
│   └── marketplace.json      ← ดัชนี marketplace
├── plugins/
│   └── <ชื่อ-plugin>/        ← หนึ่งโฟลเดอร์ต่อหนึ่ง plugin
│       ├── .claude-plugin/
│       │   └── plugin.json
│       └── skills/
│           └── <ชื่อ-skill>/
│               └── SKILL.md
├── README.md                 ← คู่มือภาษาอังกฤษ
└── README_TH.md              ← คู่มือภาษาไทย (ไฟล์นี้)
```
