# Next.js Complete Guide

## Table of Contents

- [Introduction](#introduction)
- [What is Next.js?](#what-is-nextjs)
- [Key Features](#key-features)
- [Installation](#installation)
- [Project Structure](#project-structure)
- [Routing](#routing)
- [Data Fetching](#data-fetching)
- [Rendering Methods](#rendering-methods)
- [API Routes](#api-routes)
- [Styling](#styling)
- [Image Optimization](#image-optimization)
- [Middleware](#middleware)
- [Authentication](#authentication)
- [State Management](#state-management)
- [Deployment](#deployment)
- [Best Practices](#best-practices)
- [Security](#security)
- [Performance Optimization](#performance-optimization)
- [Testing](#testing)
- [Common Issues & Solutions](#common-issues--solutions)

## Introduction

Next.js is a powerful React framework that helps developers build full-stack web applications with server-side rendering, static site generation, and many production-ready features out of the box.

### Why Choose Next.js?

**Traditional React Problems:**

- Poor SEO (Search Engine Optimization)
- Slow initial page load
- Manual routing configuration needed
- Separate backend required for server-side logic

**Next.js Solutions:**

- Built-in server-side rendering for better SEO
- Faster page loads and better performance
- Automatic file-based routing system
- Backend functionality built-in through API routes
- Automatic image and font optimization

## What is Next.js?

Next.js is an open-source React framework created by Vercel. It was launched in 2016 and is now one of the most popular React frameworks.

### Core Identity:

**Server-Side Rendering (SSR):**

- Pages are rendered on the server
- Complete HTML is sent to the user
- Excellent for SEO
- Fast initial load

**Static Site Generation (SSG):**

- Pages are generated at build time
- Pre-rendered HTML files are created
- Fastest performance
- Can be hosted on CDN

**Incremental Static Regeneration (ISR):**

- Static pages can be updated after deployment
- Pages regenerate at specified time intervals
- Perfect balance between SSG and SSR

**Hybrid Applications:**

- Different rendering methods can be used for different pages
- Homepage SSG, Dashboard SSR, Blog ISR - all possible together

## Key Features

### 1. App Router (Next.js 13+)

**What it is:**

- New routing system introduced in Next.js 13
- Based on React Server Components
- More powerful and flexible

**Main features:**

- **Layouts**: Share common UI across multiple pages
- **Templates**: Create fresh instances on every navigation
- **Loading UI**: For automatic loading states
- **Error Handling**: Built-in error boundaries
- **Nested Routes**: Support for deep nesting
- **Parallel Routes**: Render multiple pages simultaneously
- **Intercepting Routes**: Intercept and modify routes

### 2. Pages Router (Legacy)

**What it is:**

- Original Next.js routing system
- Still widely used and supported

**Features:**

- File-system based routing
- Files in `pages` folder = routes
- Dynamic routes: `[id].js` creates URLs like `/post/123`
- Catch-all routes: `[...slug].js` handles multiple segments
- API routes: Backend endpoints in `pages/api` folder

### 3. React Server Components

**What it is:**

- New React technology available in Next.js 13+
- Components render on the server
- Only HTML is sent to the client

**Benefits:**

- Reduced JavaScript bundle size
- Faster page loads
- Direct database access in server components
- Automatic code splitting
- Overall better performance

**Server vs Client Components:**

- **Server Components**: Default, no JavaScript to client, database access possible
- **Client Components**: 'use client' directive, for interactivity, can use hooks

### 4. File-Based Routing

**How it works:**

- File structure = URL structure
- No configuration needed
- Intuitive and easy to understand

**In App Router:**

- `app/page.js` → `/` (homepage)
- `app/about/page.js` → `/about`
- `app/blog/[slug]/page.js` → `/blog/any-slug`
- `app/shop/[...categories]/page.js` → `/shop/electronics/phones/samsung`

**In Pages Router:**

- `pages/index.js` → `/`
- `pages/about.js` → `/about`
- `pages/blog/[id].js` → `/blog/123`

### 5. Data Fetching Strategies

**Multiple ways to fetch data:**

**Server Components (App Router):**

- Fetch data directly in async functions
- No useEffect needed
- Cache control options available
- Automatic request deduplication

**getServerSideProps (Pages Router):**

- Runs on every request
- Perfect for real-time data
- Server-side execution
- Data passed as props to component

**getStaticProps (Pages Router):**

- Runs at build time
- Generates static pages
- Fast performance
- Can be made dynamic with ISR

**getStaticPaths (Pages Router):**

- Generates paths for dynamic routes
- Decides which pages to build at build time
- Can create new pages at runtime with fallback modes

**Client-Side Fetching:**

- Using useEffect or libraries (SWR, React Query)
- Best for interactive dashboards
- Loading states must be handled manually

### 6. Built-in Optimizations

**Automatic Code Splitting:**

- Each page loads only its own code
- Unused code is not downloaded
- Faster initial page loads

**Prefetching:**

- Link component automatically prefetches visible links
- Navigation feels instant
- Improved user experience

**Image Optimization:**

- Automatic optimization with next/image component
- Lazy loading by default
- Responsive images
- Converts to modern formats (WebP)
- Blur placeholder support

**Font Optimization:**

- Google Fonts automatically optimized
- No FOUT (Flash of Unstyled Text)
- Self-hosted fonts also optimized

**Script Optimization:**

- Optimized loading of third-party scripts
- Define strategy (beforeInteractive, afterInteractive, lazyOnload)

## Installation

### Requirements

**System Requirements:**

- Node.js 18.17 or newer version
- macOS, Windows, or Linux operating system
- Package manager: npm, yarn, pnpm, or bun

**Pre-requisite Knowledge:**

- React basics (components, props, state, hooks)
- JavaScript/TypeScript fundamentals
- HTML and CSS knowledge
- Basic terminal/command line commands

### Create Next.js App

**Automatic Setup (Recommended):**
Use the `create-next-app` tool which automatically sets up everything.

**Commands:**

- NPX: `npx create-next-app@latest my-project-name`
- Yarn: `yarn create next-app my-project-name`
- PNPM: `pnpm create next-app my-project-name`
- Bun: `bunx create-next-app my-project-name`

**Questions asked during setup:**

1. **TypeScript:** Do you want type safety with JavaScript?

   - Yes: TypeScript files (.tsx, .ts) will be created
   - No: Regular JavaScript files (.jsx, .js) will be created

2. **ESLint:** Do you want a code quality checking tool?

   - Yes: Automatically catches code errors
   - No: Manual checking required

3. **Tailwind CSS:** Do you want utility-first CSS framework?

   - Yes: Tailwind will be automatically configured
   - No: Use custom CSS solution

4. **src/ directory:** Do you want to keep code in src folder?

   - Yes: app/pages folders will be inside src
   - No: Will be at root level

5. **App Router:** Do you want to use the new App Router?

   - Yes: Modern app directory structure (Recommended)
   - No: Traditional pages directory structure

6. **Import alias:** Custom path for module imports?
   - Default: @/\* (e.g., import Button from '@/components/Button')
   - Customize: Set your preferred alias

### Manual Installation

**Step-by-step manual setup:**

**Step 1 - Install Dependencies:**

- Core packages: next, react, react-dom
- Command: `npm install next@latest react@latest react-dom@latest`

**Step 2 - Package.json Scripts:**

- `"dev"`: To start development server
- `"build"`: To create production build
- `"start"`: To run production server
- `"lint"`: To run ESLint

**Step 3 - Create Folder Structure:**

- App Router: Create `app` folder
- Pages Router: Create `pages` folder
- Create `public` folder for public assets

**Step 4 - First Page:**

- Create `app/page.js` or `pages/index.js`
- Export a simple React component

## Project Structure

### App Router Structure (Next.js 13+)

**Folder Organization:**

**Root Level:**

- `app/` - Application code and routes
- `public/` - Static assets (images, fonts)
- `components/` - Reusable React components
- `lib/` - Utility functions and helpers
- `styles/` - Global styles
- `next.config.js` - Next.js configuration
- `package.json` - Dependencies and scripts

**App Directory:**

- `layout.js` - Root layout component (wraps all pages)
- `page.js` - Home page component
- `loading.js` - Loading UI component
- `error.js` - Error UI component
- `not-found.js` - 404 page component
- `template.js` - Template for new instances on navigation
- `route.js` - API endpoint handlers

**Special Files in App Router:**

- `layout.js` - Shared UI for a segment and its children
- `page.js` - Unique UI of a route, makes route publicly accessible
- `loading.js` - Loading UI for a segment and its children
- `error.js` - Error UI for a segment and its children
- `global-error.js` - Global error UI
- `route.js` - Server-side API endpoint
- `template.js` - Specialized re-rendered layout UI
- `default.js` - Fallback UI for parallel routes

**Nested Routes:**

- Create folders for URL segments
- Each folder can have its own page.js, layout.js, etc.
- Example: `app/blog/[slug]/page.js` for `/blog/post-title`

**Route Groups:**

- Use parentheses for organization without affecting URL
- Example: `app/(marketing)/about/page.js` → URL: `/about`
- Useful for organizing related routes

**Parallel Routes:**

- Use @ symbol for parallel rendering
- Example: `app/@modal/page.js`
- Render multiple pages in same layout simultaneously

### Pages Router Structure

**Folder Organization:**

**Root Level:**

- `pages/` - All route files
- `public/` - Static files
- `styles/` - CSS files
- `components/` - React components
- `lib/` - Utilities
- `next.config.js` - Configuration

**Pages Directory:**

- `index.js` - Home page (/)
- `about.js` - About page (/about)
- `[id].js` - Dynamic route (/post/123)
- `[...slug].js` - Catch-all route
- `_app.js` - Custom App component (wraps all pages)
- `_document.js` - Custom Document (modifies HTML structure)
- `404.js` - Custom 404 page
- `500.js` - Custom 500 error page

**API Routes:**

- `pages/api/` - Backend API endpoints
- Files in this folder create API routes
- Example: `pages/api/users.js` → `/api/users`

**Special Pages Files:**

- `_app.js` - Initializes pages, wraps every page
- `_document.js` - Augments HTML and body tags
- `_error.js` - Custom error page
- `404.js` - Custom 404 page
- `500.js` - Custom 500 error page

## Routing

### App Router Routing System

**File Conventions:**

- Every folder represents a URL segment
- `page.js` makes the route publicly accessible
- Nested folders create nested routes

**Route Types:**

**Static Routes:**

- Simple folder with page.js
- Example: `app/about/page.js` → `/about`

**Dynamic Routes:**

- Use square brackets in folder name
- Example: `app/blog/[slug]/page.js` → `/blog/anything`
- Access parameter: `params.slug`

**Catch-All Routes:**

- Use [...folder] for multiple segments
- Example: `app/shop/[...categories]/page.js`
- Matches `/shop/a`, `/shop/a/b`, `/shop/a/b/c`
- Access: `params.categories` (array)

**Optional Catch-All:**

- Use [[...folder]] for optional segments
- Matches parent route too
- Example: `app/docs/[[...slug]]/page.js`
- Matches `/docs`, `/docs/a`, `/docs/a/b`

**Route Groups:**

- Parentheses create groups without affecting URL
- Example: `app/(auth)/login/page.js` → `/login`
- Useful for organizing code and layouts

**Parallel Routes:**

- @ symbol for parallel rendering
- Example: `app/@modal/page.js`
- Render multiple sections simultaneously

**Intercepting Routes:**

- (..) notation to intercept routes
- Show modal on click, full page on refresh
- Example: `app/feed/(..)photo/[id]/page.js`

### Pages Router Routing System

**File Conventions:**

- Every file in pages/ is a route
- File name = URL path
- index.js = root of directory

**Route Types:**

**Static Routes:**

- Simple files
- Example: `pages/about.js` → `/about`

**Dynamic Routes:**

- Square brackets in filename
- Example: `pages/blog/[id].js` → `/blog/123`
- Access: `router.query.id`

**Catch-All Routes:**

- [...param].js for multiple segments
- Example: `pages/docs/[...slug].js`
- Matches `/docs/a/b/c`
- Access: `router.query.slug` (array)

**Optional Catch-All:**

- [[...param]].js includes parent
- Matches parent route too

**Nested Routes:**

- Create folders for nesting
- Example: `pages/blog/post/[id].js` → `/blog/post/123`

### Navigation Between Pages

**Link Component:**

- Declarative navigation
- Automatic prefetching
- Client-side transitions
- No full page reload

**useRouter Hook:**

- Programmatic navigation
- Access route information
- Push, replace, back, forward methods

**Navigation Methods:**

- `router.push('/path')` - Navigate and add to history
- `router.replace('/path')` - Navigate without adding to history
- `router.back()` - Go back in history
- `router.reload()` - Reload current page
- `router.prefetch('/path')` - Manually prefetch page

**Route Parameters:**

- Access dynamic segments
- Query parameters
- Hash fragments

## Data Fetching

### App Router Data Fetching

**Server Components (Default):**

- Async components
- Fetch data directly
- No useEffect needed
- Automatic caching

**Fetch Options:**

- `cache: 'force-cache'` - Cache indefinitely (SSG)
- `cache: 'no-store'` - Fetch fresh every time (SSR)
- `next: { revalidate: 60 }` - Revalidate after 60 seconds (ISR)

**Data Fetching Patterns:**

- Parallel fetching - Multiple requests simultaneously
- Sequential fetching - Wait for one before starting next
- Blocking rendering - Wait for data before rendering
- Streaming - Send data as it becomes available

**Request Deduplication:**

- Automatic deduplication of identical requests
- Requests made in same render pass are cached
- No manual deduplication needed

**Client Components:**

- Use 'use client' directive
- useEffect for data fetching
- Or use libraries like SWR, React Query

### Pages Router Data Fetching

**getServerSideProps (SSR):**

- Runs on every request
- Server-side only
- Access to request and response objects
- Good for real-time, personalized data
- SEO friendly

**When to use:**

- Data changes frequently
- User-specific content
- Need request context

**getStaticProps (SSG):**

- Runs at build time
- Generates static HTML
- Fastest performance
- Can use ISR with revalidate

**When to use:**

- Data doesn't change often
- Content can be pre-rendered
- Same for all users

**getStaticPaths:**

- Required for dynamic routes with getStaticProps
- Defines which paths to pre-render
- Fallback options: false, true, 'blocking'

**Fallback Modes:**

- `false` - Only pre-rendered paths, 404 for others
- `true` - Show fallback UI while generating new pages
- `'blocking'` - Wait for page generation, no fallback UI

**Client-Side Fetching:**

- useEffect hook
- SWR library (recommended by Next.js)
- React Query
- Good for dashboards and user-specific data

**ISR (Incremental Static Regeneration):**

- Add revalidate property to getStaticProps
- Pages regenerate in background
- Stale-while-revalidate pattern
- Best of both worlds (static + dynamic)

### Data Fetching Best Practices

**Choose Right Method:**

- SSG for static content
- ISR for mostly static with updates
- SSR for real-time/personalized
- Client-side for interactive dashboards

**Performance Tips:**

- Fetch data as close to where it's needed
- Use parallel fetching when possible
- Implement proper loading states
- Cache API responses

**Error Handling:**

- Always handle fetch errors
- Provide fallback UI
- Log errors for debugging
- Use error boundaries

## Rendering Methods

### 1. Server-Side Rendering (SSR)

**What it is:**

- Pages rendered on server for each request
- Fresh HTML sent to client
- Server processes React components

**Characteristics:**

- Dynamic content
- User-specific data
- Real-time information
- SEO friendly
- Slower than static generation

**When to use:**

- Personalized dashboards
- User-specific content
- Frequently changing data
- Need request headers/cookies

**How it works:**

- User requests page
- Server fetches data
- Server renders React to HTML
- HTML sent to client
- React hydrates on client

### 2. Static Site Generation (SSG)

**What it is:**

- Pages generated at build time
- Pre-rendered HTML files
- Same content for all users

**Characteristics:**

- Fastest performance
- Cached on CDN
- No server computation per request
- SEO excellent

**When to use:**

- Marketing pages
- Blog posts
- Documentation
- Product pages (mostly static)
- Landing pages

**How it works:**

- Build process runs
- Data fetched at build time
- HTML generated for all pages
- Static files deployed
- CDN serves files instantly

### 3. Incremental Static Regeneration (ISR)

**What it is:**

- Static pages with periodic updates
- Regeneration after specified time
- Stale-while-revalidate pattern

**Characteristics:**

- Fast like SSG
- Fresh data like SSR
- Automatic background regeneration
- No rebuild needed for updates

**When to use:**

- E-commerce product pages
- News articles
- Blog with updates
- Data changes but not constantly

**How it works:**

- Page served from cache
- If stale, served anyway
- Background regeneration triggered
- Next request gets fresh version

**Revalidation Strategies:**

- Time-based: Regenerate after X seconds
- On-demand: Trigger regeneration via API
- Tag-based: Invalidate by tags

### 4. Client-Side Rendering (CSR)

**What it is:**

- Rendering happens in browser
- JavaScript downloads and executes
- Fetch data on client

**Characteristics:**

- Interactive experiences
- No SEO for dynamic parts
- Slower initial load
- Rich interactivity

**When to use:**

- Private dashboards
- Admin panels
- Interactive tools
- Real-time updates

**How it works:**

- HTML shell loaded
- JavaScript downloads
- React app bootstraps
- Data fetched and rendered
- Full interactivity available

### Hybrid Rendering

**Mix and Match:**

- Different methods for different pages
- Homepage: SSG
- Blog posts: ISR
- Dashboard: SSR
- Admin panel: CSR

**Benefits:**

- Optimize each page appropriately
- Best performance where needed
- Flexibility in architecture

## API Routes

### App Router API Routes

**Location:**

- `app/api/` directory
- Use `route.js` or `route.ts` files
- Export named functions for HTTP methods

**HTTP Methods:**

- GET - Retrieve data
- POST - Create data
- PUT/PATCH - Update data
- DELETE - Remove data
- OPTIONS - CORS preflight
- HEAD - Headers only

**Request Object:**

- URL parameters
- Query parameters
- Request body
- Headers
- Cookies

**Response Methods:**

- NextResponse.json() - Send JSON
- NextResponse.redirect() - Redirect
- NextResponse.rewrite() - Rewrite
- Set headers
- Set cookies

**Dynamic Routes:**

- Use [param] in folder name
- Access via params object
- Can have multiple segments

**Route Handlers:**

- Server-side only
- Can access databases
- Authentication logic
- Third-party API calls

### Pages Router API Routes

**Location:**

- `pages/api/` directory
- Each file is an endpoint
- Export default handler function

**Handler Function:**

- Receives req and res objects
- Check req.method for HTTP verb
- Send response with res.status().json()

**Request Object:**

- req.method - HTTP method
- req.query - Query parameters
- req.body - Request body
- req.cookies - Cookies
- req.headers - Request headers

**Response Object:**

- res.status(code) - Set status code
- res.json(data) - Send JSON
- res.send(data) - Send response
- res.redirect(url) - Redirect
- res.setHeader(name, value) - Set header

**Dynamic API Routes:**

- Use [param].js in filename
- Access via req.query.param
- Catch-all routes with [...param].js

### API Route Best Practices

**Security:**

- Validate all inputs
- Authenticate requests
- Rate limiting
- CORS configuration
- Sanitize data

**Performance:**

- Cache responses when possible
- Optimize database queries
- Use connection pooling
- Implement pagination

**Error Handling:**

- Try-catch blocks
- Meaningful error messages
- Appropriate status codes
- Log errors

**Structure:**

- Keep routes focused
- Separate business logic
- Use middleware
- Modular design

## Styling

### 1. CSS Modules

**What it is:**

- Scoped CSS files
- Automatic class name generation
- No global conflicts

**Benefits:**

- Component-level styles
- No naming conflicts
- Type-safe with TypeScript
- Dead code elimination

**File Convention:**

- [name].module.css
- Import as object
- Access classes as properties

**Features:**

- Local scope by default
- :global() for global styles
- Composition with composes
- Works with Sass/SCSS

### 2. Global CSS

**What it is:**

- Styles applied to entire application
- Traditional CSS approach

**Where to import:**

- App Router: layout.js (root)
- Pages Router: \_app.js

**Use cases:**

- Reset/normalize styles
- Font declarations
- Global variables
- Base styles

**Best Practices:**

- Minimal global styles
- Use CSS variables
- Organized structure
- Avoid specificity wars

### 3. Tailwind CSS

**What it is:**

- Utility-first CSS framework
- Pre-defined utility classes
- No custom CSS needed

**Benefits:**

- Rapid development
- Consistent design system
- Smaller bundle size
- No naming decisions

**Configuration:**

- tailwind.config.js
- Define colors, spacing, etc.
- Custom utilities
- Plugins

**Usage:**

- Apply classes directly in JSX
- Responsive modifiers (sm:, md:, lg:)
- State modifiers (hover:, focus:)
- Dark mode support

### 4. CSS-in-JS

**Popular Libraries:**

- styled-components
- Emotion
- styled-jsx (built-in)

**Benefits:**

- Dynamic styling
- Component-scoped
- JavaScript variables in styles
- TypeScript support

**Considerations:**

- Runtime overhead
- Requires 'use client' in App Router
- Setup needed for SSR

### 5. Sass/SCSS

**What it is:**

- CSS preprocessor
- Variables, nesting, mixins

**Setup:**

- Install sass package
- Use .scss or .sass files
- Can use with CSS Modules

**Features:**

- Variables
- Nesting
- Mixins and functions
- Partials and imports

### Styling Best Practices

**Choose Based on Project:**

- Small projects: CSS Modules
- Design system: Tailwind
- Complex styling: CSS-in-JS
- Existing codebase: Match current approach

**Performance:**

- Minimize CSS bundle size
- Use critical CSS
- Optimize load order
- Purge unused styles

**Organization:**

- Consistent naming
- Modular structure
- Reusable styles
- Clear hierarchy

## Image Optimization

### Next.js Image Component

**What it provides:**

- Automatic optimization
- Lazy loading
- Responsive images
- Modern formats (WebP, AVIF)
- Blur placeholders
- Priority loading

**Image Component Features:**

**Automatic Size Optimization:**

- Serves appropriately sized images
- Multiple sizes for different viewports
- Automatic format selection

**Lazy Loading:**

- Images load as they enter viewport
- Reduces initial page load
- Better performance

**Placeholder Options:**

- Blur - Blurred version while loading
- Empty - No placeholder
- Custom - Provide custom image

**Priority Loading:**

- Load important images immediately
- Skip lazy loading
- For above-fold content

### Image Sizing

**Fixed Size:**

- Provide width and height
- Known dimensions
- No layout shift

**Responsive:**

- Fill container
- Use sizes prop
- Adapt to viewport

**Fill Mode:**

- Fill parent container
- Use with position: relative parent
- objectFit for scaling

### Remote Images

**Configuration Required:**

- Define allowed domains
- In next.config.js
- Security measure
- Pattern matching

**Remote Pattern Options:**

- Protocol
- Hostname
- Port
- Pathname

### Image Formats

**Supported Formats:**

- JPEG
- PNG
- WebP (automatic)
- AVIF (if supported)
- GIF
- SVG

**Format Priority:**

- Browser support detected
- Best format served automatically
- Fallback for older browsers

### Image Loading Strategies

**Lazy (Default):**

- Load when near viewport
- Most images should use this
- Better initial performance

**Eager:**

- Load immediately
- All images loaded upfront
- Rare use case

**Priority:**

- Load before other resources
- For hero images
- Above-the-fold content

### Optimization Best Practices

**Size Appropriately:**

- Don't serve oversized images
- Use correct dimensions
- Responsive sizes

**Use Modern Formats:**

- WebP for photos
- SVG for icons/logos
- PNG for transparency

**Optimize Source:**

- Compress before upload
- Remove metadata
- Appropriate quality

**Loading Strategy:**

- Priority for critical images
- Lazy for below fold
- Preload if known needed

## Middleware

### What is Middleware?

**Definition:**

- Code that runs before request completes
- Between request and response
- Server-side only

**Use Cases:**

- Authentication checks
- Redirects
- Rewrites
- Setting headers
- Cookies manipulation
- Bot protection
- A/B testing

### How Middleware Works

**Execution Flow:**

- Request comes in
- Middleware runs
- Can modify request/response
- Continue to page or API
- Or redirect/rewrite

**Middleware File:**

- Create middleware.js or middleware.ts
- At root or in src/ directory
- Export middleware function
- Export config for matching

### Middleware Capabilities

**Request Modification:**

- Read/write headers
- Read/write cookies
- Access request URL
- Check request method

**Response Actions:**

- Continue to next
- Redirect to different URL
- Rewrite to different route
- Send custom response

**Limitations:**

- Cannot access response body
- Cannot use Node.js APIs
- Edge runtime only
- Limited to certain APIs

### Middleware Configuration

**Matcher Config:**

- Specify which routes to match
- Glob patterns supported
- Include/exclude paths
- Regular expressions

**Conditional Execution:**

- Check pathname
- Check headers
- Check cookies
- Environment variables

### Authentication with Middleware

**Common Pattern:**

- Check for auth token
- Verify token validity
- Redirect to login if missing
- Add user info to request

**Protected Routes:**

- Match protected paths
- Check authentication
- Allow or deny access

### Middleware Best Practices

**Performance:**

- Keep lightweight
- Minimal processing
- Fast execution critical
- Avoid heavy operations

**Security:**

- Validate tokens
- Check permissions
- Rate limiting
- XSS protection

**Testing:**

- Test all paths
- Edge cases
- Different scenarios
- Performance testing

## Authentication

### Authentication Strategies

**Session-Based:**

- Server stores session
- Session ID in cookie
- Traditional approach

**Token-Based (JWT):**

- Stateless tokens
- Client stores token
- Modern approach
- Scalable

**OAuth/Social Login:**

- Third-party authentication
- Google, Facebook, GitHub
- User doesn't manage password

### Implementing Authentication

**Popular Libraries:**

- NextAuth.js (most popular)
- Auth0
- Clerk
- Supabase Auth
- Firebase Auth

**NextAuth.js Features:**

- Multiple providers
- Session management
- JWT support
- Database adapters
- Callbacks and events

**Authentication Flow:**

1. User submits credentials
2. Verify against database
3. Generate token/session
4. Store in cookie/localStorage
5. Include in subsequent requests
6. Verify on protected routes

### Protected Routes

**Client-Side:**

- Check auth state
- Redirect if not authenticated
- Loading states

**Server-Side:**

- Middleware checks
- getServerSideProps verification
- API route protection

**App Router:**

- Middleware for protection
- Server components check auth
- Redirect in layout

### Session Management

**Storage Options:**

- HTTP-only cookies (most secure)
- localStorage (XSS vulnerable)
- sessionStorage (tab-scoped)

**Session Duration:**

- Set expiration time
- Refresh mechanism
- Sliding expiration
- Remember me option

**Security Considerations:**

- HTTPS only
- Secure cookie flags
- CSRF protection
- XSS prevention

### Authorization

**Role-Based Access:**

- Assign roles to users
- Check role on protected resources
- Hierarchical roles

**Permission-Based:**

- Granular permissions
- Check specific permissions
- More flexible than roles

**Route Protection:**

- Public routes
- Authenticated routes
- Role-specific routes
- Permission-specific routes

## State Management

### Client State

**React Hooks:**

- useState for local state
- useReducer for complex state
- useContext for shared state
- Custom hooks for reusable logic

**When to Use:**

- Component-specific state
- UI state
- Form state
- Temporary data

### Global State

**Context API:**

- Built-in React solution
- Good for simple global state
- No external dependencies

**Popular Libraries:**

- Redux Toolkit
- Zustand
- Jotai
- Recoil
- MobX

**Choosing Library:**

- Redux: Large apps, devtools, middleware
- Zustand: Minimal, simple API
- Jotai: Atomic state, flexible
- Recoil: Atomic, React-like API

### Server State

**What is Server State:**

- Data from backend
- Cached locally
- Needs synchronization
- Can become stale

**Popular Libraries:**

- TanStack Query (React Query)
- SWR (by Vercel)
- Apollo Client (GraphQL)

**Features Needed:**

- Caching
- Automatic refetching
- Optimistic updates
- Pagination
- Infinite scroll

### State Management Best Practices

**Keep State Local:**

- Don't lift unnecessarily
- Component-scoped when possible
- Lift only when shared

**Separate Concerns:**

- UI state vs server state
- Different tools for different needs
- Don't mix approaches

**Performance:**

- Minimize re-renders
- Use selectors
- Memoization
- Code splitting

## Deployment

### Vercel (Recommended)

**Why Vercel:**

- Made by Next.js creators
- Zero configuration
- Automatic deployments
- Edge network
- Preview deployments
- Analytics included

**Deployment Steps:**

1. Push code to Git
2. Connect repository to Vercel
3. Automatic deployment on push
4. Preview for each branch
5. Production on main branch

**Features:**

- Automatic HTTPS
- Custom domains
- Environment variables
- Edge functions
- Analytics
- Monitoring

### Self-Hosting

**Requirements:**

- Node.js server
- Build output
- Environment variables
- Process manager (PM2)

**Build Process:**

- Run npm run build
- Generates .next directory
- Static assets in public
- Server bundle created

**Deployment Steps:**

1. Build application
2. Copy files to server
3. Install dependencies
4. Set environment variables
5. Start server
6. Configure reverse proxy

### Docker Deployment

**Benefits:**

- Consistent environment
- Easy scaling
- Portable
- Version control

**Dockerfile Setup:**

- Base image (Node)
- Copy files
- Install dependencies
- Build application
- Start server

**Container Orchestration:**

- Docker Compose
- Kubernetes
- Docker Swarm

### Static Export

**When to Use:**

- Fully static sites
- No server-side features
- Host on CDN
- Simple deployment

**Limitations:**

- No API routes
- No ISR
- No SSR
- No dynamic routes (without getStaticPaths)

**Export Process:**

- Configure output: 'export'
- Run npm run build
- Gets static files in out/
- Deploy to any static host

### Platform Options

**Static Hosting:**

- Netlify
- GitHub Pages
- AWS S3 + CloudFront
- Azure Static Web Apps

**Full Hosting:**

- AWS (EC2, ECS)
- Google Cloud
- Azure
- DigitalOcean

**Serverless:**

- Vercel
- AWS Lambda
- Google Cloud Functions

### Deployment Best Practices

**Environment Variables:**

- Different values per environment
- Never commit secrets
- Use .env.local for local
- Configure in hosting platform

**Testing:**

- Test in staging first
- Smoke tests after deployment
- Monitor for errors
- Rollback plan

**Performance:**

- Enable compression
- Configure caching
- Use CDN
- Monitor metrics

## Best Practices

### Project Organization

**Folder Structure:**

- Consistent naming
- Logical grouping
- Clear separation of concerns
- Scalable architecture

**Component Organization:**

- Atomic design principles
- Reusable components
- Single responsibility
- Clear interfaces

**Code Organization:**

- Feature-based structure
- Shared utilities
- Clear dependencies
- Easy to navigate

### Performance

**Code Splitting:**

- Dynamic imports
- Route-based splitting
- Component-based splitting
- Lazy load heavy components

**Image Optimization:**

- Use Next.js Image
- Appropriate formats
- Lazy loading
- Responsive images

**Font Optimization:**

- Use next/font
- Preload critical fonts
- Subset fonts
- Limit font variants

**Bundle Optimization:**

- Analyze bundle size
- Remove unused dependencies
- Tree shaking
- Code splitting

### SEO

**Metadata:**

- Title and description
- Open Graph tags
- Twitter cards
- Canonical URLs

**Structured Data:**

- JSON-LD
- Schema.org markup
- Rich snippets

**Performance:**

- Fast page loads
- Core Web Vitals
- Mobile-friendly
- Accessible

### Accessibility

**Semantic HTML:**

- Proper heading hierarchy
- Meaningful elements
- ARIA labels when needed

**Keyboard Navigation:**

- Focusable elements
- Logical tab order
- Visible focus indicators

**Screen Readers:**

- Alt text for images
- Descriptive links
- Form labels
- ARIA attributes

### Security

**Input Validation:**

- Validate all user input
- Sanitize data
- Prevent injection attacks

**Authentication:**

- Secure token storage
- HTTPS only
- CSRF protection
- Rate limiting

**API Security:**

- Authentication required
- Input validation
- Rate limiting
- Error handling

### Code Quality

**TypeScript:**

- Type safety
- Better IDE support
- Catch errors early
- Documentation

**Linting:**

- ESLint configuration
- Consistent code style
- Catch common errors
- Pre-commit hooks

**Testing:**

- Unit tests
- Integration tests
- E2E tests
- Test coverage

## Security

### Common Vulnerabilities

**XSS (Cross-Site Scripting):**

- Injection of malicious scripts
- Sanitize user input
- Use React's built-in escaping
- Content Security Policy

**CSRF (Cross-Site Request Forgery):**

- Unwanted actions on behalf of user
- Use CSRF tokens
- SameSite cookie attribute
- Verify origin headers

**SQL Injection:**

- Malicious database queries
- Use parameterized queries
- ORM/query builders
- Input validation

**Authentication Bypass:**

- Weak authentication
- Session fixation
- Token theft

### Security Best Practices

**HTTPS:**

- Always use HTTPS
- Redirect HTTP to HTTPS
- HSTS headers
- Secure cookies

**Environment Variables:**

- Never commit secrets
- Use .env.local
- Different per environment
- Rotate regularly

**Dependencies:**

- Keep updated
- Audit regularly
- Remove unused
- Check vulnerabilities

**Headers:**

- X-Frame-Options
- X-Content-Type-Options
- Referrer-Policy
- Permissions-Policy

**Rate Limiting:**

- Prevent brute force
- API throttling
- IP-based limiting
- User-based limiting

**Input Validation:**

- Validate all inputs
- Server-side validation
- Type checking
- Length restrictions

## Performance Optimization

### Measuring Performance

**Core Web Vitals:**

- LCP (Largest Contentful Paint)
- FID (First Input Delay)
- CLS (Cumulative Layout Shift)

**Tools:**

- Lighthouse
- WebPageTest
- Chrome DevTools
- Vercel Analytics

**Metrics to Track:**

- Time to First Byte (TTFB)
- First Contentful Paint (FCP)
- Time to Interactive (TTI)
- Bundle size

### Optimization Techniques

**Code Splitting:**

- Route-based splitting
- Component lazy loading
- Dynamic imports
- Webpack chunks

**Image Optimization:**

- Next.js Image component
- Appropriate formats
- Responsive images
- Lazy loading

**Caching:**

- Static assets
- API responses
- CDN usage
- Browser caching

**Database:**

- Query optimization
- Indexing
- Connection pooling
- Caching layer

**Bundle Size:**

- Tree shaking
- Remove unused code
- Analyze bundle
- Code splitting

### Loading Strategies

**Above the Fold:**

- Load critical resources first
- Inline critical CSS
- Preload fonts
- Priority images

**Below the Fold:**

- Lazy load images
- Defer non-critical JS
- Load on interaction
- Progressive enhancement

**Prefetching:**

- Link prefetching
- Route prefetching
- DNS prefetch
- Preconnect

## Testing

### Testing Types

**Unit Testing:**

- Test individual components
- Test utility functions
- Isolated tests
- Fast execution

**Integration Testing:**

- Test component interactions
- Test API integration
- Test data flow
- Realistic scenarios

**End-to-End Testing:**

- Test full user flows
- Test critical paths
- Browser automation
- Complete scenarios

### Testing Tools

**Unit Tests:**

- Jest (test runner)
- React Testing Library
- Vitest (alternative)

**E2E Tests:**

- Playwright (recommended)
- Cypress
- Puppeteer

**API Tests:**

- Supertest
- MSW (Mock Service Worker)

### Testing Best Practices

**What to Test:**

- User interactions
- Business logic
- Edge cases
- Error states

**What Not to Test:**

- Implementation details
- Library internals
- Styling (unless critical)

**Writing Good Tests:**

- Clear test names
- Arrange-Act-Assert pattern
- One assertion per test
- Avoid test interdependence

**Test Coverage:**

- Aim for high coverage
- Focus on critical paths
- Don't chase 100%
- Quality over quantity

## Common Issues & Solutions

### Build Errors

**Module Not Found:**

- Check import paths
- Verify file exists
- Check case sensitivity
- Clear .next and rebuild

**TypeScript Errors:**

- Check type definitions
- Update @types packages
- Fix type mismatches
- Use type assertion carefully

### Runtime Errors

**Hydration Mismatch:**

- Server and client HTML differ
- Check for dynamic content
- Avoid random values
- Use useEffect for client-only

**Can't Access Window:**

- Accessing browser APIs in SSR
- Check if window exists
- Use useEffect
- Use dynamic imports

### Performance Issues

**Slow Page Load:**

- Check bundle size
- Optimize images
- Review data fetching
- Check network requests

**Memory Leaks:**

- Cleanup useEffect
- Cancel requests
- Remove event listeners
- Clear intervals/timeouts

### Deployment Issues

**Build Fails:**

- Check environment variables
- Review dependencies
- Check Node version
- Review error logs

**404 Errors:**

- Check file structure
- Verify route configuration
- Check deployment settings
- Review redirects

## Additional Resources

### Official Documentation

- Next.js Docs: https://nextjs.org/docs
- React Docs: https://react.dev
- Vercel Docs: https://vercel.com/docs

### Learning Resources

- Next.js Learn: https://nextjs.org/learn
- Next.js Examples: https://github.com/vercel/next.js/tree/canary/examples
- YouTube Tutorials
- Online Courses

### Community

- Next.js Discord
- GitHub Discussions
- Stack Overflow
- Reddit r/nextjs

### Tools & Extensions

- VS Code Extensions
- React DevTools
- Redux DevTools
- Next.js Bundle Analyzer

---

**Happy Coding with Next.js! 🚀**
