---
description: Create a new API endpoint with validation, error handling, and TypeScript for any framework
model: claude-sonnet-4-5
---

Create a new API endpoint following modern best practices for solo developers.

## Requirements

API Endpoint: $ARGUMENTS

## Implementation Guidelines

### 1. **Framework Detection**
Detect the project's framework/runtime automatically or ask the user:
- **Next.js** (App Router or Pages API)
- **Express.js**
- **Fastify**
- **Hono**
- **Deno** (Fresh, Oak, or native)
- **Bun** (Elysia, Hono, or native)
- **NestJS**
- **tRPC**
- **Other** (adapt patterns accordingly)

### 2. **Validation**
- **Recommended**: Zod for runtime type validation (framework-agnostic)
- **Alternatives**:
  - TypeBox (for Fastify/Elysia native schemas)
  - Yup, Joi (if already in project)
  - Framework-native validators (tRPC, NestJS class-validator)
- Validate input early (before DB/API calls)
- Return clear validation error messages

### 3. **Error Handling**
- Use framework-appropriate error handling patterns:
  - Next.js: try/catch in route handlers
  - Express/Fastify: Error middleware
  - Hono/Elysia: Error handlers
  - NestJS: Exception filters
- Consistent error response format
- Appropriate HTTP status codes
- Never expose sensitive error details

### 4. **TypeScript**
- Strict typing for requests/responses
- Shared type definitions
- No `any` types

### 5. **Security**
- Input sanitization (prevent XSS, SQL injection)
- CORS configuration if needed
- Rate limiting (use existing middleware or recommend solution)
- Authentication/authorization:
  - Detect existing auth (NextAuth, Lucia, Clerk, Supabase Auth, etc.)
  - Use framework-appropriate middleware/guards
  - Validate tokens/sessions before handler execution

### 6. **Response Format**
```typescript
// Success
{ data: T, success: true }

// Error
{ error: string, details?: unknown, success: false }
```

## Code Structure

Create a complete API endpoint with:

1. **Route Handler File** - Appropriate for the detected framework
   - Next.js: `app/api/[route]/route.ts` or `pages/api/[route].ts`
   - Express/Fastify: `routes/[route].ts` or `controllers/[route].ts`
   - Hono/Elysia: `routes/[route].ts`
   - Deno: Framework-specific structure
2. **Validation Schema** - Zod schemas for request/response
3. **Type Definitions** - Shared TypeScript types
4. **Error Handler** - Centralized error handling (middleware or utility)
5. **Example Usage** - Client-side fetch example

## Best Practices to Follow

-  Early validation before expensive operations
-  Proper HTTP status codes (200, 201, 400, 401, 404, 500)
-  Consistent error response format
-  TypeScript strict mode
-  Minimal logic in routes (use services/utils)
-  Environment variable validation
-  Request/response logging for debugging
- L No sensitive data in responses
- L No database queries without validation
- L No inline business logic (extract to services)

## Execution Steps

1. **Detect Framework**: Check package.json, config files, or ask the user
2. **Analyze Project Structure**: Understand existing patterns and conventions
3. **Generate Code**: Create endpoint following framework-specific patterns
4. **Provide Integration Guide**: Show how to register/import the new endpoint

Generate production-ready code that follows the project's existing patterns and can be immediately integrated.
