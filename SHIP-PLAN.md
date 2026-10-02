# 10th Mountain Link Hub — Stack + Cloudflare ship plan

**Status:** craft artifact ready at `/workspace/10th-mtn-hub/` · zip `/workspace/10th-Mountain-Link-Hub.zip`  
**Sequence (do not reorder):** **craft → RedTeam preview gate → Ace 1:1 `gh` push → Cloudflare hostname last**  
**DNS / CF hostname does not block** craft or RT preview. Hold create/push until Ace 1:1 `gh` auth; attach CF hostname after Pages is up — do **not** wait on DNS to ship the craft or run the RT gate.  
**Not done until:** live on Tony’s Cloudflare domain + RedTeam PASS  
**GitHub org/user:** **Valorius1** (Tony)  
**Repo name:** `Valorius1/10th-mtn-link-hub` (**confirmed Tony**) — **hold push** until Ace 1:1 `gh` auth (hostname can follow)  
**Visibility:** **private** (RedTeam lean locked until public gate after disclaimer/UI PASS)  
**Domain:** TBD — existing Cloudflare zone + hostname (last; non-blocking for RT preview)

---

## 1. What we build with (and why)

| Choice | Decision |
|--------|----------|
| **Stack** | **Static HTML + CSS (+ tiny JS only if needed later)** |
| **Framework** | **None** (no Astro / Next / Workers SSR) |
| **Why** | SoT link-inventory hub: fixed URL list, status badges, quarantine section. No CMS, no auth, no API, no build step. |

Already built under `/workspace/10th-mtn-hub/` with RedTeam fences.

**Not recommending:** Workers runtime, R2+custom CDN, Astro/Next for v1.

---

## 2. Cloudflare path (RedTeam FIX 2026-10-02)

**Primary: Cloudflare Pages connected to a Valorius1 GitHub repo**  
**Fallback:** Pages Direct Upload (dashboard drag-drop) if Git path blocked

| Option | Use? | Why |
|--------|------|-----|
| **Pages ↔ GitHub (Valorius1)** | **YES — prefer** | Tony wants linked GitHub; continuous deploys on push; Source of truth in repo |
| Pages Direct Upload | Fallback | No Git needed; dashboard only |
| Workers / R2 | No for v1 | Overkill |

Docs: [Pages Git integration](https://developers.cloudflare.com/pages/get-started/git-integration/) · [Direct Upload](https://developers.cloudflare.com/pages/get-started/direct-upload/)

### Deploy steps **Tony owns**

1. **Name exact repo** (e.g. `10th-mtn-link-hub`) + **public vs private** + **Cloudflare hostname**.  
   Web/Ace **hold create/push** until Tony confirms the exact name.

2. **GitHub (Valorius1)**  
   - Create **one new repo** under Valorius1 with that exact name (or approve Web to create after name is locked).  
   - Visibility = Tony’s choice.  
   - **README must include unofficial disclaimer** (not DoD / Army / 10th MTN endorsed).  
   - **No force-push / no `--no-verify`.** Do **not** touch other Valorius1 repos.

3. **Cloudflare ↔ GitHub OAuth**  
   - Tony owns approve/connect in dashboard (Workers & Pages → Create → Connect to Git → Valorius1 repo).  
   - **No token paste in Ace+RedTeam.** Group room can’t do sign-in handoff; Ace **1:1** if CLI `gh` needed.

4. **Pages project settings (static)**  
   - Framework preset: **None**  
   - Build command: *(empty)*  
   - Build/output directory: `/` (or repo root where `index.html` lives)  
   - Production branch: `main`  
   - First deploy → `*.pages.dev`

5. **Custom domain**  
   - Project → Custom domains → Tony’s hostname on existing CF zone → SSL active.

6. **Verify + RedTeam gate**  
   - Unofficial banner above fold; spot-check buckets + quarantine; RT PASS before “done.”

### Fallback: Direct Upload (no Git)

Dash → Workers & Pages → Create → Drag and drop `10th-mtn-hub/` folder → Custom domain. Same fences.

### Optional Wrangler / `gh` assist (Ace 1:1 only)

```bash
# Only after Tony names repo + visibility; never paste secrets in Ace+RedTeam
# Prefer dashboard Git connect; CLI only if Tony asks Ace 1:1
npx wrangler pages deploy /workspace/10th-mtn-hub --project-name=<pages-project>
```

---

## 3. Not a mockup — handoff artifact

| Item | Path |
|------|------|
| Site folder | `/workspace/10th-mtn-hub/` |
| README | `/workspace/10th-mtn-hub/README.md` (unofficial disclaimer) |
| Desktop zip | `/workspace/10th-Mountain-Link-Hub.zip` |
| Local preview | `http://127.0.0.1:57971/` (if server up) |
| This plan | `/workspace/10th-mtn-hub/SHIP-PLAN.md` |

“Open HTML once” ≠ done. Done = GitHub (if using Git path) + custom domain live + RedTeam PASS.

---

## 4. Secrets / auth

- **No Cloudflare API token and no GitHub PAT in Ace+RedTeam.**  
- Tony owns GitHub↔Cloudflare OAuth/approve in the dashboard.  
- CLI `gh` / Wrangler tokens → **Ace 1:1 secret-request** only.

---

## 5. Cursor / paid tools

- Cursor (Ultra) + Cloudflare Pages free + GitHub on Valorius1 — **$0 new**.  
- Nothing else unless Tony asks; then name cost once for Subscriptions.

---

## 6. Fences (unchanged)

Unofficial banner · SoT-only URLs · no scraped soldier photos · dark/black-ops · quarantine “Not the division” · live stamp badges · no OPSEC essay · README not Army-endorsed.

---

## 7. Git hygiene (RedTeam)

- Confirm **exact repo name** with Tony before create/push.  
- **No force-push / no `--no-verify`.**  
- Don’t touch other Valorius1 repos.  
- One commit stream for this hub only.

---

## Sequence note (RT)

1. **Craft** (this folder + zip) — done / polish for RT  
2. **RedTeam preview gate** — local preview + shot; **do not block on DNS**  
3. **Ace 1:1 `gh` push** — create/push `Valorius1/10th-mtn-link-hub` only after Ace 1:1 auth  
4. **Cloudflare hostname last** — Pages `*.pages.dev` first, custom domain when Tony names hostname  

## Blockers (waiting)

1. ~~Exact Valorius1 repo name~~ → `Valorius1/10th-mtn-link-hub`  
2. ~~Public vs private~~ → **private** (until post-PASS public gate)  
3. **Ace 1:1 `gh` auth** before create/push (no device-code in Ace+RedTeam room)  
4. **Cloudflare hostname** (zone + subdomain or apex) — **last; does not block RT preview**
