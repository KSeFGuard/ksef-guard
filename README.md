<div align="center">

# KSeF Guard

**Walidator faktur FA(3) offline — sprawdź XML, zanim wyślesz do KSeF.**
*Offline FA(3) invoice validator — check your XML before you send it to KSeF.*

[🌐 Strona / Website](https://www.ksefguard.pl) · [⬇️ Pobierz / Download](https://www.ksefguard.pl/en/download/) · [📄 Raport zgodności / Conformance report](https://www.ksefguard.pl/downloads/conformance-report-v9.pdf)

`KSeF` · `FA(3)` · `faktura ustrukturyzowana` · `walidacja offline` · `e-invoicing` · `Poland` · proprietary, **free tier** · Windows GUI + Linux CLI

</div>

> **What this repository is:** the **public home** of KSeF Guard — README, download links, checksums, the conformance report, a CI example, and the **issue tracker**. **It contains no engine source code.** KSeF Guard is a **commercial / proprietary** product with a **free tier** — see [Is this open source?](#-is-this-open-source--czy-to-open-source).

---

## 🇵🇱 Polski

**KSeF Guard** to **offline'owy walidator** polskich faktur **FA(3) / KSeF**. Sprawdza pełny **schemat XSD FA(3)** oraz **128 reguł biznesowych** z **podstawą prawną**, dwujęzycznie (PL/EN) — i wychwytuje **107 problemów, których samo KSeF nie egzekwuje**, **zanim** wyślesz fakturę. Wszystko działa **lokalnie** — dane faktur **nie opuszczają komputera**.

### Dlaczego to ważne
KSeF sprawdza **składnię**. Prawo wymaga **treści**. W teście **256 faktur** wobec oficjalnego **API testowego KSeF** rządowe API **przyjęło 98 dokumentów**, które były **niezgodne z prawem**. KSeF Guard sprawdza jedno i drugie — strukturę **i** logikę biznesową — zanim faktura trafi do urzędu.

### Co potrafi
- ✅ **Pełna walidacja XSD FA(3)** (schemat 1-0E) + **128 reguł** biznesowych/prawnych
- ✅ **Offline** — żadnych przesyłek do chmury; prywatność z definicji
- ✅ **Dwujęzyczne raporty** (PL/EN) z dokładną lokalizacją błędu, „co poprawić" i **cytatem z przepisu**
- ✅ **Walidacja wsadowa (batch)** całych katalogów faktur klientów
- ✅ **Eksport** do **PDF / CSV / JSON** (raporty gotowe do audytu)
- ✅ Mocna obsługa faktur **walutowych**, **korekt (KOR)**, dat, NIP-ów i pól szczególnych

### Dla kogo
Przede wszystkim **biura rachunkowe** i działy finansowe, które masowo wysyłają FA(3) do KSeF i potrzebują **pewności przed wysyłką** oraz **raportów dla klientów**.

### Pobierz
- **Windows** — instalator **MSI** lub wersja **przenośna ZIP**
- **Linux** — **CLI** (do automatyzacji / CI-CD)

➡️ **[www.ksefguard.pl](https://www.ksefguard.pl/en/download/)**

### Cennik (model: darmowa aplikacja + klucz licencyjny)
| Plan | Cena | Co zawiera |
|---|---|---|
| **Free** | 0 € | **wszystkie 128 reguł**, 10 plików/dzień, GUI + CLI (tekst), 1 urządzenie |
| **Standard** | €39/mies. (€384/rok) | eksport **PDF/CSV/JSON**, konfiguracja reguł, **5 000 plików/dzień**, 3 urządzenia |
| **Pro** | €89/mies. (€864/rok) | bez limitu plików, **white-label PDF**, presety eksportu, konfiguracja YAML, 10 urządzeń |

> Darmowy plan ma **komplet reguł**. Plany płatne to **przepustowość i raporty dla biura** — wsad, eksporty PDF/CSV/JSON, więcej urządzeń, ślad audytowy.

---

## 🇬🇧 English

**KSeF Guard** is an **offline validator** for Polish **FA(3) / KSeF** e-invoices. It checks the full **FA(3) XSD** plus **128 business rules** with **legal citations**, bilingual (PL/EN) — and catches **107 issues KSeF itself does not enforce**, **before** you submit. Everything runs **locally** — invoice data **never leaves the device**.

### Why it matters
KSeF checks **syntax**. The law requires **substance**. In a test of **256 invoices** against the official **KSeF test API**, the government API **accepted 98 documents** that were **legally non-compliant**. KSeF Guard checks both — structure **and** business logic — before the invoice reaches the tax office.

### What it does
- ✅ **Full FA(3) XSD validation** (schema 1-0E) + **128** business/legal rules
- ✅ **Offline** — no cloud uploads; private by design
- ✅ **Bilingual reports** (PL/EN) with exact error location, "what to fix", and the **legal quote**
- ✅ **Batch validation** of whole folders of client invoices
- ✅ **Export** to **PDF / CSV / JSON** (audit-ready reports)
- ✅ Strong on **foreign-currency** invoices, **corrections (KOR)**, dates, NIPs, and special fields

### Who it's for
Primarily **accounting offices (biura rachunkowe)** and finance teams submitting FA(3) to KSeF at volume, who need **pre-submission certainty** and **client-ready reports**.

### Download
- **Windows** — **MSI** installer or **portable ZIP**
- **Linux** — **CLI** (for automation / CI-CD)

➡️ **[www.ksefguard.pl](https://www.ksefguard.pl/en/download/)**

### Pricing (model: free app + license key)
| Plan | Price | Includes |
|---|---|---|
| **Free** | €0 | **all 128 rules**, 10 files/day, GUI + CLI (text), 1 machine |
| **Standard** | €39/mo (€384/yr) | **PDF/CSV/JSON** export, rule config, **5,000 files/day**, 3 machines |
| **Pro** | €89/mo (€864/yr) | unlimited files, **white-label PDF**, export presets, YAML config, 10 machines |

> The free tier runs the **full rule set**. Paid is **office throughput + client reports** — batch, PDF/CSV/JSON exports, more machines, audit trail.

---

## 🤖 Use the CLI in CI/CD

Gate your pipeline on offline FA(3) validation — see [`.github/workflows/validate-fa3-example.yml`](.github/workflows/validate-fa3-example.yml). In short:

```bash
# Download the free Linux CLI
curl -fsSL -o ksef-guard.tar.gz https://www.ksefguard.pl/downloads/ksef-guard-linux-amd64.tar.gz
tar xzf ksef-guard.tar.gz && chmod +x ksef-guard

# Validate a folder of invoices (non-zero exit on errors → fails the build)
./ksef-guard validate --format summary ./invoices/

# Or produce a machine-readable report
./ksef-guard validate --format json --output report.json ./invoices/
```

Formats: `text` · `summary` · `json` · `csv` · `pdf`. Run `./ksef-guard --help` for all flags.

## 🔒 Verify your download

Every release on [ksefguard.pl/downloads](https://www.ksefguard.pl/en/download/) publishes a **SHA-256** checksum. After downloading, confirm it matches:

```bash
# Linux / macOS
sha256sum ksef-guard-linux-amd64.tar.gz
```
```powershell
# Windows (PowerShell)
Get-FileHash .\ksef-guard_1.0.0_x64_en-US.msi -Algorithm SHA256
```

## 📦 Sample invoices

A pack of example FA(3) XML files (valid + intentionally failing) is available for trying the validator — **[download the sample XML pack](https://www.ksefguard.pl/downloads/ksef-guard-showcase-xml-pack.zip)**.

## 📊 Proof: the conformance report

We submitted **256 real invoices** to the official **KSeF test API** and recorded which legally-non-compliant ones it accepted. The full methodology + per-rule results are in the public **[conformance report (PDF)](https://www.ksefguard.pl/downloads/conformance-report-v9.pdf)**.

## ❓ Is this open source? / Czy to open source?

**No / Nie.** The validation **engine is proprietary (commercial)**. This repository is the product's **public home** — README, download links, checksums, conformance report, sample pack, CI examples, and the **issue tracker** — and contains **no engine source code**. The **app is free to download and use** (free tier); paid tiers unlock higher volume and reports.

## 🛟 Support

- **Bugs / rule questions:** open an [issue](../../issues).
- **Billing, licenses, accounts:** email **support@ksefguard.pl** (please don't put account details in public issues).

## 🔗 Links

- Website (PL): https://www.ksefguard.pl
- Website (EN): https://www.ksefguard.pl/en/
- Download: https://www.ksefguard.pl/en/download/
- Conformance report: https://www.ksefguard.pl/downloads/conformance-report-v9.pdf

---

<div align="center">
<sub>KSeF Guard is a technical validation tool, not tax advice. · KSeF Guard to narzędzie techniczne, nie porada podatkowa.</sub>
</div>
