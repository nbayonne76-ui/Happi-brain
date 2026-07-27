# 🔒 Dependency & Security Watch — Happi Brain

> Ce fichier compile, chaque semaine, l'audit des vulnérabilités connues (CVE/GHSA) dans les dépendances des projets actifs de H'appi. Agent en lecture seule sur les repos projets : aucun fichier de dépendances (`package.json`, `requirements.txt`, lockfiles) ni aucune PR n'est modifié par cet agent. Priorisation et patch à valider manuellement par Nicolas.

---
## 🔒 Dependency & Security Watch — 2026-07-27
> Rapport généré automatiquement — lecture seule, aucun fichier de dépendances ni repo projet n'a été modifié par cet agent. Priorisation à valider manuellement.

### microsoft-sales-app
- **Méthode** : audit automatique (`npm audit --omit=dev`, 396 dépendances de prod)
- **Résultat** :
  - `next-auth` 4.24.14 (+ `@auth/core` 0.41.2) — **CRITICAL** — [GHSA-xmf8-cvqr-rfgj](https://github.com/advisories/GHSA-xmf8-cvqr-rfgj) (CVSS 7.5) : `getToken()` lève une exception non interceptée sur un header `Authorization: Bearer` malformé → crash/DoS du endpoint d'auth. [GHSA-x445-f3h2-j279](https://github.com/advisories/GHSA-x445-f3h2-j279) (CVSS 6.8) : cookies state/nonce/PKCE OAuth non liés au provider qui les a créés → risque de mix-up OAuth. Fix conseillé : dernière 4.24.x ou migration Auth.js v5.
  - `xlsx` 0.18.5 — **HIGH** — [GHSA-4r6h-8v6p-xvw6](https://github.com/advisories/GHSA-4r6h-8v6p-xvw6) (CVSS 7.8, prototype pollution) + [GHSA-5pgg-2g8v-p4x9](https://github.com/advisories/GHSA-5pgg-2g8v-p4x9) (CVSS 7.5, ReDoS). **Pas de fix disponible via npm** (SheetJS ne publie plus la version corrigée sur le registre npm) — nécessite un build officiel SheetJS ≥0.20.2 hors npm ou une lib alternative.
  - `nodemailer` 7.0.13 — **HIGH** — notamment [GHSA-p6gq-j5cr-w38f](https://github.com/advisories/GHSA-p6gq-j5cr-w38f) (CVSS 7.1, l'option `raw` au niveau message contourne `disableFileAccess`/`disableUrlAccess` → lecture fichier arbitraire + SSRF) et [GHSA-r7g4-qg5f-qqm2](https://github.com/advisories/GHSA-r7g4-qg5f-qqm2) (CVSS 6.5, validation TLS incorrecte lors du fetch de token OAuth2 → interception de credentials). Fix : 9.0.3 (bump majeur).
  - `next` 15.5.18 — **HIGH** — SSRF via Server Actions ([GHSA-89xv-2m56-2m9x](https://github.com/advisories/GHSA-89xv-2m56-2m9x)), divulgation de endpoints Server Functions internes. Fix : dernier patch 15.x.
  - Transitifs secondaires (`form-data` CVSS 7.5 CRLF injection, `undici` jusqu'à CVSS 7.5 DoS WebSocket/bypass TLS SOCKS5, `sharp`, `postcss`) — fix automatique disponible, priorité plus faible.

### h-appi-website
- **Méthode** : audit automatique (`npm audit --omit=dev`)
- **Résultat** :
  - `next` 15.5.12 — **HIGH** — [GHSA-c4j6-fc7j-m34r](https://github.com/advisories/GHSA-c4j6-fc7j-m34r) (CVSS 8.6, SSRF via upgrade WebSocket), [GHSA-492v-c6pp-mqqv](https://github.com/advisories/GHSA-492v-c6pp-mqqv) (CVSS 8.1, bypass Middleware via injection de paramètre de route dynamique), plusieurs DoS (Image Optimization, Cache Components, CVSS ~7.5). Site vitrine public directement exposé. Fix : dernier patch 15.x.
  - `sharp`, `postcss`, `picomatch` — transitifs/build, pas de données sensibles traitées côté site vitrine, priorité secondaire.

### Quality-tracking-app
- **Méthode** : audit automatique (`npm audit` sur frontend et mobile, `pip-audit -r requirements.txt` sur backend + vérification manuelle des scores CVSS via recherche web, pip-audit ne les fournissant pas)
- **Résultat — frontend** :
  - `axios` 1.13.4 — **HIGH** — plus de 15 avisories cumulées, les plus graves : [GHSA-35jp-ww65-95wh](https://github.com/advisories/GHSA-35jp-ww65-95wh) (CVSS 8.7, MITM complet via pollution de prototype sur `config.proxy`), [GHSA-43fc-jf86-j433](https://github.com/advisories/GHSA-43fc-jf86-j433) (CVSS 7.5, DoS via clé `__proto__` dans `mergeConfig`), [GHSA-hfxv-24rg-xrqf](https://github.com/advisories/GHSA-hfxv-24rg-xrqf) (CVSS 7.5, ReDoS via injection de nom de cookie). Fix : dernière 1.x (pas de breaking change identifié).
  - `react-router` (dépendance de `react-router-dom` 7.13.0) — **CRITICAL réel** — [GHSA-49rj-9fvp-4h2h](https://github.com/advisories/GHSA-49rj-9fvp-4h2h) (CVSS 8.1, invocation arbitraire de constructeur via désérialisation `turbo-stream` → **RCE non authentifié**), [GHSA-8646-j5j9-6r62](https://github.com/advisories/GHSA-8646-j5j9-6r62) (CVSS 8, XSS via cible de redirection `javascript:` en mode RSC). Fix : mettre à jour `react-router-dom` en priorité.
- **Résultat — mobile (Expo/React Native)** :
  - `node-forge` 1.3.3 (transitif, lib crypto) — **HIGH** — [GHSA-2328-f5f3-gj25](https://github.com/advisories/GHSA-2328-f5f3-gj25) (CVSS 7.4, bypass `basicConstraints` dans la vérification de chaîne de certificats), [GHSA-q67f-28xg-22rw](https://github.com/advisories/GHSA-q67f-28xg-22rw) (CVSS 7.5, forgerie de signature Ed25519). Pertinent si l'app fait de la validation TLS/certificat côté client.
  - `shell-quote` et `tar` (CRITICAL selon npm) — dépendances d'outillage de build (Metro/Expo CLI), non embarquées dans le bundle livré aux utilisateurs finaux : impact limité à l'environnement de build/CI, pas au runtime mobile. Priorité secondaire, à corriger lors du prochain bump du SDK Expo.
  - Reste (`undici`, `ws`, `js-yaml`, `minimatch`, `brace-expansion`, `picomatch`, `@xmldom/xmldom`, `postcss`) — même famille d'outillage transitif Expo/Metro, essentiellement DoS via CLI, impact runtime limité. Non détaillés un par un ici (nombreux doublons GHSA) — `npm audit fix` à lancer lors de la prochaine maintenance.
- **Résultat — backend (FastAPI)** :
  - `python-jose` 3.3.0 — **CRITICAL** — CVE-2024-33663 (confusion d'algorithme avec clés OpenSSH ECDSA, classé Critical par GitHub Advisory / High CVSS 7.4-9.3 selon la source) — **utilisé directement pour le JWT d'authentification** (`app/core/security.py`), donc risque réel de contournement de la vérification de signature. + CVE-2024-33664 (DoS par bombe de compression JWE, ~CVSS 7.5). Fix : ≥3.4.0.
  - `pillow` 10.2.0 — **HIGH** — plusieurs corruptions mémoire natives (ex. PYSEC-2026-3451/3453/3454, écriture hors limites sur le tas) déclenchables par une image malveillante, **utilisé directement sur des photos uploadées par les utilisateurs** (`app/api/endpoints/photos.py` → `Image.open()`). Fix : ≥12.3.0 (bump majeur).
  - `python-multipart` 0.0.6 — **HIGH** — plusieurs DoS (nombre de parties illimité, lecture bloquante via `Content-Length` négatif). S'applique car FastAPI utilise cette lib pour tout parsing multipart ; le CVE de path traversal CVE-2026-24486 (`UPLOAD_DIR`/`UPLOAD_KEEP_FILENAME`) ne s'applique **pas** ici, l'app écrit elle-même ses fichiers. Fix : ≥0.0.20 (idéalement 0.0.31).
  - `starlette` 0.35.1 — **HIGH** — CVE-2026-54283 (CVSS 7.5, limites `max_fields`/`max_part_size` silencieusement ignorées pour les corps `x-www-form-urlencoded` → DoS non authentifié). Fix : mettre à jour FastAPI (entraîne starlette).
  - `ecdsa` 0.19.2 (transitif) — CVSS 7.4 (attaque timing Minerva sur P-256) mais **sans fix prévu par le mainteneur** (side-channel jugé hors périmètre) et nécessite des mesures de timing très précises pour être exploitable à distance — à surveiller, pas à traiter dans l'urgence.

### Happi-Secretary
- **Méthode** : audit automatique (`npm audit` sur dashboard, `pip-audit -r requirements.txt` sur backend + vérification manuelle CVSS)
- **Résultat — dashboard (Next.js)** :
  - `next` 14.2.15 — **CRITICAL** — [GHSA-f82v-jwr5-mffw](https://github.com/advisories/GHSA-f82v-jwr5-mffw) (**CVSS 9.1**, Authorization Bypass in Next.js Middleware — contournement d'autorisation via le middleware, le score le plus élevé de toute la veille), [GHSA-c4j6-fc7j-m34r](https://github.com/advisories/GHSA-c4j6-fc7j-m34r) (CVSS 8.6, SSRF via upgrade WebSocket), plusieurs DoS Server Components (CVSS 7.5). Fix indiqué par npm : ≥16.2.12 (bump majeur — migration à prévoir, mais le 9.1 justifie de prioriser).
  - `lodash` 4.17.23 — **HIGH** — [GHSA-r5fr-rjxr-66jc](https://github.com/advisories/GHSA-r5fr-rjxr-66jc) (CVSS 8.1, injection de code via les noms de clé dans `_.template`), [GHSA-f23m-r3pf-42rh](https://github.com/advisories/GHSA-f23m-r3pf-42rh) (CVSS 6.5, prototype pollution via `_.unset`/`_.omit`). Fix auto disponible.
- **Résultat — backend (FastAPI, traitement de documents)** :
  - `pypdf` 4.3.1 — **CRITICAL/HIGH** — très en retard (4.3.1 vs 6.14.2, ~30 CVE cumulées), les plus graves : CVE-2026-59935 (CVSS 8.7, boucle infinie DoS via image inline malformée dans un PDF), CVE-2026-59937 (CPU exhaustion quadratique via récupération de table de références croisées). **Utilisé directement pour l'ingestion documentaire** (`app/services/knowledge_service.py`) — si des PDF externes/uploadés sont traités, un fichier forgé peut geler le service. Fix : ≥6.14.2 (bump majeur, migration d'API 4.x→6.x probable).
  - `python-multipart` 0.0.12 — **HIGH** — mêmes familles de DoS que Quality-tracking-app (headers de parties illimités, `Content-Length` négatif). Fix : ≥0.0.31.
  - `starlette` 0.38.6 — **HIGH** — CVE-2026-54283 (CVSS 7.5, DoS via limites de formulaire ignorées). Fix : mettre à jour FastAPI.

### Happi-CRM
- **Méthode** : audit automatique (`npm audit` sur frontend, `pip-audit -r requirements.txt` sur backend et mcp)
- **Résultat — frontend** :
  - `next` 16.2.4 — **HIGH** — [GHSA-c4j6-fc7j-m34r](https://github.com/advisories/GHSA-c4j6-fc7j-m34r) (CVSS 8.6, SSRF WebSocket), [GHSA-492v-c6pp-mqqv](https://github.com/advisories/GHSA-492v-c6pp-mqqv) (CVSS 8.1, bypass Middleware via injection de paramètre de route dynamique). Fix : ≥16.2.12 (patch mineur, pas de bump majeur).
  - `axios` 1.15.2 — **HIGH** — [GHSA-35jp-ww65-95wh](https://github.com/advisories/GHSA-35jp-ww65-95wh) (CVSS 8.7, MITM via pollution `config.proxy`), [GHSA-pjwm-pj3p-43mv](https://github.com/advisories/GHSA-pjwm-pj3p-43mv) (CVSS 8.6, bypass `NO_PROXY` via adresses IPv4-mapped IPv6). Fix : dernière 1.x.
  - `xlsx` 0.18.5 — **HIGH** — mêmes CVE que microsoft-sales-app (CVSS 7.8 prototype pollution + 7.5 ReDoS), pas de fix npm disponible. Risque réel si le CRM permet l'import/export de fichiers Excel fournis par des utilisateurs.
  - Transitifs secondaires (`form-data`, `sharp`, `postcss`) — priorité plus faible.
- **Résultat — backend** : `ecdsa` 0.19.2 (transitif) — CVSS 7.4 (Minerva), même situation que Quality-tracking-app : pas de fix prévu, faible exploitabilité distante. Mention informative.
- **Résultat — mcp** : RAS — aucune vulnérabilité High/Critical identifiée (pip-audit propre).

### happi-automate
- **Méthode** : audit automatique (`npm audit` sur frontend, `pip-audit -r requirements.txt` sur backend)
- **Résultat — frontend** :
  - `next` 14.2.35 — **HIGH** — [GHSA-c4j6-fc7j-m34r](https://github.com/advisories/GHSA-c4j6-fc7j-m34r) (CVSS 8.6, SSRF WebSocket), [GHSA-h25m-26qc-wcjf](https://github.com/advisories/GHSA-h25m-26qc-wcjf) (CVSS 7.5, DoS via désérialisation de requêtes HTTP en RSC non sécurisées), [GHSA-36qx-fr4f-26g5](https://github.com/advisories/GHSA-36qx-fr4f-26g5) (CVSS 7.5, bypass Middleware i18n Pages Router). Fix indiqué par npm : ≥16.2.12 — pas de patch mineur disponible sur la branche 14.x pour ces CVE, bump majeur nécessaire.
  - `postcss` — transitif build, priorité secondaire.
- **Résultat — backend** : `ecdsa` 0.19.2 (transitif) — CVSS 7.4 (Minerva), même situation que ci-dessus, pas de fix prévu, faible exploitabilité distante. Mention informative.

### ⚠️ À traiter en priorité
Happi-Secretary/dashboard : `next` 14.2.15 expose un **contournement d'autorisation dans le Middleware (CVSS 9.1, GHSA-f82v-jwr5-mffw)** — le score le plus critique de toute la veille. Quality-tracking-app/frontend : `react-router` permet une **RCE non authentifiée par désérialisation (CVSS 8.1, GHSA-49rj-9fvp-4h2h)**, et le backend utilise `python-jose` (confusion d'algorithme JWT) directement pour l'authentification.
