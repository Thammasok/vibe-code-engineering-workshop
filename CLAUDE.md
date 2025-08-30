# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is the **Logistics CRM (MVP)** - a user-focused web application designed to simplify logistics management for non-technical staff. The project prioritizes simplicity, efficiency, and ease of learning over complex features.

**Core Philosophy**: "Effortless" user experience - everything must be clear and straightforward so that staff unfamiliar with computers can start working immediately without training.

## Architecture & Tech Stack

**Architecture Pattern**: Full-stack Serverless using Supabase + Vercel
- **Frontend**: React 18.x + TypeScript 5.x + Vite 5.x
- **UI Library**: shadcn/ui with Tailwind CSS 3.x
- **State Management**: React Context API (built-in)
- **Backend**: Supabase (PostgreSQL 15.x, Auth, Edge Functions)
- **Testing**: Vitest + React Testing Library
- **Deployment**: Vercel (frontend), Supabase (backend)

**Project Structure** (Monorepo with npm workspaces):
```
/logistics-crm-mvp
├── apps/web/                 # React application
│   ├── src/
│   │   ├── components/       # Reusable UI components
│   │   ├── pages/           # Page-level components
│   │   └── services/        # API and business logic
├── packages/shared/         # Shared types and utilities
│   └── types.ts            # TypeScript interfaces
└── package.json            # Root package with workspaces config
```

## Development Commands

**Setup and Installation**:
```bash
# Install dependencies
npm install

# Setup environment (create .env with Supabase URL + Anon Key)
# See development workflow for details

# Run development server
npm run dev --workspace=web
```

**Key Development Requirements**:
- All data access must use **Supabase Client Library**
- Shared types go in `packages/shared/types.ts`
- Environment variables accessed via `import.meta.env.VITE_*`
- Test files adjacent to source with `.test.tsx` extension

## Core Data Models

```typescript
interface Customer {
  id: string;
  created_at: string;
  name: string;
  email: string;
  phone: string;
}

interface Job {
  id: string;
  created_at: string;
  customer_id: string;
  description: string;
  status: 'New' | 'In Progress' | 'Done';
  customers?: Customer;
}
```

## BMAD Framework Integration

This project uses the **BMAD (Build, Manage, Architect, Deploy) Framework** for development workflow management.

**Key BMAD Components**:
- **Configuration**: `.bmad-core/core-config.yaml` - Project settings and paths
- **Documentation**: `docs/` - Sharded PRD and Architecture documents
- **Stories**: `docs/stories/` - User stories with detailed dev notes
- **Agent System**: `.bmad-core/agents/` - Specialized AI agents for different roles

**Available Agent Commands**:
- `/BMad:agents:po` - Product Owner (story creation, backlog management)
- `/BMad:agents:architect` - System Architect (technical design)
- `/BMad:agents:sm` - Scrum Master (story drafting, process guidance)
- `/BMad:agents:ux-expert` - UX Expert (UI/UX specifications)
- `/BMad:agents:dev` - Developer (implementation)

**Story Workflow**:
1. Stories are created in `docs/stories/` with format `{epic}.{story}.{title}.md`
2. Each story contains comprehensive dev notes with architecture references
3. Stories include acceptance criteria, tasks/subtasks, and testing requirements
4. Dev agents populate completion records in story files

## UI/UX Design Principles

**Core Screens**:
1. Login Screen - Simple email/password authentication
2. Dashboard - Key business metrics and quick actions
3. Customer List/Add Customer - Basic customer management
4. Job List/Add Job/Job Detail - Job tracking and status updates

**Layout Pattern**: Fixed left sidebar navigation + main content area
**Interaction Pattern**: Clear buttons and forms, avoid complex interactions like drag-and-drop
**Accessibility Target**: WCAG AA compliance
**Responsive Strategy**: Desktop-first, responsive web application

## Development Workflow Context

**MVP Focus**: This is an MVP designed to gather feedback quickly. Features are intentionally minimal and focused on core logistics operations.

**Target Users**: 
- Logistics staff (front-line workers)
- Operations managers (supervisors)
- Data entry clerks

**Key User Goals**:
- Reduce repetitive work time
- Minimize errors from complex software
- Enable new staff to learn system independently
- Deliver working MVP quickly for feedback

**Quality Standards**:
- New users complete core tasks within 3 minutes
- Common workflows require maximum 3 clicks from dashboard
- Clear validation and error prevention
- Immediate visual feedback for all actions

## Important File References

- **PRD**: `docs/prd/` (sharded) or `docs/prd.md` (monolithic)
- **Architecture**: `docs/architecture/` (sharded) or `docs/architecture.md` (monolithic)
- **Tech Stack Details**: `docs/architecture/tech-stack.md`
- **Coding Standards**: `docs/architecture/coding-standards.md`
- **Project Structure**: `docs/architecture/unified-project-structure.md`
- **Development Workflow**: `docs/architecture/development-workflow.md`
- **Current Story**: Check `docs/stories/` for latest story to implement

When implementing features, always reference the corresponding story file in `docs/stories/` for detailed technical context, acceptance criteria, and architectural guidance.

# please speak with me only thai lanquage with emoji and easy to read.