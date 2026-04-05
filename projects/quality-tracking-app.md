---
name: Quality Tracking App
type: mobile-app
status: production-ready
client: Mobilier de France
sector: Logistique / Livraison meubles
repo: Quality-tracking-app
---

# Quality Tracking App — Suivi Qualité Livraisons

## Contexte
Application mobile de suivi qualité des livraisons de meubles pour Mobilier de France. 5 rôles utilisateurs avec workflows dédiés.

## Stack
- **Mobile** : React Native (Expo SDK 54)
- **Backend** : FastAPI + PostgreSQL
- **State** : Zustand + AsyncStorage (offline sync)
- **Navigation** : React Navigation v6 (native-stack + bottom-tabs)
- **Auth** : JWT avec auto-refresh
- **Storage** : expo-secure-store (native) / localStorage (web)
- **Notifications** : expo-notifications avec fallback web

## Rôles & Écrans
| Rôle | Statut | Écrans |
|------|--------|--------|
| Supplier | Ready | Home, Deliveries, ProductPhotos, TruckLoading, Profile |
| Driver | Ready | Home, Deliveries, DeliveryDetail, Profile |
| Client | Ready | TrackingInput, DeliveryCard, Tracking, DeliveryDetail, Signature, OrderSummary |
| Admin | Ready | Dashboard, LiveTracking, Statistics, Profile + 3 mgmt placeholders |
| Showroom | Coming Soon | Placeholder |

## Architecture mobile
```
mobile/src/
  navigation/    → AppNavigator.tsx (React Navigation)
  screens/
    supplier/    → workflow fournisseur
    driver/      → workflow chauffeur
    client/      → workflow client
    admin/       → dashboard admin
    showroom/    → placeholder
  store/         → useStore.ts (Zustand)
  services/      → api.ts (ApiService + JWT)
  types/         → index.ts
  constants/     → delivery.ts (STATUS_LABELS, STATUS_FLAT_COLORS)
  components/    → composants partagés
```

## Comptes de test (Password: Password123)
| Rôle | Email |
|------|-------|
| Admin | admin@mobilierdefrance.com |
| Supplier | fournisseur@example.com |
| Driver | chauffeur@mobilierdefrance.com |
| Client | client@example.com |

## Backend
- DB : `postgresql://postgres:postgres@localhost/development_db`
- Port : **8001** (8000 souvent bloqué sur WSL2)
- Start : `cd backend && source venv/bin/activate && uvicorn app.main:app --host 0.0.0.0 --port 8001`

## Leçons apprises
- Expo SDK 54 : toujours créer des assets placeholder (icon, splash, favicon) dès le départ
- Zustand + offline sync queue = pattern solide pour apps mobiles avec connectivité variable
- Centraliser STATUS_LABELS et couleurs dans constants/ — évite les divergences entre rôles
- `getBaseUrl()` + env var EXPO_PUBLIC_API_URL plutôt qu'URL hardcodée
- Port 8000 souvent bloqué sur WSL2 → utiliser 8001
