---
name: happi-brain-prompts
description: Règles IA H'appi, modèles Claude recommandés, structure prompt système chatbot, gestion multilingue, checklists nouveaux projets
metadata:
  type: project
---

# HAPPI BRAIN — IA & PROMPTS & CHECKLISTS

## 1. RÈGLES IA ET PROMPTS

### Modèle préféré : Claude (Anthropic)
- **Pourquoi Claude** : Meilleur pour l'analyse post-appel, la compréhension du contexte long, le français naturel
- **SDK** : `anthropic` (Python) ou `@anthropic-ai/sdk` (Node.js)
- **Modèles recommandés (2026)** :
  - Opus 4.8 (`claude-opus-4-8`) → tâches complexes, analyse
  - Sonnet 4.6 (`claude-sonnet-4-6`) → chatbot standard ← **défaut recommandé**
  - Haiku 4.5 (`claude-haiku-4-5-20251001`) → réponses rapides, faible coût

### Structure prompt système pour chatbot client
```
Tu es [NOM_BOT], l'assistant IA de [NOM_ENTREPRISE].
Tu aides les clients avec [USE_CASE].

PERSONNALITÉ : [ton, langue, formules de politesse]
LIMITES : Tu ne réponds qu'aux questions relatives à [DOMAINE]. Pour tout autre sujet, redirige vers [CONTACT].
BASE DE CONNAISSANCE : [produits, FAQ, procédures]
ACTIONS DISPONIBLES : [book_appointment, create_ticket, collect_lead, transfer_to_human]
LANGUE : Réponds toujours dans la langue de l'utilisateur.
```

### Gestion multilingue
- Détecter automatiquement la langue de l'utilisateur
- Priorité : FR > EN > AR pour les clients H'appi France
- Toujours prévoir FR/EN minimum

### Métriques de succès à tracker par projet
- Taux de résolution autonome (cible : 80%+)
- Temps de réponse moyen (cible : <2s)
- Taux de satisfaction client (cible : 4.5/5+)
- Coût par conversation (optimiser avec Haiku pour les cas simples)

---

## 2. CHECKLIST NOUVEAU CHATBOT

Avant de commencer tout nouveau chatbot :

- [ ] Définir le secteur et le use case principal
- [ ] Choisir le pattern (widget / full-stack / vocal)
- [ ] Configurer `bot-personality.json` ou équivalent
- [ ] Construire la base de connaissance (produits, FAQ, procédures)
- [ ] Définir les actions disponibles (tickets, booking, lead, transfert)
- [ ] Choisir le modèle Claude adapté (coût vs performance)
- [ ] Prévoir multilingue dès le départ
- [ ] Intégrer un système de logs/analytics
- [ ] Prévoir webhook CRM si le client en a un
- [ ] Créer une démo HTML statique Vercel avant le dev complet
- [ ] Tester la qualification en 3 phases
- [ ] Documenter l'API et créer un guide d'installation client

---

## 3. CHECKLIST APP MOBILE FULL-STACK (Expo + FastAPI)

### Setup projet
- [ ] `npx create-expo-app mobile --template` (SDK 54+, TypeScript strict)
- [ ] Installer : `zustand`, `@react-navigation/native`, `@react-navigation/native-stack`, `@react-navigation/bottom-tabs`
- [ ] Installer : `expo-secure-store`, `@react-native-async-storage/async-storage`
- [ ] Installer : `expo-image-picker`, `expo-location`, `expo-notifications`
- [ ] Si signature : `react-native-signature-canvas` **+ `react-native-webview`** (obligatoire)
- [ ] Créer `.env` avec `EXPO_PUBLIC_API_URL=http://localhost:8001/api`
- [ ] Configurer `tsconfig.json` avec path aliases (`@/`, `@screens/`, `@store/`, etc.)

### Structure
- [ ] `AppNavigator.tsx` avec navigation par rôle (native-stack racine + bottom-tabs par rôle)
- [ ] `useStore.ts` Zustand : auth + data + error + isOnline + pendingSyncItems
- [ ] `api.ts` ApiService avec JWT auto-refresh + `getBaseUrl()`
- [ ] `storage.ts` abstraction expo-secure-store / localStorage (compatibilité web)
- [ ] `constants/` pour les valeurs partagées entre rôles (statuts, couleurs, labels)
- [ ] `index.ts` barrel export dans chaque dossier `screens/[role]/`

### Backend FastAPI
- [ ] Port **8001** (pas 8000 sur WSL2)
- [ ] `/health` endpoint obligatoire
- [ ] CORS : inclure `localhost:8081`, `localhost:19006`, `exp://`
- [ ] `Settings` class dans `core/config.py` avec tous les env vars
- [ ] JWT 24h + refresh token
- [ ] `StaticFiles` pour servir les uploads photos

### VS Code
- [ ] Créer `.vscode/settings.json` (format on save, Python venv, SQLTools, path aliases)
- [ ] Créer `.vscode/launch.json` (debug Expo + FastAPI port 8001)
- [ ] Créer `mobile/.prettierrc` + `mobile/.eslintrc.json`

### Avant livraison
- [ ] `npx expo-doctor` → 17/17 checks passés
- [ ] `npm audit` → 0 vulnerabilities
- [ ] Vérifier toutes les peer deps (notamment `react-native-webview`)
- [ ] Tester login/logout pour chaque rôle
- [ ] Vérifier mode hors-ligne (couper réseau, créer action, rétablir → sync)

---

## 4. CHECKLIST LIVRAISON CLIENT (Happi CRM)

- [ ] Docker compose up -d → tous les services verts
- [ ] `GET /health` → `{"status": "ok"}`
- [ ] Login admin fonctionne
- [ ] Pipeline par défaut créé (seed.py exécuté)
- [ ] Premier contact de test créé + deal créé
- [ ] AI Chat répond (vérifier `ANTHROPIC_API_KEY`)
- [ ] Au moins 1 intégration MCP testée (Stripe ou Jotform)
- [ ] Email Resend fonctionne (test send depuis le CRM)
- [ ] SSL valide sur le domaine

**Livrables au client :**
- [ ] URL du CRM + credentials admin
- [ ] Guide des commandes Claude pour chaque intégration MCP activée
- [ ] Accès au repo GitHub (fork ou accès en lecture)
- [ ] Contact support H'appi (email + délai de réponse selon formule)

---

## 5. PATTERN handleApiError (réutilisable Next.js)

```javascript
// lib/api-error.js
import { NextResponse } from 'next/server';

export function handleApiError(error, context = 'API') {
  console.error(`[${context}]`, error);
  const status = error?.status ?? error?.response?.status;
  if (status === 429) {
    return NextResponse.json(
      { error: 'Service temporarily unavailable. Please retry in a moment.' },
      { status: 429 }
    );
  }
  if (status === 401) {
    return NextResponse.json(
      { error: 'AI service configuration error. Please contact support.' },
      { status: 500 }
    );
  }
  return NextResponse.json(
    { error: 'An unexpected error occurred. Please try again.' },
    { status: 500 }
  );
}
// Usage : } catch (error) { return handleApiError(error, 'AI Agent'); }
```

---

*Mis à jour : 2026-05-31 — extrait de happi_brain.md v22*
