# Credential Storage — Spec

## Name

Credential Storage

## Scope

Defines how credentials are stored, retrieved, and referenced across all tool integrations.

**In scope:**
- Approved and prohibited storage mechanisms.
- Conventions for referencing credentials in artifacts and documentation.
- Repo hygiene requirements.
- Boundary declarations for API Connectivity credentials.
- OAuth token conventions for API-level integrations.

**Out of scope:**
- Access control and permissions beyond scope declarations.
- Credential rotation and lifecycle management.

## Requirements

### Storage

1. A credential manager (e.g., Bitwarden, 1Password) is the authoritative source of truth for all long-lived credentials.
2. Credentials are retrieved at runtime, never stored at rest in the repository.
3. No API keys, passwords, tokens, or secrets in any tracked repo folder — no exceptions. The gitignored `secrets/` directory is the sole exception for runtime credential access (see below).

### Acceptable Storage Mechanisms

| Mechanism | Acceptable | Conditions |
|---|---|---|
| Credential manager vault | yes | Authoritative storage for all long-lived credentials. |
| `secrets/` directory | yes | Gitignored directory for runtime credential access. The principal manually provisions JSON files containing tokens needed for the session. Files are not committed, not tracked, and may be added/removed between sessions. |
| Environment variables | session only | Ephemeral session tokens. Never persisted to disk or committed. |
| OS keychain | yes | For tool-specific credentials managed outside the vault (e.g., SSH keys). |
| `.env` files | no | — |
| Plaintext in repo | no | — |
| Hardcoded in artifacts | no | — |
| Config files committed to git | no | — |

### Repo Hygiene

1. `.gitignore` must exclude patterns that could contain credentials: `.env`, `.env.*`, `*.key`, `*.pem`, `secrets/`.
2. Credential values must never appear in commit messages, diffs, or artifact content.
3. If a credential is accidentally committed, it must be rotated immediately. Git history rewriting is secondary to rotation.

### Referencing Credentials

1. In documentation and artifacts, reference credentials by their vault item name — never by value.
2. Use the format: `[Credential: <item-name>]` when documenting which credential a tool requires.
3. Interface contracts must document the authentication method in the contract table, not the credential itself.

### Boundary Declarations

When a tool uses API Connectivity (see Integration Framework), its credential mapping must declare the provisioned scopes. The scopes constitute the tool's hard boundary — what is physically possible with that credential.

**Format:** `[Credential: <item-name>] — Scopes: <scope-list>`

The scope list is the authoritative record of what the credential allows. If an agent requests an action that requires a scope not in the declared list, the action is outside the hard boundary and must be escalated to the principal.

### OAuth Token Convention

For OAuth-based API Connectivity, the credential manager stores the long-lived credentials. Access tokens are ephemeral.

**What the vault stores:**
- Client ID (or app ID)
- Client secret (if applicable)
- Refresh token (long-lived)
- Token endpoint URL
- Authorized scopes

**What is ephemeral:**
- Access tokens — retrieved at session start via refresh token exchange, used for the session, discarded on close. Never stored in the vault or written to disk.

**Refresh lifecycle:** If a refresh token expires or is revoked, the API Connectivity capability is unavailable until the principal re-provisions. The session escalates rather than attempting re-authorization.

### Local Secrets Convention

The `secrets/` directory provides runtime credential access without requiring a credential manager CLI. This decouples API Connectivity from any specific credential retrieval tool.

**Directory:** `secrets/` (gitignored, at repo root).

**File convention:** `secrets/{tool-name}.json` — one file per tool, named to match the tool's registry name (lowercase, hyphenated). Contains the credentials needed for runtime API calls.

**Lifecycle:**
1. The principal provisions credential files manually before or during a session.
2. Agents read credentials from `secrets/` at runtime.
3. Files may be added, updated, or removed between sessions.

**Security:** The `secrets/` directory is excluded from git via `.gitignore`. It must never be committed. Agents must never write credential values to any tracked file, commit message, or artifact.

## Dependencies

- Integration Framework — constrains how authentication is documented in interface contracts. Boundary Framework defines hard and soft boundary concepts.
- Tool Registry — each registered tool must declare its credential source.

## Notes

- As new tools are added, their credential sources should be mapped in this spec's Per-Tool Credential Mapping section (added when you have tools to map).
