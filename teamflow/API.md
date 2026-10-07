# TeamFlow API

All responses use JSON except 204. Auth uses the `teamflow` httpOnly cookie.

| Status | Meaning |
|---|---|
| 400 | validation/bad request |
| 401 | unauthenticated, expired or revoked session |
| 403 | authenticated member lacks owner permission |
| 404 | missing/invalid/non-member resource |
| 409 | duplicate or stale optimistic version |

Endpoints: `POST /api/auth/register`, `POST /api/auth/login`, `POST /api/auth/logout`, `GET /api/auth/me`; `POST/GET /api/projects`; `GET/PATCH /api/projects/:projectId`; `GET/POST /api/projects/:projectId/members`; `DELETE /api/projects/:projectId/members/:userId`; `GET/POST /api/projects/:projectId/tasks`; `GET/PATCH/DELETE /api/tasks/:taskId`; `GET/POST /api/tasks/:taskId/comments`; `DELETE /api/comments/:commentId`; `GET /api/projects/:projectId/activity`; `GET /api/projects/:projectId/dashboard`; `GET /api/health`.
