# Tree Observation App - Complete System Design Diagram

## 🏗️ Full System Architecture

```mermaid
graph TB
    subgraph "📱 CLIENT LAYER"
        subgraph Mobile["📱 Mobile App (iOS)"]
            subgraph MobileUI["🎨 UI Layer"]
                RN[React Native + Expo]
                RNComponents[React Components]
                NativeWind[NativeWind UI]
            end
            
            subgraph MobileState["🧠 State Management"]
                ZustandMobile[Zustand Store]
                ReactQuery[React Query]
                ReactHookForm[React Hook Form]
            end
            
            subgraph MobileMap["🗺️ Mapping & Location"]
                MapboxNative["Mapbox GL Native<br/>@rnmapbox/maps"]
                ExpoLocation["expo-location"]
                OfflineTiles[Offline Tile Cache]
                GeoJSON[GeoJSON Renderer]
            end
            
            subgraph MobileMedia["📸 Media Handling"]
                ImagePicker["expo-image-picker"]
                Camera["expo-camera"]
                ImageCompress[Image Compression]
            end
            
            subgraph MobileStorage["💾 Local Storage"]
                SQLite["SQLite Database<br/>expo-sqlite"]
                AsyncStorage["AsyncStorage<br/>Key-Value Store"]
                FileSystem["Expo FileSystem<br/>Photo Storage"]
            end
            
            subgraph MobileSync["🔄 Sync Engine"]
                SyncQueue[Sync Queue Manager]
                BackgroundTask["expo-task-manager"]
                NetworkDetect[Network Detection]
                ConflictResolve[Conflict Resolution]
            end
            
            subgraph MobileAPI["🔌 API Layer"]
                SupabaseClientMobile[Supabase JS Client]
                AuthMobile[Auth Token Manager]
            end
            
            subgraph MobileNav["🧭 Navigation"]
                ExpoRouter[Expo Router<br/>File-based Routing]
            end
        end
        
        subgraph Web["💻 Web Admin Dashboard"]
            subgraph WebUI["🎨 UI Layer"]
                React[React 18 + Vite]
                TypeScript[TypeScript]
                Tailwind[Tailwind CSS]
                Shadcn[Shadcn/ui Components]
                LucideIcons[Lucide Icons]
            end
            
            subgraph WebState["🧠 State Management"]
                ZustandWeb[Zustand Store]
                TanStackQuery[TanStack Query]
                ReactHookFormWeb[React Hook Form]
            end
            
            subgraph WebTables["📊 Data Tables"]
                TanStackTable[TanStack Table v8]
                Filters[Filtering & Sorting]
                Pagination[Pagination]
                VirtualScroll[Virtual Scrolling]
            end
            
            subgraph WebMap["🗺️ Map Components"]
                MapboxJS["mapbox-gl"]
                ReactMapGL["react-map-gl"]
                Clustering[Marker Clustering]
                InteractiveMarkers[Interactive Markers]
            end
            
            subgraph WebCharts["📈 Visualization"]
                Recharts[Recharts]
                CustomCharts[Custom D3 Components]
            end
            
            subgraph WebAPI["🔌 API Layer"]
                SupabaseClientWeb[Supabase JS Client]
                RealtimeSub[Realtime Subscriptions]
            end
            
            subgraph WebRouter["🧭 Routing"]
                ReactRouter[React Router v6]
            end
        end
    end
    
    subgraph "🚀 SUPABASE PLATFORM"
        subgraph Auth["🔐 Authentication Service"]
            SupabaseAuth[Supabase Auth]
            JWT[JWT Token Management]
            EmailPassword[Email/Password Auth]
            RoleBased["Role-based Access Control"]
            SessionMgmt[Session Management]
        end
        
        subgraph Database["🗄️ PostgreSQL 15 + PostGIS"]
            Postgres[PostgreSQL Database]
            PostGIS[PostGIS Extension]
            RLS[Row Level Security Policies]
            RealtimeDB[Realtime Subscriptions]
            Triggers[Database Triggers]
            Functions[Database Functions]
            
            subgraph Tables["📋 Database Tables"]
                UsersTable[users<br/>id, email, role, metadata]
                ObservationsTable[observations<br/>id, user_id, location,<br/>species_id, status, survey_data]
                PhotosTable[observation_photos<br/>id, observation_id,<br/>storage_path, thumbnail_path]
                SpeciesTable[species<br/>id, common_name,<br/>scientific_name, category]
                ReviewLogsTable[review_logs<br/>id, observation_id,<br/>reviewer_id, action, comments]
                AuditLogsTable[audit_logs<br/>id, table_name, record_id,<br/>action, old_data, new_data]
            end
            
            subgraph Indexes["🔍 Indexes"]
                SpatialIndex[GIST Spatial Index]
                BTreeIndexes["B-Tree Indexes"]
                CompositeIndexes[Composite Indexes]
            end
        end
        
        subgraph Storage["📁 Storage Service"]
            SupabaseStorage["S3-compatible Storage"]
            PhotoBucket["observation-photos Bucket"]
            ThumbnailBucket[thumbnails Bucket]
            RLSStorage[Storage RLS Policies]
            SignedURLs["Short-lived Signed URLs"]
        end
        
        subgraph API["⚡ API Services"]
            PostgREST[PostgREST<br/>Auto-generated REST API]
            ODataFilter["OData-like Filtering"]
            JWTValidation[JWT Validation]
            AutoCRUD[Auto CRUD Operations]
        end
        
        subgraph Edge["🔧 Edge Functions"]
            EdgeFunctions[Deno Edge Functions]
            SyncConflict[Sync Conflict Resolution]
            BatchProcess[Batch Processing]
            ExternalAPI[External API Integration]
        end
    end
    
    subgraph "🌐 EXTERNAL SERVICES"
        subgraph MapboxServices["🗺️ Mapbox Services"]
            MapboxAPI[Mapbox API]
            TilesAPI[Map Tiles API]
            GeocodingAPI[Geocoding API]
            StaticTiles[Static Tiles API]
            DirectionsAPI[Directions API]
        end
        
        subgraph Monitoring["📊 Monitoring & Analytics"]
            Sentry[Sentry<br/>Error Tracking &<br/>Performance Monitoring]
            PostHog[PostHog<br/>Analytics - Optional]
        end
        
        subgraph DevOps["🛠️ DevOps & CI/CD"]
            GitHub[GitHub<br/>Version Control]
            GitHubActions[GitHub Actions<br/>CI/CD Pipeline]
            ExpoEAS[Expo EAS Build<br/>iOS Builds & TestFlight]
            VercelNetlify[Vercel/Netlify<br/>Web Deployment]
        end
        
        subgraph AdminTools["🔧 Admin Tools"]
            Retool[Retool<br/>Admin Dashboard]
        end
    end
    
    %% Mobile App Internal Connections
    RN --> RNComponents
    RN --> NativeWind
    RN --> ZustandMobile
    RN --> ReactQuery
    RN --> ReactHookForm
    RN --> MapboxNative
    RN --> ExpoLocation
    RN --> ImagePicker
    RN --> Camera
    RN --> SQLite
    RN --> AsyncStorage
    RN --> FileSystem
    RN --> ExpoRouter
    
    ZustandMobile --> ReactQuery
    ReactHookForm --> ZustandMobile
    
    MapboxNative --> OfflineTiles
    MapboxNative --> GeoJSON
    ExpoLocation --> MapboxNative
    
    ImagePicker --> ImageCompress
    Camera --> ImageCompress
    ImageCompress --> FileSystem
    
    SQLite --> SyncQueue
    FileSystem --> SyncQueue
    SyncQueue --> BackgroundTask
    SyncQueue --> NetworkDetect
    SyncQueue --> ConflictResolve
    
    SupabaseClientMobile --> AuthMobile
    SyncQueue --> SupabaseClientMobile
    
    %% Web Admin Internal Connections
    React --> TypeScript
    React --> Tailwind
    React --> Shadcn
    React --> LucideIcons
    React --> ZustandWeb
    React --> TanStackQuery
    React --> TanStackTable
    React --> MapboxJS
    React --> Recharts
    React --> ReactRouter
    
    ZustandWeb --> TanStackQuery
    TanStackTable --> Filters
    TanStackTable --> Pagination
    TanStackTable --> VirtualScroll
    
    MapboxJS --> ReactMapGL
    ReactMapGL --> Clustering
    ReactMapGL --> InteractiveMarkers
    
    SupabaseClientWeb --> RealtimeSub
    
    %% Mobile to Supabase Connections
    SupabaseClientMobile -->|HTTPS| SupabaseAuth
    SupabaseClientMobile -->|HTTPS| PostgREST
    SupabaseClientMobile -->|HTTPS| SupabaseStorage
    SupabaseClientMobile -->|HTTPS| EdgeFunctions
    SyncQueue -->|Background Upload| SupabaseStorage
    SyncQueue -->|Background Upload| PostgREST
    
    %% Web to Supabase Connections
    SupabaseClientWeb -->|HTTPS| SupabaseAuth
    SupabaseClientWeb -->|HTTPS| PostgREST
    SupabaseClientWeb -->|HTTPS| SupabaseStorage
    SupabaseClientWeb -->|HTTPS| RealtimeDB
    
    %% Supabase Internal Connections
    SupabaseAuth --> JWT
    SupabaseAuth --> EmailPassword
    SupabaseAuth --> RoleBased
    SupabaseAuth --> SessionMgmt
    SupabaseAuth -->|Validates| Postgres
    
    PostgREST -->|Queries| Postgres
    PostgREST -->|Validates| JWT
    PostgREST -->|Applies| RLS
    
    Postgres --> PostGIS
    Postgres --> RLS
    Postgres --> RealtimeDB
    Postgres --> Triggers
    Postgres --> Functions
    Postgres --> UsersTable
    Postgres --> ObservationsTable
    Postgres --> PhotosTable
    Postgres --> SpeciesTable
    Postgres --> ReviewLogsTable
    Postgres --> AuditLogsTable
    
    ObservationsTable -->|FK| UsersTable
    ObservationsTable -->|FK| SpeciesTable
    ObservationsTable -->|FK| PhotosTable
    ReviewLogsTable -->|FK| ObservationsTable
    ReviewLogsTable -->|FK| UsersTable
    AuditLogsTable -->|FK| UsersTable
    
    PostGIS --> SpatialIndex
    ObservationsTable --> SpatialIndex
    
    SupabaseStorage --> PhotoBucket
    SupabaseStorage --> ThumbnailBucket
    SupabaseStorage --> RLSStorage
    SupabaseStorage --> SignedURLs
    RLSStorage -->|Enforced by| RLS
    
    EdgeFunctions -->|Accesses| Postgres
    EdgeFunctions -->|Processes| SyncConflict
    EdgeFunctions -->|Handles| BatchProcess
    
    %% External Services Connections
    MapboxNative -->|API Calls| MapboxAPI
    MapboxJS -->|API Calls| MapboxAPI
    MapboxAPI --> TilesAPI
    MapboxAPI --> GeocodingAPI
    MapboxAPI --> StaticTiles
    OfflineTiles -->|Caches| StaticTiles
    
    Mobile -->|Error Reports| Sentry
    Web -->|Error Reports| Sentry
    Sentry -->|Monitors| PostHog
    
    GitHub -->|Triggers| GitHubActions
    GitHubActions -->|Builds| ExpoEAS
    GitHubActions -->|Deploys| VercelNetlify
    ExpoEAS -->|Submits| TestFlight
    
    Retool -->|Connects to| PostgREST
    Retool -->|Manages| UsersTable
    Retool -->|Reviews| ObservationsTable
    
    %% Data Flow Annotations
    classDef mobileApp fill:#4A90E2,stroke:#2E5C8A,stroke-width:3px,color:#fff
    classDef webApp fill:#61DAFB,stroke:#2E5C8A,stroke-width:3px,color:#000
    classDef backend fill:#3ECF8E,stroke:#2E5C8A,stroke-width:3px,color:#fff
    classDef external fill:#FFD93D,stroke:#2E5C8A,stroke-width:3px,color:#000
    classDef storage fill:#9B59B6,stroke:#2E5C8A,stroke-width:3px,color:#fff
    classDef security fill:#E74C3C,stroke:#2E5C8A,stroke-width:3px,color:#fff
    
    class RN,RNComponents,NativeWind,ZustandMobile,ReactQuery,ReactHookForm,MapboxNative,ExpoLocation,OfflineTiles,GeoJSON,ImagePicker,Camera,ImageCompress,SQLite,AsyncStorage,FileSystem,SyncQueue,BackgroundTask,NetworkDetect,ConflictResolve,SupabaseClientMobile,AuthMobile,ExpoRouter mobileApp
    class React,TypeScript,Tailwind,Shadcn,LucideIcons,ZustandWeb,TanStackQuery,ReactHookFormWeb,TanStackTable,Filters,Pagination,VirtualScroll,MapboxJS,ReactMapGL,Clustering,InteractiveMarkers,Recharts,CustomCharts,SupabaseClientWeb,RealtimeSub,ReactRouter webApp
    class Postgres,PostGIS,RLS,RealtimeDB,Triggers,Functions,UsersTable,ObservationsTable,PhotosTable,SpeciesTable,ReviewLogsTable,AuditLogsTable,SpatialIndex,BTreeIndexes,CompositeIndexes,PostgREST,ODataFilter,JWTValidation,AutoCRUD,EdgeFunctions,SyncConflict,BatchProcess,ExternalAPI backend
    class SupabaseAuth,JWT,EmailPassword,RoleBased,SessionMgmt,RLSStorage,SignedURLs security
    class SupabaseStorage,PhotoBucket,ThumbnailBucket,FileSystem,SQLite,AsyncStorage storage
    class MapboxAPI,TilesAPI,GeocodingAPI,StaticTiles,DirectionsAPI,Sentry,PostHog,GitHub,GitHubActions,ExpoEAS,VercelNetlify,Retool external
```

---

## 🔄 Complete Data Flow Diagram

```mermaid
flowchart TD
    Start([Start]) --> MobileApp[📱 Mobile App]
    
    MobileApp --> Login[Login]
    Login --> JWTToken[🔐 JWT Token]
    JWTToken --> RLSPolicies[RLS Policies]
    RLSPolicies --> Authentication[Authentication]
    Authentication --> RoleCheck[Role Check]
    RoleCheck --> AccessControl[Access Control]
    AccessControl --> WebAdmin[💻 Web Admin]
    
    MobileApp --> TreeObservations[🌳 Tree Observations]
    MobileApp --> PhotoCapture[📸 Photo Capture]
    
    TreeObservations --> SQLiteDB[(SQLite DB<br/>Local Cache)]
    PhotoCapture --> FileSystem[📁 FileSystem<br/>Local Storage]
    
    FileSystem --> GPSLocation[📍 GPS Location]
    FileSystem --> Upload[⬆️ Upload]
    
    GPSLocation --> CachedMaps[🗺️ Cached Maps]
    CachedMaps --> OfflineMaps[Offline Maps]
    OfflineMaps --> Validation[✅ Validation]
    
    SQLiteDB --> NetworkCheck{🌐 Network<br/>Available?}
    
    NetworkCheck -->|NO| QueueSync[📋 Queue for Sync]
    QueueSync --> WaitNetwork[⏳ Wait for Network]
    WaitNetwork --> NetworkCheck
    
    NetworkCheck -->|YES| SyncEngine[🔄 Sync Engine]
    SyncEngine --> ProcessQueue[Process Queue]
    ProcessQueue --> PostgreSQL[(PostgreSQL + PostGIS<br/>Data Storage)]
    
    Upload --> PhotoSync[📤 Photo Sync]
    PhotoSync --> S3Storage[(S3 Storage<br/>Cloud Storage)]
    S3Storage --> GalleryView[🖼️ Gallery View]
    GalleryView --> ReviewPhotos[Review Photos]
    ReviewPhotos --> WebAdmin
    
    Validation --> CoordinateCheck[📍 Coordinate Check]
    CoordinateCheck --> PostGIS[🗺️ PostGIS]
    PostGIS --> SpatialData[Spatial Data]
    SpatialData --> MapDashboard[🗺️ Map Dashboard]
    MapDashboard --> Visualize[👁️ Visualize]
    Visualize --> Heatmaps[🔥 Heatmaps]
    Heatmaps --> DensityAnalysis[Density Analysis]
    
    PostgreSQL --> WebAdmin
    WebAdmin --> ReviewData[📊 Review Data]
    ReviewData --> Analytics[📈 Analytics]
    Analytics --> Reports[📄 Reports]
    
    Reports --> End([End])
    DensityAnalysis --> End
    
    %% Styling
    classDef mobile fill:#4A90E2,stroke:#2E5C8A,stroke-width:3px,color:#fff
    classDef storage fill:#9B59B6,stroke:#2E5C8A,stroke-width:3px,color:#fff
    classDef backend fill:#3ECF8E,stroke:#2E5C8A,stroke-width:3px,color:#fff
    classDef web fill:#61DAFB,stroke:#2E5C8A,stroke-width:3px,color:#000
    classDef security fill:#E74C3C,stroke:#2E5C8A,stroke-width:3px,color:#fff
    classDef decision fill:#FFD93D,stroke:#2E5C8A,stroke-width:3px,color:#000
    classDef process fill:#3498DB,stroke:#2E5C8A,stroke-width:2px,color:#fff
    
    class MobileApp,TreeObservations,PhotoCapture,FileSystem,GPSLocation,CachedMaps,OfflineMaps,Upload,QueueSync,WaitNetwork mobile
    class SQLiteDB,S3Storage,FileSystem storage
    class PostgreSQL,PostGIS,SyncEngine,ProcessQueue,PhotoSync backend
    class WebAdmin,GalleryView,ReviewPhotos,ReviewData,Analytics,Reports,MapDashboard,Visualize,Heatmaps,DensityAnalysis web
    class JWTToken,RLSPolicies,Authentication,RoleCheck,AccessControl security
    class NetworkCheck,Validation,CoordinateCheck decision
    class Login,Start,End process
```

### **Data Flow Stages**

#### **1. Authentication & Access Control**
- User logs into Mobile App
- JWT Token generated and validated
- RLS Policies enforce security
- Role Check determines access level
- Access Control granted to Web Admin

#### **2. Mobile Data Collection**
- **Tree Observations**: Captured and stored in SQLite DB (Local Cache)
- **Photo Capture**: Stored in FileSystem (Local Storage)
- **GPS Location**: Captured and used for map caching

#### **3. Offline Capabilities**
- **Cached Maps**: GPS location enables offline map functionality
- **Offline Maps**: Available for validation without network
- **Local Cache**: SQLite DB stores observations offline
- **Local Storage**: FileSystem stores photos offline

#### **4. Network Detection & Sync Queue**
- System checks if network is available
- If **NO**: Data goes to Queue for Sync → Wait for Network → Re-check
- If **YES**: Data proceeds to Sync Engine

#### **5. Synchronization Process**
- Sync Engine processes the queue
- Observations synced to PostgreSQL + PostGIS
- Photos uploaded to S3 Storage (Cloud Storage)
- Gallery View displays synced photos

#### **6. Spatial Data Processing**
- Validation performs Coordinate Check
- PostGIS processes Spatial Data
- Map Dashboard visualizes data
- Heatmaps show Density Analysis

#### **7. Web Administration**
- Web Admin receives data from PostgreSQL
- Review Photos from Gallery View
- Review Data processed by Analytics
- Reports generated for analysis

#### **8. Visualization & Analytics**
- Map Dashboard provides spatial visualization
- Heatmaps show observation density
- Analytics processes reviewed data
- Reports generated for stakeholders

---

## 📊 System Components Overview

### **Client Layer**

#### **Mobile App (iOS)**
- **UI Layer**: React Native with Expo, NativeWind for styling
- **State Management**: Zustand for global state, React Query for server state, React Hook Form for forms
- **Mapping**: Mapbox GL Native with offline tile caching and GeoJSON rendering
- **Media**: Image picker, camera, and compression utilities
- **Local Storage**: SQLite for structured data, AsyncStorage for key-value, FileSystem for photos
- **Sync Engine**: Background sync with queue management, network detection, and conflict resolution
- **API**: Supabase client with auth token management
- **Navigation**: Expo Router for file-based routing

#### **Web Admin Dashboard**
- **UI Layer**: React 18 with Vite, TypeScript, Tailwind CSS, Shadcn/ui components
- **State Management**: Zustand, TanStack Query, React Hook Form
- **Data Tables**: TanStack Table with filtering, sorting, pagination, and virtual scrolling
- **Mapping**: Mapbox GL JS with clustering and interactive markers
- **Visualization**: Recharts and custom D3 components
- **API**: Supabase client with realtime subscriptions
- **Routing**: React Router v6

### **Supabase Platform**

#### **Authentication Service**
- JWT token management
- Email/Password authentication
- Role-based access control (Contributor, Reviewer, Admin)
- Session management

#### **Database (PostgreSQL + PostGIS)**
- **Core Tables**: users, observations, observation_photos, species, review_logs, audit_logs
- **PostGIS**: Spatial data storage and queries (geography POINT, SRID 4326)
- **Row Level Security**: Policies enforcing role-based data access
- **Realtime**: Subscriptions for live updates
- **Indexes**: GIST spatial indexes, B-Tree indexes, composite indexes
- **Triggers & Functions**: Automated database logic

#### **Storage Service**
- S3-compatible storage
- Separate buckets for photos and thumbnails
- RLS policies for access control
- Short-lived signed URLs for secure access

#### **API Services**
- PostgREST auto-generated REST API
- OData-like filtering capabilities
- JWT validation on all requests
- Automatic CRUD operations

#### **Edge Functions**
- Deno runtime for custom business logic
- Sync conflict resolution
- Batch processing capabilities
- External API integrations

### **External Services**

#### **Mapbox Services**
- Map tiles API for rendering
- Geocoding API for address lookups
- Static tiles API for offline caching
- Directions API (optional)

#### **Monitoring & Analytics**
- Sentry for error tracking and performance monitoring
- PostHog for analytics (optional)

#### **DevOps & CI/CD**
- GitHub for version control
- GitHub Actions for CI/CD pipeline
- Expo EAS for iOS builds and TestFlight distribution
- Vercel/Netlify for web deployment

#### **Admin Tools**
- Retool for admin dashboard and data management

---

## 🔄 Key Data Flows

### **1. Offline Data Creation (Mobile)**
```
User Input → React Components → Zustand Store → SQLite Database
                                    ↓
                            FileSystem (Photos)
                                    ↓
                            Sync Queue (Pending)
```

### **2. Background Sync (Mobile)**
```
Network Detected → Sync Queue → Upload Photos to Storage
                                    ↓
                            Create Observation via API
                                    ↓
                            Update SQLite (Synced)
```

### **3. Admin Review (Web)**
```
Admin Dashboard → PostgREST API → PostgreSQL
                                    ↓
                            Query Observations
                                    ↓
                            Update Status
                                    ↓
                            Create Audit Log
```

### **4. Realtime Updates**
```
PostgreSQL Change → Realtime Subscription → Web Dashboard
                                    ↓
                            Mobile App (Poll/Realtime)
                                    ↓
                            Update Local SQLite
```

---

## 🔐 Security Architecture

### **Authentication Flow**
```
Client → Supabase Auth → JWT Token → PostgREST → RLS Policies → Database
```

### **Row Level Security**
- **Contributors**: Can only access their own observations
- **Reviewers**: Can read all submitted observations, can approve/reject
- **Admins**: Full access to all data and system management

### **Storage Security**
- Private buckets with RLS policies
- Short-lived signed URLs (expires after set time)
- Path-based access control tied to database records

---

## 📈 Performance Optimizations

### **Mobile App**
- Virtualized lists (FlashList)
- Image lazy loading & caching
- Map marker clustering
- Optimistic UI updates
- Debounced search
- Background sync throttling

### **Web Admin**
- Virtual scrolling (TanStack Virtual)
- Lazy loading routes
- Memoized calculations
- Web Workers for heavy processing
- Progressive loading for large datasets

### **Database**
- PostGIS spatial indexes (GIST)
- Compound indexes on frequently queried columns
- Materialized views for dashboard stats
- Query optimization with EXPLAIN ANALYZE

---

## 🚀 Scalability Considerations

### **Current Architecture (Phase 1)**
- Single region deployment
- Manual review process
- iOS only
- Basic analytics
- ~10K observations capacity

### **Future Scaling**
- Multi-region Supabase deployment
- ML-assisted review
- Android + Web PWA support
- Advanced BI dashboards
- Millions of records capacity

---

*This comprehensive system design diagram represents the complete architecture of the Tree Observation App, including all layers, services, data flows, and integrations.*

