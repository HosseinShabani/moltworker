# OpenClaw Migration Tasks

This document tracks the migration from Moltbot/Clawdbot to OpenClaw branding and the latest OpenClaw version.

## ✅ PHASE 1: COMPLETED - Refactoring

All Phase 1 tasks have been completed. The following changes were made:

### 1. Dockerfile ✅

- Changed `npm install -g clawdbot@latest` → `npm install -g openclaw@latest`
- Updated config directory paths from `~/.clawdbot` to `~/.openclaw`
- Renamed startup script reference from `start-moltbot.sh` to `start-openclaw.sh`
- Renamed template file reference from `moltbot.json.template` to `openclaw.json.template`

### 2. start-openclaw.sh (formerly start-moltbot.sh) ✅

- Created new file with all clawdbot CLI commands changed to openclaw
- Updated all config paths from `~/.clawdbot` to `~/.openclaw`
- Changed backup directory from `/data/moltbot` to `/data/openclaw`
- Updated environment variables (`CLAWDBOT_*` → `OPENCLAW_*`)
- Deleted old `start-moltbot.sh`

### 3. openclaw.json.template (formerly moltbot.json.template) ✅

- Created new template file
- Deleted old `moltbot.json.template`

### 4. src/config.ts ✅

- Renamed `MOLTBOT_PORT` → `OPENCLAW_PORT`
- Updated `R2_MOUNT_PATH` from `/data/moltbot` to `/data/openclaw`
- Updated `R2_BUCKET_NAME` from `moltbot-data` to `openclaw-data`
- Updated comments

### 5. src/types.ts ✅

- Renamed `MoltbotEnv` → `OpenClawEnv`
- Renamed `MOLTBOT_BUCKET` → `OPENCLAW_BUCKET`
- Renamed `MOLTBOT_GATEWAY_TOKEN` → `OPENCLAW_GATEWAY_TOKEN`
- Renamed `CLAWDBOT_BIND_MODE` → `OPENCLAW_BIND_MODE`

### 6. Gateway Files ✅

- **src/gateway/env.ts**: Updated imports, changed env var names (`CLAWDBOT_*` → `OPENCLAW_*`)
- **src/gateway/process.ts**: Renamed functions (`findExistingMoltbotProcess` → `findExistingOpenClawProcess`, `ensureMoltbotGateway` → `ensureOpenClawGateway`), updated CLI commands
- **src/gateway/r2.ts**: Updated imports, comments
- **src/gateway/sync.ts**: Updated all paths from `clawdbot` to `openclaw`
- **src/gateway/index.ts**: Updated exported function names

### 7. Routes Files ✅

- **src/routes/api.ts**: Changed all `clawdbot` CLI commands to `openclaw`, updated imports
- **src/routes/debug.ts**: Changed all `clawdbot` CLI commands to `openclaw`, updated paths
- **src/routes/public.ts**: Updated service name from `moltbot-sandbox` to `openclaw-sandbox`
- **src/routes/cdp.ts**: Updated `MoltbotEnv` → `OpenClawEnv`

### 8. src/index.ts ✅

- Updated all Moltbot references to OpenClaw
- Updated imports to use new function names
- Updated environment variable names

### 9. Auth Files ✅

- **src/auth/middleware.ts**: Updated `MoltbotEnv` → `OpenClawEnv`

### 10. Package Configuration ✅

- **package.json**: Renamed project from `moltbot-sandbox` to `openclaw-sandbox`, updated bindings
- **wrangler.jsonc**: Renamed project, updated bucket binding, updated comments
- **.dev.vars.example**: Updated env var names

### 11. HTML Templates ✅

- **src/assets/loading.html**: Updated Moltworker → OpenClaw
- **src/assets/config-error.html**: Updated Moltworker → OpenClaw
- **index.html**: Updated page title

### 12. React Components ✅

- **src/client/App.tsx**: Updated header and logo alt text
- **src/client/pages/AdminPage.tsx**: Updated README link

### 13. Documentation ✅

- **README.md**: Complete rewrite with OpenClaw branding, updated all links, environment variables, and paths
- **AGENTS.md**: Complete rewrite with OpenClaw branding, updated architecture, commands, and paths
- **skills/cloudflare-browser/SKILL.md**: Updated config file reference

### 14. Test Files ✅

- **src/test-utils.ts**: Updated `MoltbotEnv` → `OpenClawEnv`, updated paths
- **src/gateway/env.test.ts**: Updated env var names
- **src/gateway/process.test.ts**: Updated function names and CLI commands
- **src/gateway/r2.test.ts**: Updated bucket name and mount paths
- **src/gateway/sync.test.ts**: Updated paths
- **src/auth/middleware.test.ts**: Updated type references

---

## PHASE 2: Test and Verification

### Completed ✅

- [x] Run test suite (`npm test`) - 64 tests pass
- [x] TypeScript check (`npm run typecheck`) - No errors

### Remaining (Manual Testing Required)

- [ ] Build project (`npm run build`)
- [ ] Local testing (`npm run start` or `wrangler dev`)
- [ ] Test deployment (`npm run deploy`)
- [ ] Verify R2 backup/restore functionality
- [ ] Verify CLI commands work with `openclaw`
- [ ] Review documentation updates

---

## Summary of Changes

### Naming Changes

| Old Name        | New Name         |
| --------------- | ---------------- |
| Moltbot         | OpenClaw         |
| Clawdbot        | OpenClaw         |
| Moltworker      | OpenClaw         |
| moltbot-sandbox | openclaw-sandbox |
| MoltbotEnv      | OpenClawEnv      |
| MOLTBOT\_\*     | OPENCLAW\_\*     |
| CLAWDBOT\_\*    | OPENCLAW\_\*     |
| ~/.clawdbot     | ~/.openclaw      |
| /data/moltbot   | /data/openclaw   |
| moltbot-data    | openclaw-data    |

### Files Created

- `start-openclaw.sh`
- `openclaw.json.template`

### Files Deleted

- `start-moltbot.sh`
- `moltbot.json.template`

### Key Environment Variable Changes

| Old Name               | New Name               |
| ---------------------- | ---------------------- |
| MOLTBOT_GATEWAY_TOKEN  | OPENCLAW_GATEWAY_TOKEN |
| MOLTBOT_BUCKET         | OPENCLAW_BUCKET        |
| CLAWDBOT_BIND_MODE     | OPENCLAW_BIND_MODE     |
| CLAWDBOT_DEV_MODE      | OPENCLAW_DEV_MODE      |
| CLAWDBOT_GATEWAY_TOKEN | OPENCLAW_GATEWAY_TOKEN |

### CLI Command Changes

| Old Command              | New Command              |
| ------------------------ | ------------------------ |
| clawdbot gateway         | openclaw gateway         |
| clawdbot devices list    | openclaw devices list    |
| clawdbot devices approve | openclaw devices approve |
| clawdbot --version       | openclaw --version       |
