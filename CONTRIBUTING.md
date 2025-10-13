# 🤝 **CONTRIBUTING TO MERMAIND**

Thank you for your interest in contributing to Mermaind! We're excited to collaborate with researchers, developers, and academics worldwide to build the best academic diagram generator.

---

## 📋 **Table of Contents**

- [Code of Conduct](#code-of-conduct)
- [Getting Started](#getting-started)
- [Development Setup](#development-setup)
- [How to Contribute](#how-to-contribute)
- [Coding Guidelines](#coding-guidelines)
- [Commit Messages](#commit-messages)
- [Pull Request Process](#pull-request-process)
- [Testing](#testing)
- [Documentation](#documentation)

---

## 📜 **Code of Conduct**

### **Our Pledge**

We are committed to providing a welcoming and inclusive environment for all contributors, regardless of background, identity, or experience level.

### **Expected Behavior**

- ✅ Be respectful and considerate
- ✅ Welcome newcomers and help them get started
- ✅ Accept constructive criticism gracefully
- ✅ Focus on what's best for the community
- ✅ Show empathy towards other contributors

### **Unacceptable Behavior**

- ❌ Harassment or discrimination of any kind
- ❌ Trolling, insulting, or derogatory comments
- ❌ Personal or political attacks
- ❌ Publishing others' private information
- ❌ Unprofessional conduct

**Reporting**: Contact us at conduct@mermaind.app

---

## 🚀 **Getting Started**

### **Ways to Contribute**

1. **Code Contributions**
   - Bug fixes
   - New features
   - Performance improvements
   - Refactoring

2. **Documentation**
   - Improve existing docs
   - Add examples
   - Write tutorials
   - Fix typos

3. **Design**
   - UI/UX improvements
   - Icons and graphics
   - Accessibility enhancements

4. **Testing**
   - Write test cases
   - Report bugs
   - Test new features

5. **Templates**
   - Create academic templates
   - Improve existing templates
   - Add domain-specific examples

6. **Community**
   - Answer questions
   - Help newcomers
   - Write blog posts
   - Give talks

---

## 💻 **Development Setup**

### **Prerequisites**

- Node.js 18+ 
- npm or yarn
- Git
- Code editor (VS Code recommended)

### **1. Fork & Clone**

```bash
# Fork the repository on GitHub
# Then clone your fork
git clone https://github.com/YOUR_USERNAME/mermaind.git
cd mermaind
```

### **2. Install Dependencies**

```bash
npm install
```

### **3. Set Up Environment**

```bash
# Copy environment template
cp .env.example .env.local

# Add your API keys (optional)
# PERPLEXITY_API_KEY=your_key_here
```

### **4. Run Development Server**

```bash
npm run dev
```

Open [http://localhost:3000](http://localhost:3000)

### **5. Create Feature Branch**

```bash
git checkout -b feature/your-feature-name
```

---

## 🎯 **How to Contribute**

### **Finding Issues to Work On**

1. Check [Issues](https://github.com/mrbrightsides/mermaind/issues)
2. Look for labels:
   - `good-first-issue` - Great for beginners
   - `help-wanted` - We need help!
   - `bug` - Something's broken
   - `enhancement` - New feature ideas
   - `documentation` - Docs improvements

3. Comment on the issue to claim it:
   ```
   I'd like to work on this! ETA: 3 days
   ```

### **Creating New Issues**

**Before creating an issue:**
- Search existing issues to avoid duplicates
- Check if it's already fixed in `main` branch

**Bug Report Template:**
```markdown
**Describe the bug**
Clear description of what's wrong

**To Reproduce**
Steps to reproduce:
1. Go to '...'
2. Click on '...'
3. See error

**Expected behavior**
What should happen

**Screenshots**
If applicable

**Environment**
- Browser: [e.g. Chrome 120]
- OS: [e.g. macOS 14]
- Version: [e.g. 1.0.0]
```

**Feature Request Template:**
```markdown
**Problem Statement**
What problem does this solve?

**Proposed Solution**
How should it work?

**Alternatives Considered**
Other approaches you thought about

**Use Cases**
Who benefits and how?
```

---

## 📝 **Coding Guidelines**

### **TypeScript Style**

```typescript
// ✅ Good: Explicit types
interface DiagramProps {
  prompt: string;
  type: DiagramType;
  onGenerate: (diagram: Diagram) => void;
}

// ❌ Bad: Implicit any
function generateDiagram(prompt, type) {
  // ...
}

// ✅ Good: Use const for immutable values
const MAX_RETRIES = 3;

// ❌ Bad: Use let for everything
let MAX_RETRIES = 3;

// ✅ Good: Destructuring
const { prompt, type } = props;

// ❌ Bad: Accessing multiple times
const prompt = props.prompt;
const type = props.type;
```

### **React Patterns**

```typescript
// ✅ Good: Functional components with hooks
const DiagramGenerator: React.FC<Props> = ({ prompt, type }) => {
  const [loading, setLoading] = useState<boolean>(false);
  
  const handleGenerate = useCallback(() => {
    // ...
  }, [prompt, type]);
  
  return <div>{/* ... */}</div>;
};

// ❌ Bad: Class components (unless necessary)
class DiagramGenerator extends React.Component {
  // ...
}

// ✅ Good: Custom hooks for reusable logic
function useDiagramGenerator(prompt: string, type: DiagramType) {
  const [diagram, setDiagram] = useState<Diagram | null>(null);
  // ...
  return { diagram, generate, loading };
}
```

### **Naming Conventions**

```typescript
// Components: PascalCase
const DiagramRenderer: React.FC = () => { /* ... */ };

// Functions: camelCase
function generateMermaidCode(prompt: string): string { /* ... */ }

// Constants: UPPER_SNAKE_CASE
const MAX_PROMPT_LENGTH = 500;

// Types/Interfaces: PascalCase
interface DiagramData {
  id: string;
  content: string;
}

// Files: kebab-case
// diagram-generator.tsx
// use-diagram-hook.ts
```

### **Code Organization**

```
src/
├── app/              # Next.js app router
├── components/       # React components
│   ├── ui/          # Reusable UI components
│   └── features/    # Feature-specific components
├── lib/             # Utility functions
├── hooks/           # Custom React hooks
├── types/           # TypeScript types
├── data/            # Static data (templates)
└── styles/          # Global styles
```

### **Import Order**

```typescript
// 1. External imports
import React, { useState } from 'react';
import { Button } from '@/components/ui/button';

// 2. Internal imports (types)
import type { DiagramType } from '@/types/diagram';

// 3. Internal imports (components/utils)
import { generateDiagram } from '@/lib/diagramService';
import { DiagramRenderer } from '@/components/diagram-renderer';

// 4. Styles
import './styles.css';
```

---

## 💬 **Commit Messages**

### **Format**

```
<type>(<scope>): <subject>

<body>

<footer>
```

### **Types**

- `feat`: New feature
- `fix`: Bug fix
- `docs`: Documentation changes
- `style`: Code formatting (not visual style)
- `refactor`: Code restructuring
- `test`: Adding tests
- `chore`: Maintenance tasks

### **Examples**

```bash
# Good commit messages
feat(api): add template filtering endpoint
fix(diagram): resolve SVG export rendering issue
docs(readme): update installation instructions
refactor(components): extract diagram logic to hook
test(api): add integration tests for diagram generation

# Bad commit messages
update stuff
fix bug
wip
asdf
```

### **Best Practices**

- Use present tense ("add feature" not "added feature")
- Keep subject line under 50 characters
- Capitalize subject line
- No period at end of subject
- Separate subject and body with blank line
- Explain *what* and *why*, not *how*

---

## 🔄 **Pull Request Process**

### **Before Submitting**

1. **Test your changes**
   ```bash
   npm run dev      # Manual testing
   npm run build    # Production build
   npm run lint     # Check code style
   npm run type-check  # TypeScript validation
   ```

2. **Update documentation**
   - Update README if needed
   - Add JSDoc comments
   - Update CHANGELOG.md

3. **Keep it focused**
   - One feature/fix per PR
   - Small, reviewable changes
   - Clear scope

### **PR Template**

```markdown
## Description
Brief description of changes

## Type of Change
- [ ] Bug fix
- [ ] New feature
- [ ] Breaking change
- [ ] Documentation update

## Related Issues
Closes #123

## Testing
How to test:
1. Step 1
2. Step 2
3. Expected result

## Screenshots
If applicable

## Checklist
- [ ] Code follows style guidelines
- [ ] Self-review completed
- [ ] Comments added where needed
- [ ] Documentation updated
- [ ] No new warnings
- [ ] Tests added/updated
- [ ] Build passes
```

### **Review Process**

1. **Automated Checks**
   - TypeScript compilation
   - Linting
   - Build success
   - (Future: Tests passing)

2. **Code Review**
   - At least 1 approval required
   - Address all comments
   - Keep discussion respectful

3. **Merge**
   - Squash and merge for clean history
   - Delete branch after merge

---

## 🧪 **Testing**

### **Manual Testing**

Before submitting PR:
- Test all affected features
- Try edge cases
- Test on different browsers
- Check mobile responsiveness

### **Future: Automated Tests**

```typescript
// Component tests
describe('DiagramGenerator', () => {
  it('generates flowchart from prompt', async () => {
    const { getByRole, getByText } = render(
      <DiagramGenerator type="flowchart" />
    );
    
    const input = getByRole('textbox');
    fireEvent.change(input, { target: { value: 'Test prompt' } });
    
    const button = getByText('Generate');
    fireEvent.click(button);
    
    await waitFor(() => {
      expect(getByText('Diagram generated')).toBeInTheDocument();
    });
  });
});

// API tests
describe('POST /api/v1/diagram', () => {
  it('returns 200 with valid request', async () => {
    const response = await request(app)
      .post('/api/v1/diagram')
      .set('Authorization', `Bearer ${API_KEY}`)
      .send({ prompt: 'Test', type: 'flowchart' });
    
    expect(response.status).toBe(200);
    expect(response.body.data).toHaveProperty('mermaidCode');
  });
});
```

---

## 📚 **Documentation**

### **Code Documentation**

```typescript
/**
 * Generates a Mermaid diagram from a natural language prompt
 * 
 * @param prompt - Natural language description of the diagram
 * @param type - Type of diagram to generate
 * @param options - Optional generation settings
 * @returns Promise resolving to diagram data
 * 
 * @example
 * ```typescript
 * const diagram = await generateDiagram(
 *   "Show machine learning pipeline",
 *   "flowchart"
 * );
 * ```
 * 
 * @throws {InvalidPromptError} If prompt is too short
 * @throws {GenerationError} If AI generation fails
 */
async function generateDiagram(
  prompt: string,
  type: DiagramType,
  options?: GenerationOptions
): Promise<DiagramData> {
  // Implementation
}
```

### **Component Documentation**

```typescript
/**
 * DiagramRenderer component displays Mermaid diagrams
 * 
 * @component
 * @example
 * ```tsx
 * <DiagramRenderer
 *   code="flowchart TD\n  A --> B"
 *   type="flowchart"
 *   onRenderComplete={(svg) => console.log('Rendered!')}
 * />
 * ```
 */
```

---

## 🏆 **Recognition**

Contributors are recognized in:
- README.md Contributors section
- CHANGELOG.md for significant contributions
- Release notes
- Monthly contributor spotlight (coming soon)

Top contributors may receive:
- Exclusive access to beta features
- Mermaind swag
- Special Discord roles
- Co-author credit on academic papers about Mermaind

---

## 🆘 **Getting Help**

**Stuck? Questions?**

- 💬 [GitHub Discussions](https://github.com/mrbrightsides/mermaind/discussions)
- 🐛 [Issue Tracker](https://github.com/mrbrightsides/mermaind/issues)
- 📧 Email: support@elpeef.com

**Office Hours** (Coming Soon):
- Weekly video call for contributors
- Get help in real-time
- Discuss architecture decisions
- Pair programming sessions

---

## 📜 **License**

By contributing, you agree that your contributions will be licensed under the MIT License.

---

## 🙏 **Thank You!**

Every contribution, no matter how small, makes Mermaind better for researchers worldwide. We appreciate your time and effort!

**Happy Contributing!** 🚀

**Built with 🔵 on Base • Community-Driven Academic Excellence**
