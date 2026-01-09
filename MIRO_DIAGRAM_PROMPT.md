# Simple Miro Diagram Prompt

## Tree Observation App - System Architecture

Create a simple 3-layer diagram:

### **TOP: Client Apps (2 boxes side by side)**
1. **📱 Mobile App** - React Native + Expo, SQLite, Mapbox, Supabase Client
2. **💻 Web Admin** - React + Vite, TanStack Table, Mapbox, Supabase Client

### **MIDDLE: Supabase Platform (5 boxes)**
1. **🔐 Auth** - JWT, Email/Password, Roles
2. **🗄️ Database** - PostgreSQL + PostGIS, Tables, RLS
3. **📁 Storage** - S3, Photo Buckets, RLS
4. **⚡ API** - PostgREST, Auto CRUD
5. **🔧 Edge Functions** - Deno, Sync Resolution

### **BOTTOM: External Services (4 boxes)**
1. **🗺️ Mapbox** - Tiles, Geocoding
2. **📊 Monitoring** - Sentry, PostHog
3. **🛠️ DevOps** - GitHub, Actions, EAS
4. **🔧 Admin** - Retool

### **CONNECTIONS:**
- Mobile & Web → HTTPS → All Supabase services
- Mobile & Web → Uses → Mapbox
- Mobile & Web → Reports → Monitoring
- All Supabase services → Connect to → Database
- DevOps → Builds/Deploys → Mobile & Web

### **COLORS:**
- Blue = Mobile App
- Cyan = Web Admin  
- Green = Supabase services
- Yellow = External services

**Keep it simple - one box per service, clear arrows, readable text.**

