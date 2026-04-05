# 🧠 Happi Brain

> Base de connaissance centrale de H'appi — cerveau évolutif de Claude pour tous les projets chatbot IA.

## Structure

```
happi_brain.md          ← Cerveau principal (27 repos analysés, stack, patterns, clients)
README.md               ← Ce fichier

memory/
  MEMORY_global.md      ← Index mémoire global (tous projets)
  MEMORY_quality_tracking.md ← Index mémoire projet Quality Tracking
  project_dropos.md     ← Détails projet DropOS
  project_happi_foundry.md   ← Détails projet H'appi Foundry

claude-config/
  CLAUDE.md             ← Instructions globales Claude Code (chargé automatiquement)
```

## Mise à jour automatique

L'agent **Happi Brain — Veille Tech Quotidienne** tourne chaque jour à 9h00 (GMT+2) et ajoute une section veille tech dans `happi_brain.md`.

Sources surveillées : HackerNews · DEV.to · GitHub Trending · The New Stack · InfoQ

## Comment utiliser

1. Clone ce repo dans ton environnement de dev
2. Claude Code charge automatiquement `CLAUDE.md` depuis `~/CLAUDE.md`
3. Après chaque nouveau projet H'appi terminé, dis à Claude : **"mets à jour le Happi Brain"**

## Projets couverts

- SAV-BOT Mobilier de France
- INnatural Stores Chatbot
- Happi Secretary (secrétariat vocal IA)
- 18 démos clients HTML (hôtellerie, BTP, agroalimentaire, sport...)
- Happi Foundry (playground Claude)
- DropOS (SaaS dropshipping)
- Quality Tracking App (React Native)
- Top Tier Collection (e-commerce)

---
*Startup H'appi — happi-bot.com*
