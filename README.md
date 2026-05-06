# FCM release v
# Federated Content Manager

## Development Workflow

Our development workflow follows these steps:

1. Feature Development

   - Create a feature branch from `dev` (format: `feature/*`)
   - Version in feature branches should be `x.y.z-b.n` (beta)
   - Create PR to merge into `dev`

2. Development to Staging

   - Merge feature PRs into `dev`
   - Create PR from `dev` to `staging`
   - Version changes from beta to RC (`x.y.z-rc.n`)

3. Staging to Production

   - Test thoroughly in staging
   - Version becomes release version (`x.y.z`)
   - Create PR from `staging` to `main`

4. Version Alignements (hotfix)
   - Hotfixes triggers a retag on the FE repo

### Environment Variables

### Guide for deployment:

| Environment variable                 | Description                                                                                                                   | Default value                                     | Default value can be used in deployment |
| ------------------------------------ | ----------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------- | --------------------------------------- |
| **FCM_USER**                         | Email to create an user                                                           | fcm@fmc.io                                        | Yes                                     |
| **FCM_PASSWORD**                     | Password to create an user                                                        | fcm123#                                           | Yes                                     |
| **POSTGRES_HOST**                    | Postgres database host                                                                                                        | localhost                                         | No                                      |
| **POSTGRES_USER**                    | Postgres database user                                                                                                        | postgres                                          | No                                      |
| **POSTGRES_PASSWORD or DB_PASSWORD** | Postgres database password                                                        | postgres                                          | No                                      |
| **POSTGRES_DB**                      | Postgres database name                                                                                                        | postgres                                          | No                                      |
| **POSTGRES_PORT**                    | Postgres database port                                                                                                        | 5432                                              | No                                      |
| **ENCRYPTION_PASSWORD**              | Random UUID string to be used for encrypting and decrypting data                  | 14ec44e0-db48-4cb2-bde4-5bc73095807b              | No                                      |
| **CORS_ALLOWED_ORIGINS**             | Comma separated origins from which the backend is allowed to accept requests from                                             | http://localhost:3000,http://localhost:3001       | No                                      |
| **NODE_ENV**                         | Runing mode used internally, can be either _development_ or _production_                                                      | production                                        | Yes                                     |
| **APP_HOST**                         | Frontend URL (and used as SAML issuer )                                                                                       | localhost:3001                                    | Yes                                     |
| **SAML_ENTRYPOINT_ID**               | Url in order to do the SAML authentication                                        | https://accounts.google.com/o/saml2/idp?idpid=*** | No                                      |
| **SAML_SECRET**                      | Token to be used to authenticate through SAML                                     | ksadnHBWEW832rlndHUOWQ923he1l                     | No                                      |
| **JWT_SECRET**                       | Seed used to create the JWT tokens                                                                                            | secreyKey                                         | Yes                                     |
| **BEARER_TOKEN_EXPIRE_TIME**         | Expiration time for logout                                                                                                    | 30m                                               | Yes                                     |
| **JWT_REFRESH_SECRET**               | Expiration time for JWT secret                                                                                                | 2h                                                | Yes                                     |
| **REFRESH_TOKEN_EXPIRE_TIME**        | Expiration time for logout                                                                                                    | 2h                                                | Yes                                     |
| **CHECK_NEW_MSSP_INSTANCES**         | Boolean that determains if the user wants the FCM to check for new instances from the MSSP                                    | true                                              | Yes                                     |                                   |
| **MAINTENANCE_TOKEN**                | Token to be used in maintenance routes                                                                                        | f4b9c2c6-6fc9-4770-9574-33ca87c5a72f              | Yes                                     |
| **INTERVAL_UPDATE_FAILED_TASKS_MIN** | Time in min, that FCM will update failed taks for exceeded time                                                               | 3000                                              | Yes                                     |

### Running locally with development environment (optional)

```bash
cd content-distribution-platform-server

openssl req -x509 -nodes -days 365 -newkey rsa:2048 -keyout localhost.key -out localhost.crt

docker-compose up -d

npm i


npm run start
```

## Running Unit Tests

```bash
cd content-distribution-platform-server

npm i

npm run test

```

## Running E2E Automated Tests

```bash
cd content-distribution-platform-server

npm i

npm run test:e2e

```
# Federated Content Manager

### Environment Variables

| Environment variable | Description                                                   | Example value         | Required |
| -------------------- | ------------------------------------------------------------- | --------------------- | -------- |
| **SERVER_HOST**      | Back-end url to perform requests                              | http://localhost:3000 | No       |
| **TIMEOUT**          | Timeout, that can be used, for example, in the axios requests | 5000 (ms)             | No       |

### Build Application

After having the server configured and running, run the following commands to setup the front-end application:

```bash
cd -content-distribution-platform-app

npm i

npm run dev
```

Open [http://localhost:3001](http://localhost:3001) with your browser to see the result.

## Deployment Process

This section outlines our deployment pipeline stages:

1. Development (beta versions)
2. Staging (release candidates)
3. Production (release versions)

### Version Management

Our version management follows semantic versioning with pre-release tags:

- Development: x.y.z-b.n (beta versions)
- Staging: x.y.z-rc.n (release candidates)
- Production: x.y.z (release versions)

The version is automatically managed by our CI/CD pipeline based on branch merges.

Version increments happen automatically:

- Feature → Dev: Increases beta number (b.1 → b.2)
- Dev → Staging: First merge creates rc.1, subsequent merges increment rc number (rc.1 → rc.2)
- Staging → Production: Removes pre-release tag

Testing the new version management system with build-info.json
