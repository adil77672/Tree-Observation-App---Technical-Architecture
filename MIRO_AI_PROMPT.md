# Miro AI Prompt - Tree Observation App System Architecture

## Copy this prompt to Miro AI:

```
Create a system architecture diagram for a Tree Observation App with 4 horizontal layers:

LAYER 1 (Top - Blue): CLIENT APPLICATIONS
- Mobile App iOS box: React Native + Expo, UI Components, State Management (Zustand, React Query), Mapbox GL Native, Camera/Image Picker, SQLite/FileSystem Storage, Background Sync Engine, Expo Router
- Web Admin Dashboard box: React 18 + Vite + TypeScript, Shadcn/ui Components, TanStack Table & Query, Mapbox GL JS, Recharts Charts, React Router

LAYER 2 (Second - Purple): API LAYER  
- Mobile API Client box: Supabase JS Client, Auth Token Management, Offline Queue Handler, Background Sync
- Web API Client box: Supabase JS Client, Realtime Subscriptions, Query Builder, File Upload Handler

LAYER 3 (Third - Green): SUPABASE PLATFORM
- Authentication Service box: Supabase Auth, JWT Tokens, Email/Password Auth, Role-based Access Control, Session Management
- REST API Service box: PostgREST API, Auto CRUD, OData Filtering, JWT Validation, Query Optimization
- Database Service cylinder: PostgreSQL 15, PostGIS Extension, Row Level Security, Realtime Engine, Tables: users, observations, observation_photos, species, review_logs, audit_logs
- Storage Service box: S3-compatible Storage, Photo Buckets, Thumbnail Generation, RLS Policies, Signed URLs
- Edge Functions box: Deno Runtime, Sync Conflict Resolution, Batch Processing, External API Integration

LAYER 4 (Bottom - Yellow): EXTERNAL SERVICES
- Mapbox Services box: Map Tiles API, Geocoding API, Static Tiles, Directions API
- Monitoring Services box: Sentry Error Tracking, Performance Monitoring, PostHog Analytics
- DevOps Services box: GitHub, GitHub Actions CI/CD, Expo EAS Builds, Vercel/Netlify Deployment
- Admin Tools box: Retool Dashboard

CONNECTIONS:
- Mobile App → Mobile API Client
- Web App → Web API Client
- Mobile API Client → HTTPS → Authentication Service, REST API, Storage, Edge Functions
- Web API Client → HTTPS → Authentication Service, REST API, Storage, Realtime
- Authentication Service → Validates → Database
- REST API → Queries → Database
- Storage → Enforces → Database
- Edge Functions → Accesses → Database
- Mobile App → Uses → Mapbox Services
- Mobile App → Reports → Monitoring
- Web App → Uses → Mapbox Services
- Web App → Reports → Monitoring
- DevOps → Builds → Mobile App
- DevOps → Deploys → Web App
- Admin Tools → Connects → REST API

COLORS: Blue for Mobile, Cyan for Web, Purple for API Layer, Green for Backend, Yellow for External Services, Red for Security components.

Make boxes large and readable with clear labels. Use arrows with labels showing connection types (HTTPS, Uses, Reports, etc.).
```

---

## Alternative Shorter Version:

```
Create a 4-layer system architecture: 
1) Client Apps: Mobile App (React Native) and Web Admin (React)
2) API Layer: Mobile and Web API Clients (Supabase)
3) Backend: Supabase Platform with Auth, Database (PostgreSQL+PostGIS), Storage, REST API, Edge Functions
4) External: Mapbox, Monitoring (Sentry), DevOps (GitHub/Actions), Admin Tools (Retool)

Show connections: Clients → API → Backend → External Services. Use color coding: Blue (Mobile), Cyan (Web), Green (Backend), Yellow (External).
```

---

## For Data Flow Diagram:

```
Create a data flow diagram showing:
1. User logs into Mobile App
2. Creates observation: Capture Photo → Get GPS → Fill Form → Save to SQLite
3. Network check: If offline → Queue for Sync, If online → Sync Engine
4. Sync: Upload Photos to S3 → Create DB Record → Update Local Status
5. Web Admin: Load Data → Review → Approve/Reject → Update Status → Notify Mobile
6. Mobile: Receive Status Update → Update Local SQLite

Use decision diamonds for Network Available and Approve/Reject. Use rectangles for processes, cylinders for databases. Color code: Blue (Mobile processes), Green (Backend), Cyan (Web), Purple (Storage).
```

