# Quality Tracking App - Project Memory

## Project Overview
- **App**: Quality Tracking for Mobilier de France (furniture delivery tracking)
- **Repo**: github.com:nbayonne76-ui/Quality-tracking-app.git
- **Branch**: `workflow/admin`
- **Stack**: React Native (Expo SDK 54) + FastAPI + PostgreSQL
- **Roles**: Supplier, Driver, Client, Admin, Showroom (coming soon)

## Key Paths
- **Mobile**: `/home/v-nbayonne/Quality-tracking-app/mobile/`
- **Backend**: `/home/v-nbayonne/Quality-tracking-app/backend/`
- **Navigation**: `mobile/src/navigation/AppNavigator.tsx`
- **Store**: `mobile/src/store/useStore.ts` (Zustand)
- **API Service**: `mobile/src/services/api.ts`
- **Types**: `mobile/src/types/index.ts`
- **Constants**: `mobile/src/constants/delivery.ts`

## Architecture
- Navigation: React Navigation v6 (native-stack + bottom-tabs)
- State: Zustand with offline sync queue (AsyncStorage)
- API: `ApiService` class with JWT auth, auto-refresh, `getBaseUrl()`
- Storage: `expo-secure-store` (native) / `localStorage` (web)
- Notifications: `expo-notifications` with web fallback stubs

## Workflow Status (as of Feb 2026)
| Role | Status | Screens |
|------|--------|---------|
| Supplier | Ready | Home, Deliveries, ProductPhotos, TruckLoading, Profile |
| Driver | Ready | Home, Deliveries, DeliveryDetail, Profile |
| Client | Ready | TrackingInput, DeliveryCard, Tracking, DeliveryDetail, Signature, OrderSummary |
| Admin | Ready | Dashboard, LiveTracking, Statistics, Profile + 3 placeholder mgmt screens |
| Showroom | Coming Soon | Placeholder only |

## Database Test Users (Password: `Password123`)
| Role | Email |
|------|-------|
| Admin | admin@mobilierdefrance.com |
| Supplier | fournisseur@example.com |
| Driver | chauffeur@mobilierdefrance.com |
| Client | client@example.com |

## Backend
- Default DB: `postgresql://postgres:postgres@localhost/development_db`
- Port 8000 is often occupied (system-level) — use **port 8001** as fallback
- Start: `cd backend && source venv/bin/activate && uvicorn app.main:app --host 0.0.0.0 --port 8001`
- API URL in mobile configured via `EXPO_PUBLIC_API_URL` env var (`.env` file)

## Completed Audit Fixes (P1-P10)
1. Created placeholder assets (icon, splash, favicon)
2. Wired Client flow (6 screens + navigation)
3. Wired Admin flow (3 screens + tabs + 3 placeholder mgmt)
4. Fixed broken supplier routes
5. Added index.ts barrel exports for all screen folders
6. Fixed French accents in driver screens
7. Consolidated STATUS_LABELS/STATUS_FLAT_COLORS into shared constants
8. Added error state to Zustand store
9. Fixed hardcoded URLs → `getBaseUrl()` + env var
10. Wired admin screens with real store/API data

## Known Issues
- Port 8000 often blocked by system process on WSL2 — use 8001
- `as any` casts on dynamic width percentages in StatisticsScreen (RN TS limitation)
- Admin management screens (Users, Orders, Incidents) are placeholders
- Showroom workflow not implemented yet

See also: [audit-details.md](audit-details.md) for the full audit report

## Happi Brain (cerveau central IA)
- Base de connaissance de TOUS les projets H'appi (27 repos analysés)
- Contient : stack référence, patterns chatbot, secteurs clients, checklist, règles Claude
- **À consulter EN PRIORITÉ** pour tout nouveau chatbot ou projet H'appi
- See [happi_brain.md](happi_brain.md) for the full brain database

## DropOS Project
- New SaaS project at `/home/v-nbayonne/DropOS/`
- One-stop shop dropshipping platform (Next.js + FastAPI + PostgreSQL)
- See [project_dropos.md](project_dropos.md) for full details

## H'appi Foundry Project
- AI platform at `/home/v-nbayonne/ai-foundry/`
- GitHub: github.com/nbayonne76-ui/Happi-Foundry (main branch)
- Stack: Next.js 14 + FastAPI + PostgreSQL
- 19 models across 8 providers, 16 routes
- See [project_happi_foundry.md](project_happi_foundry.md) for roadmap and architecture
