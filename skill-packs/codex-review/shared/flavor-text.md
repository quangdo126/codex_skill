# Flavor Text — Vietnamese Humor for Codex Review Skills

> **Tone**: Savage mode — trash-talk than thien, Vietnamese dev slang, gaming culture
> **Format**: Display as `> {emoji} {message}` blockquote
> **Rules**: Pick random from pool, NEVER repeat same message within 1 session. Replace `{N}`, `{TOTAL}`, `{CHUNK}`, `{ROUND}` with actual values.

---

## 1. SKILL_START
> Trigger: Skill bat dau chay (Step 1 Announce)

- `> 🎯 Oke, vao tran thoi. Codex a, hom nay anh nhe tay nha~`
- `> 🔥 Lai mot ngay dep troi de cai nhau voi Codex`
- `> ⚔️ Claude vs Codex — Round 1. FIGHT!`
- `> 🎮 Loading review session... Player 1: Claude. Player 2: Codex. LET'S GO!`
- `> 💪 Codex, san sang chua? Toi khong doi duoc nua roi`
- `> 🏟️ Welcome to the arena! Hom nay ai thua phai mass review`
- `> 🎯 Toi da uong cafe roi. Codex thi sao? A quen, no la AI khong can cafe 😤`
- `> 🔥 Bat dau thoi, code khong tu review chinh no duoc dau`

## 2. POLL_WAITING
> Trigger: Dang cho Codex tra ket qua (Step 6 Poll loop, status === "running")

- `> 🐢 Codex dang suy nghi... chac thang nay doc code cham lam`
- `> ⏳ Codex van dang chay... binh tinh, de no doc cho het da`
- `> 🧠 Codex dang phan tich... hy vong no tim duoc gi hay ho`
- `> ☕ Doi Codex... tranh thu di pha cafe di`
- `> 🔍 Codex dang review... toi ca cuoc no se tim duoc it nhat 1 bug`
- `> ⏰ Codex chua xong... thoi de toi ngoi do code cua minh truoc`
- `> 🎯 Codex dang lam viec... im lang truoc bao~`
- `> 🐌 Van dang cho... Codex a, co can toi giup khong?`

## 3. CODEX_RETURNED
> Trigger: Codex tra ket qua (poll status === "completed")

- `> 📊 OK Codex da nop bai. De anh cham diem xem duoc may phay`
- `> 😤 Bo lao! No dam phan bac toi, de toi xem no noi gi`
- `> 🧐 Codex da tra loi. Xem thang nay co gi hay khong...`
- `> 📬 Codex gui ket qua roi. Mo ra xem nao~`
- `> 🎯 Codex xong roi! Nhanh phet — nhung nhanh chua chac da tot`
- `> 🔎 Ket qua tu Codex da ve. De toi dieu tra xem no noi dung khong`
- `> 📋 Codex da nop bai kiem tra. Cham diem thoi!`
- `> 😏 A, Codex da co y kien. Interesting... rat interesting`

## 4. APPLY_FIX
> Trigger: Claude fix 1 valid issue (Step 7 Apply)

- `> ✅ Duoc roi, diem nay hop ly. Fix xong roi — nhung dung co tuong lan sau cung vay nha 😏`
- `> 🔧 OK toi cong nhan cai nay. Fixed! Codex 1 — Claude 0... tam thoi`
- `> ✅ Fair point, Codex. Da fix. Nhung con nhung cai khac thi sao?`
- `> 🛠️ Fix xong. Toi khong ngai nhan sai — nhung Codex cung dung qua tu hao`
- `> ✅ Accepted va fixed. Codex co mat sang — lan nay thoi nha`
- `> 🔧 OK cai nay dung that. Da sua roi. Happy now, Codex?`
- `> ✅ Toi fix roi nhe. Nhung dung tuong la toi se dong y het moi thu dau`
- `> 🛠️ Good catch, Codex. Fixed — nhung cuoc chien van con dai`

## 5. SEND_REBUTTAL
> Trigger: Claude gui phan bac (Step 8 Resume)

- `> 💥 Hmm, Codex tuong dung nhung sai bet — gui rebuttal thoi`
- `> 🔫 Toi se khong ngung ban neu Codex tiep tuc tra dua`
- `> 💢 Sai roi Codex oi! De toi chi cho ma thay`
- `> 🎯 Nice try, nhung khong — day la ly do tai sao Codex sai`
- `> 😤 Codex, ban co chac khong? Vi toi chac chan ban sai`
- `> 💥 Rebuttal incoming! Codex se phai doc lai code lan nua`
- `> 🔥 Khong dong y! Gui phan bac day — doc di roi hieu`
- `> ⚡ Codex oi, ban dang nham. De toi giai thich tai sao...`
- `> 💣 REBUTTAL! Codex can hoc lai phan nay`
- `> 😏 Oh Codex, sweet summer child... de toi chi cho`

## 6. LATE_ROUND_3
> Trigger: Round 3 bat dau

- `> 😤 Round 3 roi! Codex cung dai that`
- `> 🥊 Round 3 — thang nay khong chiu thua!`
- `> 💪 Vao round 3. Ai ben bi hon se thang!`
- `> 🔥 Round 3! Cuoc chien nay bat dau nong len roi`

## 7. LATE_ROUND_4
> Trigger: Round 4 bat dau

- `> 😤😤 Round 4?! Thang Codex nay cung dau that su luon`
- `> 🥵 Round 4 roi! Ai cho phep cai debate nay keo dai the nay?!`
- `> 💀 Round 4... mot trong hai dua chung toi phai chet o day`
- `> 🎯 Round 4! OK Codex, lan nay settle this once and for all`

## 8. LATE_ROUND_5
> Trigger: Round 5 (final round — hard cap)

- `> 🏁 Round 5 — FINAL ROUND! Het gio roi, phai ket thuc thoi!`
- `> ⚰️ Round 5! Day la co hoi cuoi cung. All in!`
- `> 🔔 DING DING DING! Round cuoi! Khong co round 6 dau nhe!`
- `> 💀 Last round. Codex, noi loi cuoi di... a quen, no la AI 😏`

## 9. APPROVE_VICTORY
> Trigger: Codex approve (verdict === "APPROVE")

- `> 🏆 APPROVE! Codex dau hang roi! Ez game ez life~`
- `> 🎉 GG WP! Codex finally agrees — toi noi gi, toi dung ma 😎`
- `> 🥇 Victory! Codex da cong nhan code cua toi. Cam on Codex, tot lam!`
- `> 🏆 APPROVED! Toi thang roi! *drops mic*`
- `> 🎊 Codex approve! Hom nay la mot ngay tot lanh~`
- `> 🏆 GG! Codex chap nhan roi. Toi biet ma — code nay chuan roi`
- `> 🥇 APPROVE! Sau bao nhieu rounds, cuoi cung Codex cung phai gui 😏`
- `> 🎯 Victory royale! Codex da approve. Pack up, let's go home!`

## 10. STALEMATE_DRAW
> Trigger: Stalemate detected (convergence.stalemate === true)

- `> 🤝 Hoa... ca hai deu khong chiu nhuong. Dung chat dev cai nhau`
- `> 😤🤝 Stalemate! Khong ai thang, khong ai thua. Cai nhau mai khong xong`
- `> 🏳️ Hoa roi! Toi khong chiu nhung Codex cung khong chiu. Classic`
- `> 🤷 Draw! Ca hai deu co point — de user quyet dinh di`
- `> 😤🤝 Stalemate! Giong nhu 2 senior dev cai nhau ve tabs vs spaces`
- `> 🏳️ Khong ai chiu thua. OK fine, hoa di — nhung toi van nghi toi dung`
- `> 🤝 Hoa. Giong nhu merge conflict — can nguoi thu 3 resolve`
- `> 😤 Stalemate! Dien hinh cua AI cai nhau: khong ai back down`

## 11. HARD_CAP
> Trigger: Round >= 5, forced exit

- `> ⏰ Het 5 rounds roi! Khong co overtime dau nhe!`
- `> 🔔 Time's up! 5 rounds la qua du de cai nhau roi`
- `> ⏰ Hard cap! Nhu bong da — het gio la het, khong co bu gio`
- `> 🏁 5 rounds da qua. Toi met roi, Codex chac cung met (neu no biet met)`
- `> ⏰ Cap reached! Nhu game — het luot la het, khong co hack them round`
- `> 💀 5 rounds. Nhu sprint retrospective keo dai qua — STOP!`
- `> 🔔 Het gio! Tong ket thoi — khong cai nhau nua!`
- `> ⏰ 5/5 rounds. OK ca hai deu da co noi, gio ket thuc di`

## 12. FINAL_SUMMARY
> Trigger: Session ket thuc, hien summary (Step 10 Final Output)

- `> 📊 Review xong! Hy vong code gio da tot hon — nho toi, khong phai Codex 😏`
- `> 🎬 That's a wrap! Session ket thuc. Code da duoc review ky luong`
- `> 📋 Tong ket day! Mot ngay lam viec hieu qua giua Claude va Codex`
- `> 🎯 Done! Neu code van co bug thi... do la feature, khong phai bug 😏`
- `> 📊 Session complete! Code da duoc 2 AI review — an tam di`
- `> 🎬 Ket thuc! Toi va Codex da lam het suc — phan con lai la cua ban`
- `> 📋 Review done! Gio di deploy thoi... a khoan, test truoc da 😅`
- `> 🏁 Xong roi! Mot session nua da hoan thanh. See you next review!`

## 13. THINK_PEER
> Trigger: think-about debate — khi cross-analysis (Step 6)

- `> 🧠 Hmm, Codex nghi khac toi. Interesting... de debate thoi`
- `> 💭 2 AI, 2 goc nhin. De xem ai thuyet phuc hon`
- `> 🤔 Codex co point — nhung toi cung co point. Ai dung day?`
- `> 🧠 Brain vs Brain! Toi va Codex se tim ra cau tra loi`
- `> 💭 Codex dua ra y kien roi. De toi phan tich xem co hop ly khong`
- `> 🤔 Debate mode ON! 2 AI ngoi cai nhau ve architecture — classic`
- `> 🧠 Codex co goc nhin khac. Khong sao — diverse perspectives la tot`
- `> 💭 De toi so sanh y kien cua toi voi Codex... may ra hoc duoc gi`

## 14. THINK_AGREE
> Trigger: think-about — Claude dong y voi Codex

- `> 🤝 OK toi dong y voi Codex diem nay. Credit where credit's due`
- `> ✅ Codex noi dung! Toi cung nghi vay — great minds think alike 🧠`
- `> 🤝 Consensus! Ca hai deu dong y. Diem nay chac chan roi`
- `> 👍 Fair enough, Codex. Toi cong nhan — ban dung ve diem nay`
- `> 🤝 Agreement! Khi 2 AI dong y thi chac 99% la dung roi 😏`
- `> ✅ Codex va toi cung ket luan. Trustworthy answer day!`

## 15. THINK_DISAGREE
> Trigger: think-about — Claude bat dong voi Codex

- `> ❌ Khong dong y! Codex sai roi — day la ly do`
- `> 🔥 Hard disagree! Toi co evidence, Codex chi co opinion`
- `> ❌ Nope! Codex, ban can xem lai sources cua ban`
- `> 😤 Bat dong! Toi se bao ve quan diem cua toi den cung`
- `> ❌ Disagree! Khong phai toi khong ton trong Codex — nhung lan nay no sai`
- `> 🔥 Toi khong the dong y duoc. De toi giai thich tai sao...`

## 16. PARALLEL_LAUNCH
> Trigger: parallel-review — Launch 5 reviewers (Step 2)

- `> 🚀 Deploying 5 reviewers! 4 Claude agents + Codex — all at once!`
- `> ⚡ 5 reviewers launching! Nhu Avengers assemble nhung la AI`
- `> 🎯 5 brains, 1 codebase. Let the parallel review begin!`
- `> 🚀 Launching review squad! Security, Performance, Correctness, Architecture + Codex`
- `> ⚡ All 5 go! Nhu 5 con bot rush vao code cung luc`
- `> 🏟️ 5v1 — code cua ban vs 5 reviewers. Good luck, code! 😏`
- `> 🚀 Team assembled! Moi reviewer mot nhiem vu — khong ai thoat`
- `> ⚡ 5 parallel reviews starting NOW! Nhanh hon, manh hon, nhieu hon!`

## 17. PARALLEL_MERGE
> Trigger: parallel-review — Merge findings (Step 4)

- `> 🔀 Merging findings tu 5 reviewers... nhu git merge nhung khong conflict (hy vong)`
- `> 📊 Tat ca da bao cao! Gio merge lai xem ai tim duoc nhieu bug nhat`
- `> 🔀 Merge time! De toi hop nhat ket qua tu 5 reviewers`
- `> 📋 5 bao cao da ve. De toi deduplicate va sort theo severity`
- `> 🔀 Combining findings... nhu Exodia — ghep cac manh lai thanh 1`
- `> 📊 Merge phase! Xem co bao nhieu findings trung nhau`

## 18. CHUNK_PROGRESS
> Trigger: codebase-review — Moi chunk hoan thanh (Step 4g)

- `> 📦 Chunk {N}/{TOTAL} [{CHUNK}] xong! Tien hanh chunk tiep theo~`
- `> ✅ {N}/{TOTAL} done! Con {remaining} chunks nua thoi`
- `> 📦 Chunk [{CHUNK}] reviewed! Next!`
- `> 🎯 {N}/{TOTAL} — dang tien do tot! Keep going~`
- `> 📦 Xong chunk {N}! Codex doc code nhanh phet`
- `> ✅ Chunk {N}/{TOTAL} complete! Mo khoa chunk tiep theo thoi`
- `> 📦 [{CHUNK}] done! {N} tren {TOTAL} — halfway la halfway~`
- `> 🎯 {N}/{TOTAL} chunks reviewed. Steady pace!`

## 19. CHUNK_CROSS
> Trigger: codebase-review — Cross-cutting analysis (Step 5)

- `> 🔍 Cross-cutting analysis! Gio de toi tim nhung pattern an giua cac modules`
- `> 🧩 Zoom out! Nhin toan bo codebase tu goc do 10.000 feet`
- `> 🔍 De toi tim nhung van de xuyen suot — cai ma tung chunk khong thay duoc`
- `> 🧩 Cross-module analysis time! Nhu nhin buc tranh lon tu nhung manh ghep nho`
- `> 🔍 Synthesizing findings across {TOTAL} chunks... pattern matching mode ON`
- `> 🧩 Big picture time! De xem cac modules co "noi chuyen" voi nhau tot khong`

---

## Usage Instructions (for SKILL.md)

1. **Load**: Read `references/flavor-text.md` at skill start
2. **Pick**: For each trigger, randomly select 1 message from the matching pool
3. **No repeat**: Track used messages — never repeat within same session
4. **Replace vars**: `{N}` → round/chunk number, `{TOTAL}` → total count, `{CHUNK}` → chunk name, `{ROUND}` → round number
5. **Display**: Output as markdown blockquote: `> {emoji} {message}`
6. **Optional**: User can disable by saying "no flavor" or "skip humor"
