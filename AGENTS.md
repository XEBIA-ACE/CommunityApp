# AGENTS.md

## Stack

- **Service:** User Service
- **Type:** business
- **Technologies:**
- Node.js with NestJS (TypeScript)
- PostgreSQL 15+ with pgcrypto for PII encryption at rest
- Redis (JWT session tokens TTL 24h, OTP codes TTL 5min, token blacklist)
- JWT / OAuth2 (RS256 signing)
- BCrypt for token hashing
- AWS Secrets Manager / Azure Key Vault for credential management
- OpenAPI 3.0 for contract documentation
- **Responsibilities:**
- User registration with role-specific profile capture for Senior, Helper, Family Member, and Admin roles
- OTP generation, rate-limited delivery coordination via SMS Gateway, and single-use validation (5-minute TTL)
- JWT access token issuance (RS256) and refresh token management; token blacklisting via Redis on role change or suspension
- Profile management: read, update, deactivate, and delete for all roles
- Family member linking to senior accounts with senior consent enforcement
- Helper profile management including skills, availability, language preferences, and verification status
- Helper KYC document submission and status tracking via Identity Verification Provider
- Account suspension and reactivation triggered by admin actions
- Publish domain events: UserRegistered, UserVerified, UserSuspended, FamilyLinked
- Enforce RBAC role claims embedded in JWT tokens

## General Rules

- Always read files in /specs before implementing
- Never implement without acceptance criteria
- Code should be simple and readable
- Avoid overengineering
- The project follows a hexagonal architecture

## Required Workflow

1. Read the specs in the /specs directory
2. Generate tasks.md if it does not exist
3. Implement based on the tasks
4. Create automated tests
5. Validate acceptance criteria

## Testing

- Cover all acceptance criteria
- Tests should be clear and straightforward
- Generated code must reach **90% unit test coverage**

## Constraints

- Do not invent requirements that are not described
- Do not change behavior without updating the spec
