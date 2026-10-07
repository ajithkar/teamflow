# TeamFlow

Full-stack team project management platform: Express 4 + TypeScript REST API, Next.js App Router frontend, MongoDB/Mongoose, JWT httpOnly cookies, optimistic locking and transactional activity/audit changes.

## Quick start
1. Start MongoDB as a single-node replica set:
   `docker run -d --name teamflow-mongo -p 27017:27017 mongo:7 --replSet rs0`
   then `docker exec teamflow-mongo mongosh --quiet --eval "rs.initiate()"`.
2. Copy `server/.env.example` to `server/.env` and set a 20+ character JWT secret.
3. `cd server && npm install && npm run seed && npm run dev`
4. In another terminal: `cd client && npm install && npm run dev`
5. Open http://localhost:3000.

## Demo accounts
| Email | Password | Role |
|---|---|---|
| maya@teamflow.dev | password123 | Apollo owner |
| arjun@teamflow.dev | password123 | Apollo member |
| lena@teamflow.dev | password123 | Both projects |
| carlos@teamflow.dev | password123 | Nova owner |

## Tests
`cd server && npm test`
`cd client && npx playwright install chromium && npx playwright test`
`npm run build` at repository root builds both apps.

## Architecture
JWT contains a tokenVersion; logout increments the DB value, revoking copied cookies. Non-members receive 404 to avoid leaking resource existence; authenticated members attempting owner-only actions receive 403. Task versions provide optimistic locking and stale writes return 409 with the current task. Member removal, task updates and deletes use MongoDB transactions. Dates are stored as UTC and overdue means `dueDate < now && status !== Done`.

### Indexes
User.email unique; Project.members; Task project/status, project/assignee, project/createdAt descending, project/dueDate; Activity project/createdAt descending.

## Known limitations
- Client rendering is intentionally used instead of SSR data fetching.
- UI currently focuses on the core board/table workflow; deeper task-detail/member management screens can be expanded.
- No email delivery by design.
- No drag-and-drop by design.
- No file storage for task designs in this scope.
- No websocket live updates in this scope.
- Local development requires MongoDB replica-set support.
- E2E depends on a running replica-set API database.

## Time spent
| Phase | Time |
|---|---:|
| Scaffold/auth | TBD |
| API/domain | TBD |
| Frontend | TBD |
| Tests/docs | TBD |
