# Shobot — แผนงาน (Phase 0)

repo `Shobot-ai` ว่างเปล่า จึงสร้างใหม่จากศูนย์ ฟีเจอร์ที่เอกสารเรียกว่า "เดิม" (แชท, โหมดโค้ด, robot avatar, 3D builder, music studio, test area) ยังไม่มีอยู่ ต้องสร้างด้วย

## สภาพแวดล้อมที่ตรวจแล้ว (ใน cloud session ของผม ไม่ใช่เครื่องคุณ)
| รายการ | สถานะ |
|---|---|
| Node 22 / npm 10 / Git | มี |
| JDK | มี (ยังไม่ได้ตรวจว่าเป็น 17+) |
| Android SDK | **ไม่มี** (ต้องใช้ใน Phase 3; build APK ต้องทำบนเครื่องคุณ หรือตั้งค่าเพิ่ม) |
| Vercel CLI | ไม่มี |
| สแกน key รั่ว | repo ว่าง ไม่มีอะไรให้รั่ว |

## Stack ที่เสนอ (ยังไม่ลงมือ)
- เว็บ: Next.js (App Router) + TypeScript + Tailwind, deploy บน Vercel
- AI: OpenRouter, โมเดล Claude Sonnet 5.5, streaming + tool calling
- Test: Vitest, lint: ESLint
- Android: Kotlin + Jetpack Compose ใน `android/` (Phase 3)

## แผนแต่ละ Phase
- **Phase 1 — สมอง + ฐานแอป**: scaffold Next.js, หน้าแชท/โหมดโค้ด, `lib/shobot/prompts/` (CORE/CHAT/CODE/TOOLS/PHONE/REVIEWER ตามเอกสาร), ข้อมูลสด (เวลา Asia/Bangkok), reasoning, prompt caching, ค้นเว็บ, รอบตรวจโค้ด (สูงสุด 2 รอบ), พรีวิว + auto-fix error (สูงสุด 3 รอบ), test
- **Phase 1.5 — ฟีเจอร์ที่ยังไม่มี**: robot avatar, 3D builder, music studio, test area (บอกรายละเอียดที่อยากได้ก่อน)
- **Phase 2 — MCP**: `@modelcontextprotocol/sdk`, Streamable HTTP, หน้าตั้งค่าแอปที่เชื่อมต่อ, เก็บ token เข้ารหัส AES-GCM, agent loop (25 รอบ/30 วิ/ตัด 20,000 ตัวอักษร), ปุ่มอนุญาต, `/api/mcp-test`
- **Phase 3 — Shobot Hands (Android)**: AccessibilityService, FinanceGuard + unit test, จับคู่ด้วยรหัส 6 หลัก, relay WebSocket, ปุ่ม STOP, log
- **Phase 4 — ทดสอบ/deploy**: `docs/TEST_REPORT.md`, รายการ env vars, README

## env vars ที่จะใช้ (ชื่อเท่านั้น)
`OPENROUTER_API_KEY`, `ENCRYPTION_KEY`, ค่าของ database/auth/relay ตามที่เลือกด้านล่าง

## ต้องให้คุณเลือก (แก้ทีหลังยาก/มีค่าใช้จ่าย)
1. **Database**: (ก) Supabase Postgres — ฟรี tier, รวม auth + realtime ในที่เดียว (ข) Neon/Vercel Postgres + Drizzle — เรียบง่าย ต้องหา auth/realtime แยก (ค) Turso/SQLite — ถูกสุด แต่ไม่มี realtime
2. **Login**: (ก) Supabase Auth (ข) Auth.js (NextAuth) + Google login (ค) Clerk — ใช้ง่ายสุด แต่ผู้ใช้เยอะแล้วเสียเงิน
3. **Relay มือถือ**: (ก) Supabase Realtime — ถ้าเลือก Supabase ก็ไม่เพิ่มบริการ (ข) Ably — ฟรี tier จำกัด (ค) Node เล็กๆ บน Railway/Fly — คุมเองได้ ~ $5/เดือน
4. ฟีเจอร์ avatar / 3D / music: ต้องการแบบไหน (เช่น 3D ใช้ three.js, music ใช้ Web Audio)?
5. คุณมี Android SDK + JDK 17 บนเครื่องหรือยัง? จะ build APK เองไหม
6. ใช้ repo `Shobot-ai` ต่อ และ Vercel project ชื่ออะไร?
