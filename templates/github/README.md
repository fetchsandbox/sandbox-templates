# GitHub REST API Template

Repository, issue, and pull request management sandbox with realistic development workflow data.

## Resources & State Machines

| Resource | States | Key Transitions |
|----------|--------|-----------------|
| Repos | active ↔ archived | Archive and unarchive repositories |
| Issues | open ↔ closed | Track bugs and feature requests |
| Pull Requests | open → closed | Code review and merge workflow |

## Scenarios

| Scenario | Description |
|----------|-------------|
| `default` | All CRUD operations succeed |
| `auth_failure` | Revoked/expired token (401) |
| `rate_limited` | API abuse detection (403) |
| `repo_not_found` | Deleted or private repo (404) |
| `merge_conflict` | PR has unresolved conflicts (409) |
| `server_error` | GitHub service outage (500) |
| `read_only` | Read-only token — writes return 403 |

## Seed Data

- 3 repos (Go API gateway, TypeScript component lib, Python ML pipeline)
- 3 issues (concurrency bug, feature request, closed memory leak)
- 3 pull requests (merged fix, open feature, draft dependency update)
- 3 users (org account, staff engineer, senior SRE)
