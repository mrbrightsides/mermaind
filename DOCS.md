# 📚 Mermaind Technical Documentation

Complete technical documentation for developers and contributors.

---

## Table of Contents

1. [Architecture Overview](#architecture-overview)
2. [Core Technologies](#core-technologies)
3. [Feature Modules](#feature-modules)
4. [AI Integration](#ai-integration)
5. [Database & State Management](#database--state-management)
6. [API Reference](#api-reference)
7. [Component Library](#component-library)
8. [Development Guide](#development-guide)
9. [Deployment](#deployment)
10. [Troubleshooting](#troubleshooting)

---

## Architecture Overview

### System Architecture

```
┌─────────────────────────────────────────────────────────┐
│                    Client (Browser)                      │
│  ┌──────────────┐  ┌──────────────┐  ┌──────────────┐  │
│  │   Desktop    │  │    Mobile    │  │    Tablet    │  │
│  │  Experience  │  │  Experience  │  │  Experience  │  │
│  └──────────────┘  └──────────────┘  └──────────────┘  │
└─────────────────────────────────────────────────────────┘
                         ↓ HTTP/WebSocket
┌─────────────────────────────────────────────────────────┐
│                 Next.js App Router (SSR)                 │
│  ┌──────────────────────────────────────────────────┐  │
│  │  App Routes          │  API Routes               │  │
│  │  - page.tsx          │  - /api/generate-diagram  │  │
│  │  - layout.tsx        │  - /api/proxy             │  │
│  │                      │  - /api/analyze-context   │  │
│  └──────────────────────────────────────────────────┘  │
└─────────────────────────────────────────────────────────┘
                         ↓
┌─────────────────────────────────────────────────────────┐
│                    Service Layer                         │
│  ┌──────────────┐  ┌──────────────┐  ┌──────────────┐  │
│  │ Diagram Svc  │  │  AI Service  │  │  Export Svc  │  │
│  │ Generation   │  │  Perplexity  │  │  SVG/PDF/etc │  │
│  └──────────────┘  └──────────────┘  └──────────────┘  │
└─────────────────────────────────────────────────────────┘
                         ↓
┌─────────────────────────────────────────────────────────┐
│                  External Services                       │
│  ┌──────────┐  ┌──────────┐  ┌──────────┐  ┌─────────┐│
│  │Perplexity│  │  Zotero  │  │  Notion  │  │Mendeley ││
│  │   API    │  │   API    │  │   API    │  │   API   ││
│  └──────────┘  └──────────┘  └──────────┘  └─────────┘│
└─────────────────────────────────────────────────────────┘
```

### Data Flow

```
User Input → Input Validation → Feature Flags Check → AI Analysis
    ↓
Context Enhancement (Research Tools Integration)
    ↓
Perplexity AI Processing → Structured Data Extraction
    ↓
Mermaid Code Generation → Syntax Validation
    ↓
Diagram Rendering (SVG) → Post-Processing
    ↓
Export Options (PDF/LaTeX/PNG/Citations)
```

---

## Core Technologies

### Frontend Stack

#### **Next.js 15** (App Router)
```typescript
// app/page.tsx - Server Component by default
export default function Page() {
  // Server-side rendering, SEO optimized
  return <ClientComponent />
}

// Client components use 'use client'
'use client'
export function ClientComponent() {
  // Interactive UI with hooks
}
```

**Why Next.js?**
- SSR for SEO and performance
- API routes for backend logic
- File-based routing
- Built-in optimization

#### **TypeScript 5.0** (Strict Mode)
```typescript
// types.ts - Strict type definitions
export interface DiagramType {
  id: DiagramTypeId;
  name: string;
  description: string;
  icon: LucideIcon;
  mermaidType: string;
  academicUse: string[];
}

// No implicit any allowed
const config: Record<string, number> = {
  timeout: 5000
}
```

**Benefits:**
- Zero runtime errors
- Better IDE support
- Self-documenting code
- Refactoring safety

#### **Tailwind CSS 3.0**
```typescript
// Utility-first styling
<div className="bg-gradient-to-r from-blue-500 to-cyan-500 
                text-white p-4 rounded-lg shadow-lg
                hover:shadow-xl transition-all">
```

**Advantages:**
- No CSS file management
- Built-in responsive design
- Purged unused styles
- Consistent design system

#### **Radix UI**
```typescript
// Accessible, unstyled components
import * as Dialog from '@radix-ui/react-dialog'

<Dialog.Root>
  <Dialog.Trigger>Open</Dialog.Trigger>
  <Dialog.Content>
    {/* Fully accessible modal */}
  </Dialog.Content>
</Dialog.Root>
```

**Features:**
- WAI-ARIA compliant
- Keyboard navigation
- Focus management
- Screen reader support

### Backend Services

#### **Perplexity AI**
```typescript
// lib/diagramService.ts
const response = await fetch('/api/proxy', {
  method: 'POST',
  body: JSON.stringify({
    protocol: 'https',
    origin: 'api.perplexity.ai',
    path: '/chat/completions',
    method: 'POST',
    headers: {
      'Authorization': `Bearer ${PERPLEXITY_API_KEY}`,
      'Content-Type': 'application/json'
    },
    body: {
      model: 'llama-3.1-sonar-small-128k-online',
      messages: [/* AI prompt */]
    }
  })
})
```

**Why Perplexity?**
- Latest model architecture
- Fast response times
- Academic understanding
- Reliable fallbacks

#### **Mermaid.js**
```typescript
// Diagram rendering
import mermaid from 'mermaid'

mermaid.initialize({
  theme: 'base',
  themeVariables: {
    primaryColor: '#00d4ff',
    // Custom academic styling
  }
})

const { svg } = await mermaid.render('diagram-id', mermaidCode)
```

---

## Feature Modules

### 1. AI Research Assistant

**Location**: `src/components/ai-research-assistant.tsx`

**Purpose**: Provides intelligent diagram suggestions based on research context

**Key Functions**:
```typescript
interface AIResearchAssistantProps {
  isOpen: boolean;
  onClose: () => void;
  onSelectSuggestion: (prompt: string, type: DiagramTypeId) => void;
}

// Analyzes research context
const analyzeResearch = async (context: string) => {
  const analysis = await fetch('/api/analyze-context', {
    method: 'POST',
    body: JSON.stringify({ context })
  })
  return analysis.json()
}

// Returns 3-5 diagram suggestions
interface DiagramSuggestion {
  type: DiagramTypeId;
  title: string;
  description: string;
  reasoning: string;
  promptTemplate: string;
  estimatedComplexity: 'Low' | 'Medium' | 'High';
}
```

**Usage**:
```typescript
<AIResearchAssistant 
  isOpen={showAIAssistant}
  onClose={() => setShowAIAssistant(false)}
  onSelectSuggestion={(prompt, type) => {
    setPrompt(prompt)
    setSelectedDiagramType(type)
    generateDiagram()
  }}
/>
```

### 2. Research Tool Integration

**Location**: `src/components/research-integration.tsx`

**Supported Platforms**:
- Zotero (API v3)
- Notion (API v1)
- Mendeley (OAuth 2.0)

**Integration Flow**:
```typescript
// 1. Connect to platform
const connectZotero = async (apiKey: string, userId: string) => {
  const response = await fetch(
    `https://api.zotero.org/users/${userId}/items?limit=50`,
    { headers: { 'Zotero-API-Key': apiKey } }
  )
  return response.json()
}

// 2. Extract metadata
interface Reference {
  title: string;
  authors: string[];
  year: number;
  abstract?: string;
  keywords?: string[];
  doi?: string;
}

// 3. Enhance diagram generation
const enhancedContext = {
  userPrompt: originalPrompt,
  researchContext: {
    references: zoteroReferences,
    keywords: extractedKeywords,
    methodology: detectedMethodology
  }
}
```

**API Endpoints**:
```typescript
// Zotero
GET https://api.zotero.org/users/{userId}/items

// Notion
POST https://api.notion.com/v1/databases/{databaseId}/query

// Mendeley
GET https://api.mendeley.com/documents
```

### 3. Team Collaboration

**Location**: `src/components/collaboration-panel.tsx`

**Features**:
- Real-time team member presence
- Comment system with threads
- Share link generation
- Role-based permissions

**Data Structures**:
```typescript
interface TeamMember {
  id: string;
  email: string;
  role: 'owner' | 'editor' | 'viewer';
  addedAt: Date;
  isOnline: boolean;
}

interface Comment {
  id: string;
  author: string;
  content: string;
  timestamp: Date;
  resolved: boolean;
  replies?: Comment[];
}

interface ShareLink {
  id: string;
  url: string;
  permission: 'view' | 'edit';
  expiresAt: Date | null;
  createdAt: Date;
}
```

**Real-time Updates** (Future Enhancement):
```typescript
// WebSocket connection for live collaboration
const ws = new WebSocket('wss://mermaind.app/collaboration')

ws.on('member-joined', (member: TeamMember) => {
  // Update UI
})

ws.on('comment-added', (comment: Comment) => {
  // Show notification
})

ws.on('diagram-updated', (changes: DiagramChanges) => {
  // Apply operational transformation
})
```

### 4. Mobile Experience

**Location**: `src/components/mobile-experience.tsx`

**Responsive Breakpoints**:
```typescript
const breakpoints = {
  mobile: '< 768px',
  tablet: '768px - 1024px',
  desktop: '> 1024px'
}

// Mobile detection
const isMobile = window.innerWidth < 768
```

**Mobile-Specific Features**:

**Bottom Navigation**:
```typescript
<div className="fixed bottom-0 left-0 right-0 z-50 
                bg-background border-t
                md:hidden"> {/* Hidden on desktop */}
  <div className="grid grid-cols-4 gap-1 p-2">
    <Button variant="ghost">Generate</Button>
    <Button variant="ghost">Templates</Button>
    <Button variant="ghost">Export</Button>
    <Button variant="ghost">Share</Button>
  </div>
</div>
```

**Drawer Menu**:
```typescript
<Sheet open={drawerOpen} onOpenChange={setDrawerOpen}>
  <SheetContent side="left" className="w-[300px]">
    {/* Mobile-optimized feature access */}
  </SheetContent>
</Sheet>
```

**Touch Optimizations**:
- Input font size: 16px (prevents zoom on iOS)
- Touch targets: minimum 44x44px
- Swipe gestures: for navigation
- Pull-to-refresh: diagram reload

---

## AI Integration

### Perplexity API Integration

**Model**: `llama-3.1-sonar-small-128k-online`

**Configuration**:
```typescript
const AI_CONFIG = {
  model: 'llama-3.1-sonar-small-128k-online',
  temperature: 0.3, // Lower = more focused
  max_tokens: 2000,
  top_p: 0.9,
  stream: false
}
```

### Prompt Engineering

**System Prompt Structure**:
```typescript
const systemPrompt = `
You are an expert academic diagram generator AI.

Context: ${diagramType} diagram for ${researchField}
Research Context: ${researchReferences}

Task: Generate a detailed, accurate ${diagramType} diagram based on the user's description.

Output Format: Valid Mermaid.js syntax only.
Academic Standards: Follow publication guidelines for ${journalStyle}.
Terminology: Use discipline-specific terms for ${researchField}.

Requirements:
- Clear node labels
- Logical connections
- Academic rigor
- Publication quality
`
```

**User Prompt Enhancement**:
```typescript
const enhancePrompt = (
  userPrompt: string,
  context: ResearchContext
) => {
  return `
${userPrompt}

Additional Context:
- Related References: ${context.references.slice(0, 5).map(r => r.title)}
- Key Concepts: ${context.keywords.join(', ')}
- Research Methodology: ${context.methodology}
- Target Audience: ${context.audience}
  `.trim()
}
```

### Response Parsing

**JSON Extraction**:
```typescript
const extractMermaidCode = (aiResponse: string): string => {
  // Try JSON extraction
  const jsonMatch = aiResponse.match(/```json\n([\s\S]*?)\n```/)
  if (jsonMatch) {
    const parsed = JSON.parse(jsonMatch[1])
    return parsed.mermaidCode || parsed.code
  }
  
  // Try code block extraction
  const codeMatch = aiResponse.match(/```(?:mermaid)?\n([\s\S]*?)\n```/)
  if (codeMatch) {
    return codeMatch[1].trim()
  }
  
  // Return raw response
  return aiResponse.trim()
}
```

### Error Handling & Retries

```typescript
const generateWithRetry = async (
  prompt: string,
  maxRetries: number = 3
): Promise<string> => {
  for (let attempt = 1; attempt <= maxRetries; attempt++) {
    try {
      const result = await generateDiagram(prompt)
      return result
    } catch (error) {
      if (attempt === maxRetries) throw error
      
      // Exponential backoff
      await new Promise(resolve => 
        setTimeout(resolve, Math.pow(2, attempt) * 1000)
      )
    }
  }
  throw new Error('Max retries exceeded')
}
```

---

## Database & State Management

### State Architecture

**Client-Side State** (React Hooks):
```typescript
// Global app state
const [prompt, setPrompt] = useState<string>('')
const [selectedDiagramType, setSelectedDiagramType] = useState<DiagramTypeId>('flowchart')
const [generatedSVG, setGeneratedSVG] = useState<string>('')
const [isGenerating, setIsGenerating] = useState(false)

// Feature states
const [teamMembers, setTeamMembers] = useState<TeamMember[]>([])
const [comments, setComments] = useState<Comment[]>([])
const [versions, setVersions] = useState<DiagramVersion[]>([])
```

**LocalStorage Persistence**:
```typescript
// Save diagram to history
const saveDiagramToHistory = (diagram: GeneratedDiagram) => {
  const history = JSON.parse(
    localStorage.getItem('diagram-history') || '[]'
  )
  history.unshift({
    ...diagram,
    timestamp: Date.now()
  })
  localStorage.setItem(
    'diagram-history',
    JSON.stringify(history.slice(0, 50)) // Keep last 50
  )
}

// Load diagram history
const loadDiagramHistory = (): GeneratedDiagram[] => {
  return JSON.parse(
    localStorage.getItem('diagram-history') || '[]'
  )
}
```

**Future: Database Integration**

```typescript
// Prisma Schema (Future Enhancement)
model User {
  id        String   @id @default(cuid())
  email     String   @unique
  diagrams  Diagram[]
  teams     TeamMember[]
}

model Diagram {
  id          String   @id @default(cuid())
  userId      String
  type        String
  prompt      String
  svgContent  String   @db.Text
  mermaidCode String   @db.Text
  createdAt   DateTime @default(now())
  updatedAt   DateTime @updatedAt
  user        User     @relation(fields: [userId], references: [id])
  versions    DiagramVersion[]
  comments    Comment[]
}
```

---

## API Reference

See [API.md](API.md) for complete API documentation.

**Quick Reference**:

| Endpoint | Method | Purpose |
|----------|--------|---------|
| `/api/generate-diagram` | POST | Generate diagram from prompt |
| `/api/proxy` | POST | Proxy external API calls |
| `/api/analyze-context` | POST | AI context analysis |
| `/api/export` | POST | Export diagram in formats |
| `/api/citations` | POST | Generate academic citations |

---

## Component Library

### Core Components

**Location**: `src/components/ui/*`

All UI components are from Radix UI with custom styling:

```typescript
// Button
import { Button } from '@/components/ui/button'
<Button variant="default | outline | ghost | destructive">

// Dialog
import { Dialog, DialogContent, DialogTitle } from '@/components/ui/dialog'
<Dialog open={isOpen} onOpenChange={setIsOpen}>

// Select
import { Select, SelectContent, SelectItem } from '@/components/ui/select'
<Select value={value} onValueChange={setValue}>

// Textarea
import { Textarea } from '@/components/ui/textarea'
<Textarea placeholder="Enter prompt..." />

// Card
import { Card, CardHeader, CardTitle, CardContent } from '@/components/ui/card'
<Card><CardHeader><CardTitle>Title</CardTitle></CardHeader></Card>
```

### Custom Components

```typescript
// MermaidRenderer - Renders Mermaid diagrams
<MermaidRenderer 
  code={mermaidCode}
  onError={handleError}
/>

// DiagramExplanation - Shows scientific context
<DiagramExplanation 
  type={diagramType}
  visible={showExplanation}
/>

// EnhancedExportManager - Export in multiple formats
<EnhancedExportManager
  svgContent={svg}
  diagramType={type}
  onExport={handleExport}
/>
```

---

## Development Guide

### Setup Development Environment

```bash
# Clone repository
git clone https://github.com/yourusername/mermaind.git
cd mermaind

# Install dependencies
npm install

# Setup environment variables
cp .env.example .env.local

# Run development server
npm run dev

# Run type checking
npm run type-check

# Run linting
npm run lint

# Build for production
npm run build
```

### Code Style Guidelines

**TypeScript**:
- Strict mode enabled
- Explicit types for all parameters
- Interface over type aliases
- Functional components with hooks

**React**:
- Functional components only
- Hooks for state management
- Props destructuring
- Meaningful component names

**File Naming**:
```
components/       → kebab-case.tsx
lib/              → camelCase.ts
types/            → types.ts
utils/            → camelCase.ts
```

### Testing Strategy

```typescript
// Unit tests (Future)
describe('DiagramService', () => {
  it('should generate valid Mermaid code', async () => {
    const result = await generateDiagram('flowchart', 'test prompt')
    expect(result).toContain('graph TD')
  })
})

// Integration tests
describe('AI Integration', () => {
  it('should call Perplexity API correctly', async () => {
    // Test API integration
  })
})

// E2E tests (Playwright)
test('should generate diagram from prompt', async ({ page }) => {
  await page.goto('/')
  await page.fill('[data-testid="prompt-input"]', 'test prompt')
  await page.click('[data-testid="generate-button"]')
  await expect(page.locator('[data-testid="diagram"]')).toBeVisible()
})
```

---

## Deployment

### Vercel (Recommended)

```bash
# Install Vercel CLI
npm i -g vercel

# Login
vercel login

# Deploy
vercel

# Production deployment
vercel --prod
```

**Environment Variables** (Vercel Dashboard):
```
PERPLEXITY_API_KEY=***
ZOTERO_API_KEY=***
NOTION_API_KEY=***
MENDELEY_CLIENT_ID=***
MENDELEY_CLIENT_SECRET=***
```

### Docker Deployment

```dockerfile
FROM node:18-alpine

WORKDIR /app
COPY package*.json ./
RUN npm install
COPY . .
RUN npm run build

EXPOSE 3000
CMD ["npm", "start"]
```

```bash
# Build
docker build -t mermaind .

# Run
docker run -p 3000:3000 mermaind
```

---

## Troubleshooting

### Common Issues

**1. Diagram Not Rendering**
```typescript
// Check Mermaid syntax validity
try {
  await mermaid.parse(mermaidCode)
} catch (error) {
  console.error('Invalid Mermaid syntax:', error)
}
```

**2. AI Generation Fails**
```typescript
// Check API key
if (!process.env.PERPLEXITY_API_KEY) {
  throw new Error('PERPLEXITY_API_KEY not set')
}

// Check rate limits
// Implement exponential backoff
```

**3. Export Issues**
```typescript
// Ensure SVG is valid
const parser = new DOMParser()
const doc = parser.parseFromString(svgContent, 'image/svg+xml')
const errors = doc.getElementsByTagName('parsererror')
if (errors.length > 0) {
  console.error('Invalid SVG')
}
```

**4. Mobile Performance**
```typescript
// Lazy load heavy components
const MobileExperience = dynamic(
  () => import('@/components/mobile-experience'),
  { ssr: false }
)

// Optimize images
<Image 
  src="/logo.png"
  width={100}
  height={100}
  loading="lazy"
/>
```

---

## Performance Optimization

### Bundle Size

```bash
# Analyze bundle
npm run build
npx @next/bundle-analyzer
```

### Code Splitting

```typescript
// Dynamic imports
const HeavyComponent = dynamic(() => import('./HeavyComponent'), {
  loading: () => <Spinner />,
  ssr: false
})
```

### Caching Strategy

```typescript
// Next.js automatic static optimization
export const revalidate = 3600 // 1 hour

// API route caching
export async function GET() {
  return NextResponse.json(data, {
    headers: {
      'Cache-Control': 'public, s-maxage=3600, stale-while-revalidate=86400'
    }
  })
}
```

---

## Security Considerations

### API Key Protection

```typescript
// Never expose API keys to client
// Use Next.js API routes as proxy
export async function POST(request: Request) {
  const apiKey = process.env.PERPLEXITY_API_KEY // Server-side only
  // Make request to external API
}
```

### Input Sanitization

```typescript
// Sanitize user input
const sanitizePrompt = (prompt: string): string => {
  return prompt
    .trim()
    .replace(/<script>/gi, '')
    .slice(0, 5000) // Max length
}
```

### Rate Limiting

```typescript
// Implement rate limiting (Future)
import { Ratelimit } from '@upstash/ratelimit'

const ratelimit = new Ratelimit({
  redis: redis,
  limiter: Ratelimit.slidingWindow(10, '1 m')
})
```

---

## Feature Flags

**Location**: `src/lib/featureFlags.ts`

```typescript
export const FEATURE_FLAGS = {
  enhancedTemplateLibrary: true,
  contextAwareGeneration: true,
  advancedTemplateBuilder: true,
  versionControlSystem: true,
  multiModelAI: true,
  advancedAnalytics: true,
  realTimeCollaboration: false, // Coming soon
  institutionSSO: false // Coming soon
}

// Usage
if (FEATURE_FLAGS.realTimeCollaboration) {
  // Show collaboration features
}
```

---

## Conclusion

This documentation covers the core technical architecture of Mermaind. For specific implementation details, see the source code. For API details, see [API.md](API.md). For contribution guidelines, see [CONTRIBUTING.md](CONTRIBUTING.md).

**Questions?** Open an issue on GitHub or contact the maintainers.

---

**Last Updated**: 2025
**Version**: 1.0.0
**Maintainer**: [@mrbrightsides](https://github.com/mrbrightsides)
