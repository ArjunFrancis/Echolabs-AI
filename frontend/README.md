# EchoLabs Frontend - Web Application

> **Purpose:** Modern, responsive web interface for LLM/AI agent evaluation platform

**Status:** ⚠️ Skeleton - Ready for Phase 1 Implementation  
**Last Updated:** December 15, 2025  
**Implementation Phase:** Phase 1 - MVP Launch (Weeks 5-12)  
**Framework:** Next.js 14+ (React 18+, TypeScript)  
**Styling:** Tailwind CSS + shadcn/ui  
**State Management:** Zustand + React Query

---

## Overview

This directory contains the complete frontend implementation for EchoLabs AI platform:
- **Agent Monitoring Dashboard** - Real-time agent performance and metrics
- **Admin Portal** - User/organization/project management
- **Compliance Dashboard** - Regulatory reporting and audit interface
- **Dataset Manager** - Upload, version, and manage test datasets
- **Evaluation Viewer** - Results and analysis interface

**Architecture Pattern:** Server components + client components, API routes, middleware for auth and logging.

---

## Directory Structure (Phase 1)

```
frontend/
│
├── app/                              # Next.js 14 app directory
│   ├── layout.tsx                  # Root layout with metadata
│   ├── page.tsx                    # Homepage/landing
│   ├── error.tsx                   # Error boundary
│   ├── not-found.tsx               # 404 page
│   ├── globals.css                 # Global Tailwind styles
│   │
│   ├── (auth)/                     # Auth route group (shared layout)
│   │   ├── layout.tsx
│   │   ├── login/page.tsx
│   │   ├── signup/page.tsx
│   │   └── forgot-password/page.tsx
│   │
│   ├── (protected)/                # Protected routes (with auth)
│   │   ├── layout.tsx              # Auth check layout
│   │   ├── ├── dashboard/              # Main dashboard
│   │   │   ├── page.tsx             # Dashboard home
│   │   │   ├── agents/              # Agent list/detail
│   │   │   ├── evaluations/         # Evaluations list/detail
│   │   │   ├── datasets/            # Dataset management
│   │   │   ├── compliance/          # Compliance reports
│   │   │   └── settings/            # User settings
│   │   ├── admin/                  # Admin portal
│   │   │   ├── page.tsx             # Admin home
│   │   │   ├── users/               # User management
│   │   │   ├── organizations/       # Org management
│   │   │   ├── usage/               # Usage analytics
│   │   │   └── settings/            # System settings
│   │   └── api/                    # API routes (Optional Edge APIs)
│   │       ├── auth/
│   │       ├── evaluations/
│   │       └── datasets/
│   │
│   ├── providers.tsx               # Context providers (Zustand, React Query)
│   └── middleware.ts               # Next.js middleware (auth check, logging)
│
├── components/                      # React components
│   ├── dashboard/                  # Dashboard-specific components
│   │   ├── agent-status.tsx        # Agent status cards
│   │   ├── performance-chart.tsx   # Performance metrics chart
│   │   ├── error-log-viewer.tsx    # Error log display
│   │   ├── cost-tracker.tsx        # Token/cost tracking
│   │   └── quick-actions.tsx       # Dashboard quick actions
│   ├── admin/                      # Admin-specific components
│   │   ├── user-table.tsx          # User management table
│   │   ├── org-form.tsx            # Organization form
│   │   ├── role-selector.tsx       # Role assignment
│   │   └── audit-log-viewer.tsx    # Audit trail display
│   ├── compliance/                 # Compliance-specific components
│   │   ├── compliance-summary.tsx   # NDMO/DIFC/ADGM status
│   │   ├── report-generator.tsx     # Report generation UI
│   │   └── risk-dashboard.tsx       # Risk assessment display
│   ├── shared/                     # Reusable components
│   │   ├── layout/                 # Layout components
│   │   │   ├── sidebar.tsx
│   │   │   ├── header.tsx
│   │   │   ├── footer.tsx
│   │   │   └── layout-wrapper.tsx
│   │   ├── forms/                  # Form components
│   │   │   ├── login-form.tsx
│   │   │   ├── evaluation-form.tsx
│   │   │   └── dataset-upload.tsx
│   │   ├── tables/                 # Table components
│   │   │   ├── data-table.tsx         # Reusable data table
│   │   │   ├── columns.ts             # Column definitions
│   │   │   └── pagination.tsx
│   │   ├── modals/                 # Modal dialogs
│   │   ├── cards/                  # Card wrappers
│   │   ├── buttons/                # Button variants
│   │   ├── inputs/                 # Input components
│   │   ├── loading/                # Loaders, spinners
│   │   └── errors/                 # Error displays
│   └── icons/                      # Icon components (Lucide)
│
├── lib/                             # Utility functions
│   ├── api.ts                      # API client wrapper
│   ├── auth.ts                     # Authentication utilities
│   ├── validators.ts               # Form validation schemas
│   ├── constants.ts                # App constants
│   ├── formatters.ts               # Data formatting utilities
│   ├── colors.ts                   # Color/theme utilities
│   ├── classnames.ts               # CSS class utilities
│   └── hooks/                      # Custom React hooks
│       ├── useAuth.ts              # Auth state management
│       ├── useFetch.ts             # Data fetching hook
│       ├── useLocalStorage.ts       # Local storage hook
│       ├── useNotification.ts       # Notification toast
│       ├── usePagination.ts         # Pagination hook
│       └── useAsync.ts             # Async operations hook
│
├── store/                          # Zustand state management
│   ├── auth.store.ts               # Auth state (user, token)
│   ├── dashboard.store.ts          # Dashboard state
│   ├── ui.store.ts                 # UI state (modals, sidebar)
│   └── notifications.store.ts       # Notification state
│
├── styles/                         # Global styles and themes
│   ├── globals.css                 # Global Tailwind
│   ├── variables.css               # CSS variables (colors, spacing)
│   ├── tailwind-config.ts          # Tailwind configuration
│   └── theme.ts                    # Theme definitions
│
├── public/                         # Static assets
│   ├── logo.svg                    # EchoLabs logo
│   ├── favicon.ico                 # Favicon
│   ├── og-image.png                # Open Graph image
│   └── icons/                      # Social icons, etc.
│
├── tests/                          # Test suite
│   ├── setup.ts                    # Test configuration
│   ├── __mocks__/                  # Mock data
│   ├── unit/                       # Unit tests
│   │   ├── components.test.tsx
│   │   ├── hooks.test.ts
│   │   └── utils.test.ts
│   └── e2e/                        # End-to-end tests (Playwright)
│       ├── auth.spec.ts            # Login/auth flows
│       ├── dashboard.spec.ts       # Dashboard functionality
│       └── evaluations.spec.ts     # Evaluation workflows
│
├── .env.example                    # Example environment variables
├── .env.local                      # Local environment (git-ignored)
├── next.config.js                  # Next.js configuration
├── tsconfig.json                   # TypeScript configuration
├── package.json                    # Dependencies and scripts
├── package-lock.json               # Dependency lock file
├── tailwind.config.js              # Tailwind CSS configuration
├── postcss.config.js               # PostCSS configuration
├── playwright.config.ts            # Playwright E2E configuration
├── jest.config.js                  # Jest testing configuration
└── README.md                       # This file
```

---

## Tech Stack

### **Framework & Runtime**
- **Next.js 14+** - React framework with App Router
- **React 18+** - UI library
- **TypeScript 5+** - Type safety
- **Node.js 18+** - Runtime

### **Styling & UI**
- **Tailwind CSS 3.3+** - Utility CSS framework
- **shadcn/ui** - High-quality component library
- **Lucide React** - Icon library
- **PostCSS 8+** - CSS processing

### **State Management & Data**
- **Zustand 4+** - Lightweight state management
- **React Query 5+** - Server state management
- **React Hook Form 7+** - Form handling
- **Zod 3+** - Schema validation

### **HTTP & APIs**
- **axios** - HTTP client
- **NextAuth.js 4.24+** - Authentication

### **Real-Time & WebSocket**
- **Socket.IO Client** - Real-time updates (agent status, metrics)
- **Server-Sent Events** - Alternative real-time approach

### **Charts & Visualization**
- **Recharts 2.10+** - Chart library
- **Tremor 3+** - Metric displays

### **Testing**
- **Jest 29+** - Unit testing framework
- **React Testing Library 14+** - Component testing
- **Playwright 1.40+** - E2E testing
- **MSW (Mock Service Worker)** - API mocking

### **Development & Build**
- **ESLint** - Code linting
- **Prettier** - Code formatting
- **Husky** - Git hooks
- **lint-staged** - Run linters on staged files

---

## Getting Started

### **Prerequisites**
- Node.js 18+
- npm 9+ or yarn 3+
- Backend API running (http://localhost:8000)

### **Installation**

```bash
# 1. Install dependencies
npm install

# 2. Set up environment variables
cp .env.example .env.local
# Edit .env.local with your configuration

# 3. Run development server
npm run dev

# 4. Open browser
# http://localhost:3000
```

### **Available Scripts**

```bash
npm run dev          # Start development server (port 3000)
npm run build        # Build for production
npm run start        # Start production server
npm run lint         # Run ESLint
npm run format       # Format code with Prettier
npm run type-check   # TypeScript type checking
npm run test         # Run unit tests (Jest)
npm run test:watch   # Watch mode for tests
npm run test:coverage # Generate coverage report
npm run e2e          # Run E2E tests (Playwright)
npm run e2e:ui       # Run E2E tests with UI
```

---

## Key Features (Phase 1)

### **Agent Monitoring Dashboard**
- Real-time agent status (running, idle, error, paused)
- Performance metrics (latency, success rate, cost)
- Error log viewer with stack traces
- Cost/token usage analytics
- Agent communication flow visualization

### **Admin Portal**
- User management (create, edit, delete)
- Organization/team management
- Role-based access control (RBAC)
- API key management
- Audit log viewer
- System settings and configuration

### **Compliance Dashboard**
- Compliance status (NDMO, DIFC, ADGM)
- Risk assessment scores
- Audit report generation (PDF export)
- Privacy impact analysis
- Data residency verification

### **Dataset Manager**
- File upload interface (drag & drop)
- Dataset versioning and history
- Preview and validation
- Privacy and encryption settings
- Sharing and access control

### **Evaluation Viewer**
- Results display and analysis
- Comparison of multiple evaluations
- Detailed metrics and breakdowns
- Export results (PDF, JSON, CSV)

---

## Component Architecture

### **Server Components (Default)**
- Layouts
- Data fetching pages
- Database queries

### **Client Components (Marked with 'use client')**
- Interactive components
- Forms and inputs
- Charts and visualizations
- Real-time updates

### **Pattern Example**

```typescript
// app/dashboard/page.tsx (Server Component)
export default async function DashboardPage() {
  const data = await fetchDashboardData(); // Server-side fetch
  return <Dashboard initialData={data} />;
}

// components/dashboard/dashboard.tsx (Client Component)
'use client';
export function Dashboard({ initialData }) {
  const [data, setData] = useState(initialData);
  // Interactive logic here
  return <div>...</div>;
}
```

---

## Styling Guidelines

### **Tailwind CSS Best Practices**
- Use design tokens for consistency
- Avoid inline styles
- Use component classes for reusable patterns
- Mobile-first responsive design

### **Color Palette**
- Primary: Blue (brand color)
- Success: Green
- Warning: Orange
- Error: Red
- Neutral: Gray

### **Example Component**

```typescript
export function Button({ children, variant = 'primary' }) {
  const variants = {
    primary: 'bg-blue-600 text-white hover:bg-blue-700',
    secondary: 'bg-gray-200 text-gray-800 hover:bg-gray-300',
    danger: 'bg-red-600 text-white hover:bg-red-700',
  };
  
  return (
    <button className={`px-4 py-2 rounded-lg ${variants[variant]}`}>
      {children}
    </button>
  );
}
```

---

## API Integration

### **API Client Wrapper**

```typescript
// lib/api.ts
const apiClient = axios.create({
  baseURL: process.env.NEXT_PUBLIC_API_URL || 'http://localhost:8000',
  withCredentials: true,
});

// Auto-add auth token
apiClient.interceptors.request.use((config) => {
  const token = getAuthToken();
  if (token) {
    config.headers.Authorization = `Bearer ${token}`;
  }
  return config;
});
```

### **React Query Hook Example**

```typescript
// hooks/useEvaluations.ts
export function useEvaluations() {
  return useQuery({
    queryKey: ['evaluations'],
    queryFn: () => apiClient.get('/api/v1/evaluations'),
  });
}
```

---

## Environment Variables

```bash
# .env.local
NEXT_PUBLIC_API_URL=http://localhost:8000
NEXT_PUBLIC_APP_NAME=EchoLabs
NEXT_PUBLIC_APP_VERSION=1.0.0

NEXTAUTH_URL=http://localhost:3000
NEXTAUTH_SECRET=your-secret-key-here

# Analytics (optional)
NEXT_PUBLIC_ANALYTICS_ID=...
```

---

## Testing Strategy

### **Unit Tests (Jest + React Testing Library)**
- Test individual components
- Test custom hooks
- Test utility functions
- Minimum 70% coverage

### **E2E Tests (Playwright)**
- Login flow
- Dashboard navigation
- Evaluation creation and viewing
- Compliance report generation

### **Run Tests**

```bash
# Unit tests
npm run test

# Unit tests with coverage
npm run test:coverage

# E2E tests
npm run e2e

# E2E tests with UI
npm run e2e:ui
```

---

## Performance Optimization

### **Next.js Best Practices**
- Image optimization (`next/image`)
- Font optimization
- Code splitting and lazy loading
- Route prefetching
- Incremental Static Regeneration (ISR)

### **React Best Practices**
- Memoization for expensive components
- Virtual scrolling for large lists
- Debouncing for search inputs
- Batch state updates

---

## Accessibility (WCAG 2.1)

### **Standards**
- Semantic HTML
- ARIA labels and roles
- Keyboard navigation
- Color contrast (4.5:1 minimum)
- Focus indicators

### **Tools**
- axe DevTools
- Lighthouse
- WAVE browser extension

---

## Related Documentation

**Specifications:**
- [Agent Monitoring UI](../../ui-design/agent-monitoring-ui.md)
- [Admin Portal](../../ui-design/admin-portal.md)
- [Compliance Dashboard](../../ui-design/compliance-dashboard.md)
- [Technical Specifications](../../deliverables/technical-specifications.md)

**Development:**
- [Developer Quickstart](../../DEVELOPER_QUICKSTART.md)
- [Contributing Guidelines](../../CONTRIBUTING.md) (coming soon)

---

**Directory Status:** ⚠️ Skeleton - Ready for Phase 1  
**Implementation Start:** Phase 1, Week 5  
**Last Updated:** December 15, 2025  
**Maintainer:** EchoLabs Frontend Team
