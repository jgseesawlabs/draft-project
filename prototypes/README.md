# Prototypes

This directory contains throwaway prototype code built during early client discovery.

## Purpose

These prototypes exist to:
- Test ideas quickly
- Spark conversations with the client
- Learn what resonates before committing to production work

## Important

**This is not production code.**

- Optimize for speed, not quality
- Skip tests, skip polish, skip best practices
- If it helps you learn faster, it's good enough
- When exploration ends, this directory gets archived

## Structure

Each prototype gets its own subdirectory:
```
/prototypes/
  client-app/        # e.g., Next.js mobile-first web app
  admin-dashboard/   # e.g., Internal admin tool
  landing-page/      # e.g., Marketing concept
```

## Deployment

Prototypes can be deployed to real URLs for demos and feedback. Use whatever is fastest - Vercel, Netlify, etc. These are temporary.

## When Exploration Ends

When the team transitions to production 5D work:

1. Learnings are captured in `.ss5d/exploration-log.md`
2. Valuable experiments are promoted via `ss5d promote`
3. This directory is archived or added to `.gitignore`
4. Production code starts fresh in the main project structure

## Documentation

All experiments are documented in `.ss5d/exploration-log.md`, not here. This directory is just code.
