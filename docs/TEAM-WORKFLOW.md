# QRPOC Team Workflow

**Status:** proposed to Erk · agreed on Yaren's side · 2026-08-15
**People:** Yaren (design/UX) · Erk (frontend/backend, owner of the Lovable prototype)

## Principle

Two sources of truth, one owner each. Nobody edits the other person's source directly; the boundary is always crossed through an approved handoff.

| Truth | Owner | Lives in | The other person may |
|---|---|---|---|
| Design | Yaren | Figma + `qrpoc` docs repo | read, open PRs |
| Code | Erk | Lovable + app repo (GitHub) | read, open issues, open branch PRs |

## One-time setup (Erk, ~10 minutes)

1. **Connect Lovable to GitHub** (Lovable settings → GitHub → Connect). This creates the app repo with two-way sync: every Lovable edit becomes a commit, every merged commit reaches Lovable. The repo is the single home of the code from then on.
2. **Give Yaren access** to the app repo: read + permission to open branches and PRs.
3. **Protect `main`:** only Erk merges to `main`. Everything else arrives as branch + PR. Lovable follows `main`, so this same rule protects the live prototype from accidents.
4. **No manual code copies, ever.** Nobody copies app code into other folders or repos; copies start lying the moment they are made. "What does the code do?" is always answered by the app repo itself.

## Everyday flow (per slice)

1. **Design** — Yaren designs in Figma. Approval gate: Yaren + Erk together.
2. **Handoff** — approved Figma frames + the screen acceptance checklist (deck, slide 32) + the domain glossary. No room for guessing names, states, or behavior.
3. **Build** — Erk implements in Lovable or directly in the repo; either way every change lands in the repo automatically.
4. **Verify** — Yaren walks the live URL (qrpoc.lovable.app) against the checklist. Findings become GitHub issues labeled with the slice name — not DMs.
5. **Record** — durable decisions are written into the `qrpoc` docs repo. A decision that exists only in chat is not a decision.

## Yaren's prototype loop

For behavior questions, Yaren also works hands-on — without touching Erk's flow:

- Current screen is imported into Figma (code→design) → redesigned → Claude Code implements the frame **on a Yaren branch of the app repo** → validated in a live browser preview → the settled state is synced back to Figma → handoff as above, now with the branch/PR attached as reference.
- Branches never touch `main`, and Lovable follows only `main` — so this loop cannot break the live prototype.
- The PR is a reference, not an obligation: Erk merges it as-is or reimplements it to his own standards. Erk's call.

## Three don'ts

1. **No code copying** — link, don't copy.
2. **No direct edits to `main`** — branch + PR + Erk's merge, no exceptions (including Yaren, including Claude).
3. **No decisions left in chat** — Figma approval or a docs-repo record; everything else counts as "still being discussed."

---

# QRPOC Ekip İş Akışı (Türkçe çeviri)

**Durum:** Erk'e öneri · Yaren tarafında mutabık · 15-08-2026
**Kişiler:** Yaren (tasarım/UX) · Erk (frontend/backend, Lovable prototipinin sahibi)

## İlke

İki kaynak gerçeği var, her birinin tek sahibi var. Kimse diğerinin kaynağını doğrudan düzenlemez; sınır her zaman onaylı teslimle geçilir.

| Gerçek | Sahibi | Nerede yaşar | Diğer kişi ne yapabilir |
|---|---|---|---|
| Tasarım | Yaren | Figma + `qrpoc` docs repo | okur, PR açar |
| Kod | Erk | Lovable + app repo (GitHub) | okur, issue açar, branch PR'ı açar |

## Tek seferlik kurulum (Erk, ~10 dakika)

1. **Lovable'ı GitHub'a bağla** (Lovable ayarları → GitHub → Connect). Bu, iki yönlü senkronlu app repo'yu oluşturur: Lovable'daki her düzenleme commit olur, merge edilen her commit Lovable'a yansır. Kodun tek adresi artık bu repodur.
2. **Yaren'e erişim ver:** okuma + branch/PR açabilme.
3. **`main`'i koru:** `main`'e sadece Erk merge eder. Diğer her şey branch + PR olarak gelir. Lovable `main`'i izlediği için bu kural canlı prototipi de kazalardan korur.
4. **El ile kod kopyalama yok.** Kimse uygulama kodunu başka klasöre/repoya kopyalamaz; kopya, yapıldığı anda yalan söylemeye başlar. "Kod ne yapıyor?" sorusunun cevabı her zaman app repo'nun kendisidir.

## Günlük akış (dilim başına)

1. **Tasarım** — Yaren Figma'da tasarlar. Onay kapısı: Yaren + Erk birlikte.
2. **Teslim** — onaylı Figma frame'leri + ekran kabul listesi (deck, slayt 32) + domain sözlüğü. İsim, durum ve davranışta tahmine yer kalmaz.
3. **Uygulama** — Erk, Lovable'da veya doğrudan repoda uygular; her iki durumda da değişiklik repoya otomatik düşer.
4. **Doğrulama** — Yaren canlı URL'de (qrpoc.lovable.app) kabul listesi üzerinden gezer. Bulgular, dilim adıyla etiketlenmiş GitHub issue olur — DM değil.
5. **Kayıt** — kalıcı kararlar `qrpoc` docs repo'ya işlenir. Sadece sohbette kalan karar, karar değildir.

## Yaren'in prototip döngüsü

Davranış soruları için Yaren de elleriyle çalışır — Erk'in akışına dokunmadan:

- Mevcut ekran Figma'ya alınır (code→design) → yeniden tasarlanır → Claude Code frame'i **app repo'da Yaren'in branch'inde** uygular → canlı tarayıcı önizlemesinde doğrulanır → oturan hal Figma'ya geri işlenir → teslim yukarıdaki gibi yapılır, artık branch/PR referansı da eklenmiş olur.
- Branch'ler `main`'e asla dokunmaz; Lovable yalnız `main`'i izler — bu döngü canlı prototipi bozamaz.
- PR bir referanstır, yükümlülük değil: Erk ister olduğu gibi alır, ister kendi standartlarına göre yeniden yazar. Karar Erk'in.

## Üç "yapma"

1. **Kod kopyalama yok** — link ver, kopyalama.
2. **`main`'e doğrudan dokunma yok** — branch + PR + Erk'in merge'ü; istisnasız (Yaren dahil, Claude dahil).
3. **Kararı sohbette bırakma yok** — Figma onayı veya docs repo kaydı; bunun dışındaki her şey "henüz konuşuluyor" sayılır.
