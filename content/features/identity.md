---
title: Identity
type: feature
status: draft
sources: [raw/test-cases/by-feature/fe_identity.jsonl, raw/docs/devrev-developer-docs.md, raw/docs/devrev-docs-scraped.md, raw/docs/devrev-agent-dump-settings.md]
related: ["entities/dev-user", "entities/rev-user", "entities/group", "features/mfz"]
last_updated: 2026-04-12
---

# Identity

## What it does
The Identity feature manages all aspects of user authentication, authorization, and user account lifecycle within DevRev. It encompasses auth token management (PAT creation, deletion, revocation), dev user CRUD operations (create, read, update, delete, activate, deactivate, merge), role-based access control (role sets, roles, access control entries), and account management (create, update, delete, export, merge, duplicate detection). This is the foundational identity layer that underpins all other DevRev features, with 3015 test cases making it the most extensively tested feature.

## Why it exists
Every multi-tenant SaaS platform requires a robust identity and access management layer. DevRev users need to authenticate via tokens (PATs), manage their profiles and organizations, control who can access what resources via roles and permissions, and manage customer accounts that map to external organizations. Without this, no other feature can securely operate.

## Key behaviors
- **Auth token lifecycle**: Create PATs with configurable expiration (max 1825 days), list, get, update, delete, and self-delete tokens
- **Token self-deletion**: Supports empty body `{}` defaulting to PAT token type revocation
- **Dev user management**: Full CRUD with activate/deactivate, bulk license updates, merge capabilities, email updates, phone number verification (send-code/check-code)
- **Dev user identity linking**: Link and unlink external identities to dev users
- **Dev user self-service**: Self-read, self-update, self-delete, post-login hooks, logout
- **Dev user export**: Async export support with [[glossary/don]]-format job IDs
- **Account management**: CRUD with environment defaults (production), domains, websites, tiers, phone numbers, SLA assignment
- **Account operations**: Merge accounts, detect/list/count/ignore duplicates, export (sync and async), sample CSV generation, bulk CSV creation
- **Account commerce details**: Get and list commerce details per account
- **Role management**: Create, list, get, update, delete roles; apply roles to principals; list principals per role
- **Role sets**: Create, list, get, update, delete, count role sets; apply role sets; UI config retrieval
- **Access control entries**: Create, list, delete entries with filtering by principal type and combined filters
- **Principal access graph**: Query the access graph for a principal
- **User privileges**: Query privileges for users; list dynamic groups

## Entry points
- **Base URL**: `https://api.devrev.ai/internal/`
- All endpoints require `Authorization: Bearer $TOKEN` header
- All endpoints use `Content-Type: application/json`

## API endpoints

| Endpoint | Methods | Description |
|----------|---------|-------------|
| `auth-tokens.create` | POST | Create a new PAT/token |
| `auth-tokens.delete` | POST | Delete a specific token |
| `auth-tokens.get` | POST | Retrieve token details |
| `auth-tokens.info` | POST | Get token info |
| `auth-tokens.list` | POST | List all tokens |
| `auth-tokens.self.delete` | POST | Revoke own token |
| `auth-tokens.update` | POST | Update token properties |
| `dev-users.create` | POST | Create a dev user |
| `dev-users.get` | GET, POST | Retrieve dev user |
| `dev-users.list` | GET, POST | List dev users |
| `dev-users.update` | POST | Update dev user |
| `dev-users.delete` | POST | Delete dev user |
| `dev-users.activate` | POST | Activate dev user |
| `dev-users.deactivate` | POST | Deactivate dev user |
| `dev-users.merge` | POST | Merge two dev users |
| `dev-users.count` | GET, POST | Count dev users |
| `dev-users.self` | GET, POST | Get current user |
| `dev-users.self.update` | POST | Update own profile |
| `dev-users.self.delete` | POST | Delete own account |
| `dev-users.logout` | POST | Logout current user |
| `dev-users.post-login` | POST | Post-login hook |
| `dev-users.email.update` | POST | Update email |
| `dev-users.phone-number.send-code` | POST | Send phone verification |
| `dev-users.phone-number.check-code` | POST | Verify phone code |
| `dev-users.identities.link` | POST | Link external identity |
| `dev-users.identities.unlink` | POST | Unlink external identity |
| `dev-users.highlights.create` | POST | Create user highlight |
| `dev-users.highlights.delete` | POST | Delete user highlight |
| `dev-users.bulk-update-licenses` | POST | Bulk update licenses |
| `dev-users.export.async` | POST | Async export dev users |
| `accounts.create` | POST | Create account |
| `accounts.get` | POST | Get account |
| `accounts.update` | POST | Update account |
| `accounts.delete` | POST | Delete account |
| `accounts.count` | GET, POST | Count accounts |
| `accounts.export` | POST | Export accounts |
| `accounts.export.async` | POST | Async export accounts |
| `accounts.group` | POST | Group accounts |
| `accounts.merge` | POST | Merge accounts |
| `accounts.get-sla` | GET, POST | Get account SLA |
| `accounts.sample-csv.get` | GET, POST | Get sample CSV |
| `accounts.create.bulk.csv` | POST | Bulk create from CSV |
| `accounts.delete.validate` | POST | Validate before delete |
| `accounts.duplicates.list` | GET, POST | List duplicate pairs |
| `accounts.duplicates.count` | GET, POST | Count duplicates |
| `accounts.duplicates.ignore` | POST | Ignore duplicate pair |
| `accounts.commerce-details.get` | GET, POST | Get commerce details |
| `accounts.commerce-details.list` | GET, POST | List commerce details |
| `role-sets.create` | POST | Create role set |
| `role-sets.get` | GET, POST | Get role set |
| `role-sets.list` | GET, POST | List role sets |
| `role-sets.update` | POST | Update role set |
| `role-sets.delete` | POST | Delete role set |
| `role-sets.count` | POST | Count role sets |
| `role-sets.apply` | POST | Apply role set |
| `role-sets.ui-config.get` | GET, POST | Get UI config |
| `roles.create` | POST | Create role |
| `roles.get` | POST | Get role |
| `roles.list` | POST | List roles |
| `roles.update` | POST | Update role |
| `roles.delete` | POST | Delete role |
| `roles.apply` | POST | Apply role to principal |
| `roles.principals.list` | POST | List principals for role |
| `access-control-entries.create` | POST | Create ACE |
| `access-control-entries.list` | GET, POST | List ACEs |
| `access-control-entries.delete` | POST | Delete ACE |
| `principal.access-graph` | POST | Query access graph |
| `user.privileges` | POST | Query user privileges |
| `users.list-dynamic-groups` | POST | List dynamic groups |

## User Types

| Type | Description |
|------|-------------|
| Dev User | Internal team member with app access |
| Rev User | Customer/contact (external) |
| System User | DevRev Bot (automated actions) |
| Service Account | Programmatic access for integrations |
| Shadow User | No app access; created by AirSync for tracking |

## RBAC Model
- **Roles** = sets of privileges (permissions) on objects.
- **Groups** = collections of users assigned roles.
- Users are assigned to Groups (not directly to roles).
- Highest privilege wins when a user belongs to multiple groups.
- Supports field-level access control and condition-based restrictions.

## Creating User Roles (UI)
1. Go to Settings > User Management > Roles.
2. Click + Create new.
3. Enter role name and description.
4. Select an object (e.g., Ticket, Inbox) to assign permissions.
5. Optionally add conditions to restrict permissions.
6. Select Apply to all subtypes or configure per subtype.
7. Click Save.

Customer roles are managed under Settings > Customer Management > Roles. Assigned to customer groups or individual customers.

## SSO / SAML
- Configured under Settings > External identity provider setup (`/docs/product/sso-saml`).
- Supports **SAML 2.0** and **OpenID Connect (OIDC)** protocols.
- Supported identity providers: **Okta**, **Azure AD**, **Google Workspace**, **JumpCloud**.
- SCIM 2.0 for automated user provisioning/deprovisioning.
- DevRev supports **SP-initiated SSO only** (not IDP-initiated). Workaround: bookmark workspace URL in identity provider portal.
- Connections are created with `enabled: false` by default; must be explicitly enabled.

### SSO Connection Naming
The `connection_name` must follow pattern: `^[a-zA-Z0-9](-[a-zA-Z0-9]|[a-zA-Z0-9])*$`
- Start with alphanumeric character
- Only alphanumeric characters or hyphens (no consecutive/trailing hyphens)
- Must be unique within organization
- Format: `<dev_oid>-<CUSTOM-STRING>`

### SSO Configuration Steps (API)
1. Create authentication connection via API (`dev-orgs.auth-connections.create`)
2. Enable connection via API (`dev-orgs.auth-connections.toggle`)
3. Verify at `https://app.devrev.ai/<DEV_ORG_SLUG>`
4. Optionally disable alternative authentication methods

### Customer Portal SSO (Federated Identity)
Customer-facing login methods for the portal and PLuG:
- **Email OTP** -- one-time password sent to customer email
- **Federated identity** -- Okta, Azure AD, Google Workspace via SAML/OIDC
- **JWT-based authentication** -- programmatic token-based login
Configured under **Settings > Plug & Portal > Portal Settings > Login methods**.

### SCIM Provisioning
SCIM 2.0 enables automated user provisioning and deprovisioning from the identity provider. When a user is added/removed in the IdP, the change is synced to DevRev automatically.

## Session Policies & Security

### Email Domain Auto-Join
Toggle under **Settings > Organization**: when enabled, users with your org's email domain can join without an invitation.

### IP Allowlisting
[gap] No IP allowlisting configuration detail found in current sources. Requires further investigation.

### 2FA / MFA
[gap] No dedicated 2FA/MFA configuration detail found in current sources beyond SSO-provider-level MFA enforcement. Requires further investigation.

## Groups
A group is a collection of users that can contain either organizational users or customers.

### Static Groups
Manually managed collections. Administrators add/remove users. Group members can add more members. Suited for precise control or non-automatable membership criteria.

### Dynamic Groups
Automatically maintain membership based on predefined rules evaluating user attributes. Users are added when they meet criteria and removed when they no longer qualify. Eliminates manual management overhead.

## Roles
A role is a defined grouping of access privileges determining what actions a user can perform on different objects.

### Actors
An actor is an entity performing an action: org member, customer, system user, or service account. Roles control what access actors have on the app, portal, and PLuG.

### Scope of Control
Roles grant permissions across: stock objects (issues, tickets, etc.), custom objects and subtypes, and specific actions (read, write, update, delete).

### Dynamic Access Control
Permissions can be granted conditionally based on object attributes (e.g., priority, owner).

## Access Control
The system checks user access through a four-step verification:
1. Fetch all user groups
2. Fetch roles associated directly with the user or their groups
3. Locate the specific object requiring access (e.g., Tickets)
4. Review each role's configuration for that object

When unauthorized actions are attempted, users see: "You are not authorized to perform this action."

### MFZ Policies
Two predefined roles:
- **Admins Role**: Full permissions across all operations
- **Platform Users Role**: Create/read/update/delete personal dashboards/reports; create personal datasets; cannot access other users' datasets by default

### Vista Privileges
Users need minimum dashboard access. Operations: Read (view), Create (build), Update (modify), Share (requires update permissions).

## Token Types
- **Personal Access Tokens (PAT):** Settings > Account > Personal Access Tokens.
- **Application Access Tokens (AAT):** For server-to-server authentication.
- **Rev session tokens:** For customer portal authentication.

## Related flows
- [gap] Login/authentication flow
- [gap] User onboarding flow
- [gap] Account provisioning flow

## Related scenarios
- [gap] Scenarios to be created from 3015 test cases

## Open questions
- [gap] How does the STS (Security Token Service) integrate with the auth-tokens endpoints?
- [gap] What are the exact permission requirements for each role/access-control operation?
- [gap] How does the `post-login` hook work and what triggers it?
- [gap] What are the complete set of environment values beyond "production" and "staging"?
