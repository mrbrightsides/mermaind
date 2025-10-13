# 📝 **CHANGELOG**

All notable changes to Mermaind will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

---

## [Unreleased]

### 🚧 In Progress
- Real backend with database (Supabase)
- User authentication system
- Real-time WebSocket collaboration
- Mobile apps (iOS/Android)
- Template marketplace
- Institution SSO

---

## [1.2.0] - 2024-01-15

### 🎉 Added
- **Overleaf Integration**: Complete LaTeX project generation and export
  - Full document classes: article, report, thesis, beamer
  - Quick snippet generation for existing documents
  - Professional figure formatting with positioning controls
  - Comprehensive upload guide and instructions
  - Project management with local storage
  - Live code preview before generation
- **Export System Enhancements**:
  - Multi-format export (SVG, PNG, PDF, LaTeX)
  - High-resolution output (300+ DPI)
  - Publication-ready metadata
  - Project packaging for Overleaf upload

### ✨ Improved
- Enhanced LaTeX code generation with proper package management
- Better error handling for export operations
- Improved UI for Overleaf integration modal
- More comprehensive documentation in upload guide

### 🐛 Fixed
- LaTeX package conflicts in generated documents
- Figure positioning issues in exported LaTeX
- Preview rendering for complex diagrams
- File naming in project packages

---

## [1.1.0] - 2024-01-10

### 🎉 Added
- **Reference Manager Integration**:
  - Zotero RDF export
  - Mendeley BibTeX export
  - EndNote XML export
  - One-click metadata export to all formats
- **Citation Generator**:
  - IEEE format
  - APA format
  - MLA format
  - Chicago format
  - Auto-generated BibTeX entries
- **Real-time Commenting System**:
  - @mention support for collaborators
  - Threaded discussions
  - Reaction system (like, agree, question, important)
  - Resolution tracking
  - Edit and delete capabilities
  - Timestamp display
- **REST API (v1)**:
  - POST /api/v1/diagram - Generate diagrams programmatically
  - GET /api/v1/templates - Access academic templates
  - API key management interface
  - Usage analytics dashboard
  - Rate limiting (100 req/hour)
  - Comprehensive API documentation
- **Version Control System**:
  - Git-like branching
  - Commit history tracking
  - Change comparison
  - Version restoration
- **Analytics Dashboard**:
  - Diagram generation statistics
  - Template usage tracking
  - Performance metrics
  - User activity insights
- **Advanced Template Builder**:
  - Custom template creation
  - Template sharing capabilities
  - Field customization
  - Preview system

### ✨ Improved
- Enhanced AI prompt processing with better context understanding
- Improved export quality for SVG and PNG formats
- Better error messages and user feedback
- Optimized diagram rendering performance
- Enhanced mobile responsiveness

### 🐛 Fixed
- SVG export color inconsistencies
- Citation format edge cases
- API rate limiting calculation errors
- Comment thread ordering issues
- Template search functionality

### 📚 Documentation
- Added comprehensive API.md
- Created CONTRIBUTING.md for open source contributors
- Enhanced README.md with detailed usage guide
- Added code examples for all programming languages

---

## [1.0.0] - 2024-01-01

### 🎉 Initial Release

**Core Features:**
- AI-powered diagram generation using Perplexity
- 200+ academic templates across all disciplines
- 6 diagram types:
  - Flowchart
  - Sequence
  - Class
  - State
  - Gantt
  - Git Graph
- Export to SVG, PNG, PDF
- Light/dark mode with web3 aesthetic
- Real-time diagram preview
- Scientific explanations for each diagram type
- Template suggestion system
- Input validation and error handling

**UI/UX:**
- Clean, modern interface
- Responsive design (mobile, tablet, desktop)
- Radix UI components
- Tailwind CSS styling
- Beautiful gradient backgrounds
- Smooth animations and transitions

**Technical:**
- Next.js 14 with App Router
- TypeScript for type safety
- Edge runtime for API routes
- LocalStorage for offline-first experience
- Mermaid.js for diagram rendering
- html2canvas for PNG export
- jsPDF for PDF export

**Academic Features:**
- Publication-ready output
- Q1 journal compliance
- Scientific diagram explanations
- Academic template categories:
  - Medical/Clinical
  - Engineering
  - Social Sciences
  - Computer Science
  - Business/Management
  - Natural Sciences

---

## [0.3.0] - 2023-12-20 (Beta)

### 🎉 Added
- Context-aware AI generation
- Advanced export options
- Template filtering by category
- Dark mode support

### ✨ Improved
- AI prompt understanding
- Diagram quality
- Export performance
- UI polish

### 🐛 Fixed
- Rendering issues on Safari
- Export filename handling
- Template loading performance

---

## [0.2.0] - 2023-12-10 (Alpha)

### 🎉 Added
- AI integration (Perplexity)
- Basic template system
- Export to SVG/PNG
- Scientific explanations

### ✨ Improved
- Diagram rendering speed
- Error handling
- User feedback

---

## [0.1.0] - 2023-12-01 (Prototype)

### 🎉 Initial Prototype
- Basic Mermaid diagram generation
- Manual syntax input
- Simple preview
- Export to SVG

---

## 📋 **Version Naming Convention**

- **Major (X.0.0)**: Breaking changes, major feature additions
- **Minor (0.X.0)**: New features, backward compatible
- **Patch (0.0.X)**: Bug fixes, minor improvements

---

## 🔮 **Upcoming Releases**

### [1.3.0] - Q2 2024 (Planned)
- Real backend with Supabase
- User authentication (email, OAuth)
- Cross-device sync
- Team workspaces
- Persistent storage

### [1.4.0] - Q2 2024 (Planned)
- Real-time WebSocket collaboration
- Live cursor tracking
- Conflict resolution
- Simultaneous editing

### [2.0.0] - Q3 2024 (Planned)
- Mobile apps (iOS/Android)
- Offline mode
- Native performance
- Push notifications
- Tablet optimization

### [2.1.0] - Q3 2024 (Planned)
- Template marketplace
- Community templates
- Template ratings and reviews
- Revenue sharing for template creators

### [2.2.0] - Q4 2024 (Planned)
- Blockchain verification on Base
- Immutable diagram history
- Proof of authorship
- Smart contract integration

### [3.0.0] - Q4 2024 (Planned)
- Institution SSO
- Enterprise features
- Admin dashboard
- Usage analytics
- GDPR/HIPAA compliance

---

## 🐛 **Known Issues**

### Current
- LocalStorage has 5MB limit (affects large diagrams)
- No cross-device sync yet (planned for 1.3.0)
- Commenting is local-only (real-time planned for 1.4.0)
- Mobile app not available (planned for 2.0.0)

### Workarounds
- Export diagrams regularly to prevent data loss
- Use one device for now
- Coordinate comments via external tools temporarily

---

## 🔗 **Links**

- [GitHub Repository](https://github.com/yourusername/mermaind)
- [Issue Tracker](https://github.com/yourusername/mermaind/issues)
- [Documentation](./README.md)
- [API Docs](./API.md)
- [Contributing Guide](./CONTRIBUTING.md)

---

## 📊 **Release Statistics**

| Version | Release Date | Features | Bug Fixes | Contributors |
|---------|-------------|----------|-----------|--------------|
| 1.2.0   | 2024-01-15  | 8        | 4         | 5            |
| 1.1.0   | 2024-01-10  | 15       | 5         | 8            |
| 1.0.0   | 2024-01-01  | 20+      | -         | 3            |
| 0.3.0   | 2023-12-20  | 4        | 3         | 2            |
| 0.2.0   | 2023-12-10  | 4        | -         | 1            |
| 0.1.0   | 2023-12-01  | 1        | -         | 1            |

---

**Built with 🔵 on Base • Continuously Improving for Academic Excellence** 🚀
