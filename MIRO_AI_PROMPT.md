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

## For Complete Data Flow Diagram (Based on My First Board):

```
Create a comprehensive data flow diagram for Tree Observation App:

START (Green Oval) → Mobile App (Yellow Rectangle)

From Mobile App, create 3 main paths:

PATH 1 - AUTHENTICATION (Upward):
Mobile App → "Login" → JWT Token → "Authentication" → RLS Policies → "Security" → Role Check → "Access control" → Web Admin

PATH 2 - DATA COLLECTION (Rightward):
Mobile App → "Tree observations" → SQLite DB (Local Cache) → "Local cache" → Network Available? (Blue Diamond Decision)
  - If NO: Network Available? → "Wait for Network" → Queue for Sync → Loop back to Network Available?
  - If YES: Network Available? → Sync Engine → "Process queue" → PostgreSQL + PostGIS (Data Storage)

PATH 3 - PHOTO CAPTURE (Downward):
Mobile App → "Photo capture" → FileSystem (Local Storage) → "Local storage" → Upload → "Photo sync" → S3 Storage (Cloud Storage) → "Cloud storage" → Gallery View → "Review photos" → Web Admin

ADDITIONAL FLOWS:
- FileSystem → "GPS location" → Cached Maps → "Offline maps" → Validation → "Coordinate check" → PostGIS → "Spatial data" → Map Dashboard → "Visualize" → Heatmaps → "Density analysis" → END
- PostgreSQL + PostGIS → "Data storage" → Web Admin
- Web Admin → "Review data" → Analytics → "Reports" → END (Green Oval)

SHAPES:
- Green Ovals: Start and End nodes
- Yellow Rectangles: All processes and components
- Blue Diamond: Decision point (Network Available?)
- Cylinders: Databases (SQLite DB, PostgreSQL + PostGIS, S3 Storage)

CONNECTIONS:
- Label all arrows clearly (Start, Login, Tree observations, Photo capture, Local cache, Authentication, Security, Access control, Local storage, Photo sync, Cloud storage, Review photos, GPS location, Offline maps, Coordinate check, Spatial data, Visualize, Density analysis, Data storage, Review data, Reports, Wait for Network, Process queue)
- Show loop from Queue for Sync back to Network Available?

LAYOUT:
- Start at top left
- Mobile App in center left
- Authentication flow goes upward
- Data collection flows rightward
- Photo capture flows downward
- Web Admin in center right
- End at bottom right

COLORS:
- Green: Start/End nodes
- Yellow: All process boxes
- Blue: Decision diamonds
- Use different shades for different component types
```

