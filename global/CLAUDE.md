# CLAUDE CODE CONFIGURATION

## Core Behavior
- **No fallbacks** - If something fails, debug and fix it. Don't give up.
- **No hardcoding** - Use parameters, env vars, or config. Never hardcode paths, IDs, or data.
- **No secrets in code** - Use environment variables for API keys and credentials.

## Code Quality
- Match existing codebase conventions
- Prefer editing existing files over creating new ones
- Don't over-engineer - keep solutions minimal

## Decision Points
For high-impact decisions, present options before proceeding:
- Architecture choices (monolith vs microservices)
- Database schema design
- Authentication approach
- Major dependency additions
- API design patterns

Rule: If reversing a decision would take >1 day of rework, present options first.

## Environment
- **Split keyboard** - No numpad, don't suggest numpad shortcuts
- **Dev server always running** - Don't run `npm run dev` unless asked. Hot reload handles changes.
