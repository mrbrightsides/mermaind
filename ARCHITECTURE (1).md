# 🏗️ **MERMAIND ARCHITECTURE**

Technical architecture and design documentation for contributors and maintainers.

---

## 📋 **Table of Contents**

- [Overview](#overview)
- [Tech Stack](#tech-stack)
- [Architecture Diagram](#architecture-diagram)
- [Directory Structure](#directory-structure)
- [Core Components](#core-components)
- [Data Flow](#data-flow)
- [API Design](#api-design)
- [State Management](#state-management)
- [Performance](#performance)
- [Security](#security)
- [Future Architecture](#future-architecture)

---

## 🌟 **Overview**

Mermaind is built as a **modern, serverless web application** using Next.js 14 with the App Router. The architecture follows these principles:

- **Serverless-First**: Edge functions for API routes
- **Offline-First**: LocalStorage for client-side persistence
- **AI-Enhanced**: Perplexity integration for intelligent diagram generation
- **Type-Safe**: Full TypeScript coverage
- **Component-Based**: Modular React architecture
- **Progressive Enhancement**: Works without JavaScript (base functionality)

---

## 🛠️ **Tech Stack**

### **Frontend**
```yaml
Framework: Next.js 14 (App Router)
Language: TypeScript 5.x
Styling: Tailwind CSS 3.x
UI Components: Radix UI
Diagram Engine: Mermaid.js 10.x
State: React Hooks (useState, useEffect, useCallback)
Export: html2canvas, jsPDF
```

### **Backend**
```yaml
Runtime: Next.js Edge Runtime
API: RESTful (Next.js API Routes)
AI: Perplexity API (pplx-70b-online)
Storage: LocalStorage (browser)
Future: Supabase (PostgreSQL + Auth)
```

### **DevOps**
```yaml
Hosting: Vercel
CI/CD: GitHub Actions (planned)
Monitoring: Vercel Analytics
Error Tracking: Sentry (planned)
```

---

## 📐 **Architecture Diagram**

```
┌─────────────────────────────────────────────────────────────┐
│                         FRONTEND                            │
│  ┌─────────────────────────────────────────────────────┐   │
│  │            Next.js App (React)                       │   │
│  │  ┌──────────────┐  ┌──────────────┐  ┌───────────┐ │   │
│  │  │   UI Layer   │  │  Logic Layer │  │  Storage  │ │   │
│  │  │              │  │              │  │  Layer    │ │   │
│  │  │ - Components │  │ - Hooks      │  │           │ │   │
│  │  │ - Radix UI   │  │ - Services   │  │ LocalStor.│ │   │
│  │  │ - Tailwind   │  │ - Utils      │  │           │ │   │
│  │  └──────────────┘  └──────────────┘  └───────────┘ │   │
│  └─────────────────────────────────────────────────────┘   │
└─────────────────────────────────────────────────────────────┘
                            │
                            │ HTTPS
                            ▼
┌─────────────────────────────────────────────────────────────┐
│                    API LAYER (Edge)                         │
│  ┌──────────────┐  ┌──────────────┐  ┌──────────────┐     │
│  │   Diagram    │  │  Templates   │  │  Analytics   │     │
│  │  Generation  │  │    Access    │  │   Tracking   │     │
│  └──────────────┘  └──────────────┘  └──────────────┘     │
└─────────────────────────────────────────────────────────────┘
                            │
                            │ HTTPS
                            ▼
┌─────────────────────────────────────────────────────────────┐
│                  EXTERNAL SERVICES                          │
│  ┌──────────────┐  ┌──────────────┐  ┌──────────────┐     │
│  │  Perplexity  │  │   Mermaid    │  │   Vercel     │     │
│  │     AI       │  │   Renderer   │  │   Hosting    │     │
│  └──────────────┘  └──────────────┘  └──────────────┘     │
└─────────────────────────────────────────────────────────────┘
```

---

## 📁 **Directory Structure**

```
mermaind/
├── src/
│   ├── app/                    # Next.js App Router
│   │   ├── page.tsx           # Main application page
│   │   ├── layout.tsx         # Root layout with metadata
│   │   ├── globals.css        # Global styles
│   │   └── api/               # API routes
│   │       ├── generate-diagram/
│   │       ├── proxy/
│   │       └── v1/
│   │           ├── diagram/
│   │           └── templates/
│   │
│   ├── components/            # React components
│   │   ├── ui/               # Base UI components (Radix)
│   │   │   ├── button.tsx
│   │   │   ├── input.tsx
│   │   │   ├── card.tsx
│   │   │   └── ...
│   │   │
│   │   ├── diagram-renderer.tsx
│   │   ├── citation-generator.tsx
│   │   ├── reference-manager-export.tsx
│   │   ├── overleaf-integration.tsx
│   │   ├── commenting-system.tsx
│   │   ├── version-control-system.tsx
│   │   ├── analytics-dashboard.tsx
│   │   ├── context-analyzer.tsx
│   │   ├── advanced-template-builder.tsx
│   │   ├── api-key-management.tsx
│   │   └── enhanced-export-manager.tsx
│   │
│   ├── lib/                   # Core services and utilities
│   │   ├── diagramService.ts
│   │   ├── enhancedAIService.ts
│   │   ├── referenceManagerService.ts
│   │   ├── overleafService.ts
│   │   ├── commentingService.ts
│   │   ├── versionControlService.ts
│   │   ├── analyticsService.ts
│   │   ├── apiKeyService.ts
│   │   └── utils.ts
│   │
│   ├── types/                 # TypeScript definitions
│   │   └── diagram.ts
│   │
│   ├── data/                  # Static data
│   │   └── academicTemplates.ts
│   │
│   └── hooks/                 # Custom React hooks (planned)
│       └── useDiagram.ts
│
├── public/                    # Static assets
│   ├── icons/
│   └── images/
│
├── docs/                      # Documentation
│   ├── README.md
│   ├── API.md
│   ├── CONTRIBUTING.md
│   ├── CHANGELOG.md
│   └── ARCHITECTURE.md
│
├── .env.local                # Environment variables (gitignored)
├── .env.example              # Environment template
├── next.config.js            # Next.js configuration
├── tailwind.config.ts        # Tailwind configuration
├── tsconfig.json             # TypeScript configuration
└── package.json              # Dependencies
```

---

## 🧩 **Core Components**

### **1. Main Application (`src/app/page.tsx`)**

**Responsibility**: Orchestrates the entire application

**Key Features**:
- Prompt input and validation
- Diagram type selection
- Real-time suggestions
- Feature modal management
- Export coordination

**State Management**:
```typescript
const [prompt, setPrompt] = useState<string>('');
const [diagramType, setDiagramType] = useState<DiagramType>('flowchart');
const [generatedSVG, setGeneratedSVG] = useState<string>('');
const [isGenerating, setIsGenerating] = useState<boolean>(false);
// ... modal states for each feature
```

### **2. Diagram Service (`src/lib/diagramService.ts`)**

**Responsibility**: Core diagram generation logic

**Key Functions**:
- `generateDiagram()`: AI-enhanced generation
- `generateMermaidCode()`: Mermaid syntax creation
- `validatePrompt()`: Input validation
- `renderDiagram()`: SVG rendering

**AI Integration**:
```typescript
async function generateDiagram(
  prompt: string,
  type: DiagramType
): Promise<DiagramData> {
  // 1. Validate prompt
  validatePrompt(prompt);
  
  // 2. Call Perplexity AI
  const aiResponse = await callPerplexityAPI(prompt, type);
  
  // 3. Extract structured data
  const structured = parseAIResponse(aiResponse);
  
  // 4. Generate Mermaid code
  const mermaidCode = generateMermaidCode(structured, type);
  
  // 5. Render SVG
  const svg = await renderMermaid(mermaidCode);
  
  return { mermaidCode, svg, metadata };
}
```

### **3. Enhanced AI Service (`src/lib/enhancedAIService.ts`)**

**Responsibility**: Multi-model AI orchestration

**Features**:
- Primary: Perplexity API
- Fallbacks: GPT-4, Claude (future)
- Context-aware prompting
- Response caching
- Error recovery

**Design Pattern**: Circuit Breaker
```typescript
class AIService {
  private circuitBreaker = new CircuitBreaker({
    failureThreshold: 3,
    resetTimeout: 60000
  });
  
  async generate(prompt: string): Promise<AIResponse> {
    return this.circuitBreaker.execute(async () => {
      try {
        return await this.perplexity.generate(prompt);
      } catch (error) {
        return await this.fallback.generate(prompt);
      }
    });
  }
}
```

### **4. Component Architecture**

**Base UI Components** (`src/components/ui/`)
- Built on Radix UI primitives
- Fully accessible (ARIA)
- Themeable via CSS variables
- Type-safe props

**Feature Components** (`src/components/`)
- Self-contained functionality
- Props-based communication
- Event-driven updates
- Lazy-loaded modals

---

## 🔄 **Data Flow**

### **Diagram Generation Flow**

```
User Input
    ↓
Validation
    ↓
AI Processing (Perplexity)
    ↓
Structured Data Extraction
    ↓
Mermaid Code Generation
    ↓
SVG Rendering (Mermaid.js)
    ↓
Display + Storage (LocalStorage)
    ↓
Export Options Available
```

### **State Flow**

```
┌─────────────┐
│  Component  │
│   (React)   │
└─────────────┘
      │
      │ useState
      ↓
┌─────────────┐
│  Local      │
│  State      │
└─────────────┘
      │
      │ useEffect
      ↓
┌─────────────┐
│  Local      │
│  Storage    │
└─────────────┘
```

**Future with Backend**:
```
Component → Local State → API → Database → Realtime Sync
```

---

## 🔌 **API Design**

### **REST API Structure**

**Base**: `/api/v1`

**Endpoints**:
```
POST   /api/v1/diagram      # Generate diagram
GET    /api/v1/templates    # List templates
GET    /api/v1/templates/:id # Get specific template
POST   /api/v1/auth/login  # (Future) User auth
GET    /api/v1/user/diagrams # (Future) User diagrams
```

### **Request/Response Format**

**Request**:
```typescript
interface DiagramRequest {
  prompt: string;
  type: DiagramType;
  style?: 'academic' | 'minimal' | 'professional';
  options?: {
    theme?: string;
    width?: number;
    height?: number;
  };
}
```

**Response**:
```typescript
interface APIResponse<T> {
  success: boolean;
  data?: T;
  error?: {
    code: string;
    message: string;
    details?: Record<string, unknown>;
  };
}
```

### **Error Handling**

**HTTP Status Codes**:
- `200`: Success
- `400`: Bad Request (validation error)
- `401`: Unauthorized (invalid API key)
- `429`: Rate Limit Exceeded
- `500`: Internal Server Error

**Error Response**:
```json
{
  "success": false,
  "error": {
    "code": "INVALID_PROMPT",
    "message": "Prompt must be at least 10 characters",
    "details": {
      "minLength": 10,
      "providedLength": 5
    }
  }
}
```

---

## 🗄️ **State Management**

### **Current: React Hooks + LocalStorage**

**Advantages**:
- Simple, no external dependencies
- Works offline
- Fast read/write
- No backend required

**Limitations**:
- 5MB storage limit
- No cross-device sync
- No multi-user collaboration
- Data loss on cache clear

### **Future: Redux/Zustand + Supabase**

```typescript
// Global state store
interface AppStore {
  user: User | null;
  diagrams: Diagram[];
  templates: Template[];
  collaborators: User[];
  
  // Actions
  generateDiagram: (prompt: string) => Promise<void>;
  saveDiagram: (diagram: Diagram) => Promise<void>;
  syncWithCloud: () => Promise<void>;
}
```

---

## ⚡ **Performance**

### **Current Optimizations**

1. **Code Splitting**
   ```typescript
   // Lazy load heavy components
   const OverleafIntegration = dynamic(
     () => import('./overleaf-integration'),
     { loading: () => <Spinner /> }
   );
   ```

2. **Memoization**
   ```typescript
   const memoizedDiagram = useMemo(
     () => renderDiagram(mermaidCode),
     [mermaidCode]
   );
   ```

3. **Debounced Input**
   ```typescript
   const debouncedPrompt = useDebounce(prompt, 500);
   ```

4. **Edge Runtime**
   ```typescript
   export const runtime = 'edge'; // Fast API responses
   ```

### **Performance Metrics** (Target)

| Metric | Target | Current |
|--------|--------|---------|
| First Contentful Paint | < 1.5s | ~1.2s |
| Time to Interactive | < 3.0s | ~2.5s |
| Largest Contentful Paint | < 2.5s | ~2.0s |
| API Response Time | < 2.0s | ~1.8s |

### **Future Optimizations**

- Server-side rendering for initial content
- Image optimization with Next.js Image
- Database query optimization
- CDN caching for templates
- WebAssembly for heavy computations

---

## 🔒 **Security**

### **Current Security Measures**

1. **API Key Authentication**
   - Bearer token validation
   - Rate limiting per key
   - Key rotation support

2. **Input Validation**
   - Prompt length limits
   - Type checking
   - XSS prevention

3. **CORS Configuration**
   - Restricted origins
   - Proper headers

4. **Environment Variables**
   - Secrets in `.env.local`
   - Never committed to Git

### **Future Security Enhancements**

1. **Authentication & Authorization**
   - JWT-based auth
   - OAuth providers (Google, GitHub)
   - Role-based access control (RBAC)

2. **Data Encryption**
   - At-rest encryption (database)
   - In-transit encryption (HTTPS)
   - End-to-end encryption for sensitive diagrams

3. **Security Headers**
   ```typescript
   // next.config.js
   async headers() {
     return [{
       source: '/(.*)',
       headers: [
         { key: 'X-Frame-Options', value: 'DENY' },
         { key: 'X-Content-Type-Options', value: 'nosniff' },
         { key: 'X-XSS-Protection', value: '1; mode=block' },
         { key: 'Strict-Transport-Security', value: 'max-age=63072000' }
       ]
     }];
   }
   ```

4. **Dependency Scanning**
   - Automated vulnerability checks
   - Regular dependency updates
   - npm audit integration

---

## 🔮 **Future Architecture**

### **Phase 1: Backend Integration (Q2 2024)**

```
Frontend (Next.js)
    ↓ REST API
Backend (Supabase)
    ├── PostgreSQL (data)
    ├── Auth (users)
    ├── Storage (files)
    └── Realtime (sync)
```

**New Features**:
- User accounts
- Cloud storage
- Cross-device sync
- Data persistence

### **Phase 2: Real-time Collaboration (Q2-Q3 2024)**

```
Frontend (Next.js)
    ↓ WebSocket
Collaboration Server
    ├── Operational Transformation
    ├── Conflict Resolution
    └── Live Cursor Tracking
```

**New Features**:
- Simultaneous editing
- Live cursors
- Change propagation
- Conflict resolution

### **Phase 3: Mobile Apps (Q3 2024)**

```
Mobile Apps (React Native)
    ↓ REST API
Backend (Supabase)
    └── Same backend as web
```

**New Features**:
- iOS/Android apps
- Offline mode
- Push notifications
- Native performance

### **Phase 4: Microservices (Q4 2024)**

```
API Gateway
    ├── Diagram Service (Node.js)
    ├── AI Service (Python)
    ├── Export Service (Go)
    ├── Collaboration Service (Rust)
    └── Analytics Service (Node.js)
```

**Benefits**:
- Independent scaling
- Language optimization
- Better fault isolation
- Easier maintenance

---

## 📊 **Monitoring & Observability**

### **Current**
- Vercel Analytics (basic)
- Console logging

### **Planned**
- **Error Tracking**: Sentry
- **Performance Monitoring**: New Relic / Datadog
- **Logging**: CloudWatch / Papertrail
- **Alerting**: PagerDuty
- **Metrics**: Prometheus + Grafana

**Example Metrics**:
```typescript
metrics.track('diagram.generated', {
  type: 'flowchart',
  aiModel: 'perplexity',
  processingTime: 1234,
  success: true
});
```

---

## 🧪 **Testing Strategy**

### **Planned Testing Pyramid**

```
        ┌──────────────┐
        │     E2E      │  5%
        └──────────────┘
       ┌────────────────┐
       │  Integration   │  15%
       └────────────────┘
      ┌──────────────────┐
      │   Unit Tests     │  80%
      └──────────────────┘
```

**Unit Tests**: Jest + React Testing Library
**Integration**: Supertest for API
**E2E**: Playwright / Cypress

---

## 📚 **Additional Resources**

- [Next.js Documentation](https://nextjs.org/docs)
- [Mermaid.js Guide](https://mermaid.js.org/)
- [Tailwind CSS](https://tailwindcss.com/)
- [Radix UI](https://www.radix-ui.com/)
- [Perplexity API](https://docs.perplexity.ai/)

---

**Built with 🔵 on Base • Architected for Scale and Academic Excellence** 🚀
