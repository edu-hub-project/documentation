---
sidebar_position: 1
---

# Overview

Here docu for the google stuff


# Deployment


## Production

You should set some additional environment variables for production deployment.
  
### Hasura

[Documentation used](https://hasura.io/docs/latest/graphql/core/deployment/production-checklist.html)

```
HASURA_GRAPHQL_ADMIN_SECRET=averylongpasswordstring
HASURA_GRAPHQL_ENABLED_APIS=graphql
HASURA_GRAPHQL_ENABLE_CONSOLE=false
HASURA_GRAPHQL_DEV_MODE=false
HASURA_GRAPHQL_CORS_DOMAIN=https://my-ui.com
```

### Next.js

[Documentation used](https://nextjs.org/docs/deployment)

```
NODE_ENV=production
```

### Keycloak

?
