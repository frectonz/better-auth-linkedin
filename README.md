# better-auth-linkedin

Your `.env` file should look like this.

```
DATABASE_URL=file:local.db
BETTER_AUTH_URL=http://localhost:5173
BETTER_AUTH_SECRET=
LINKEDIN_CLIENT_ID=
LINKEDIN_CLIENT_SECRET=
```

Install packages

```bash
pnpm install
```

Setup Database

```bash
pnpm db:push
```

Run Dev Server

```bash
pnpm dev
```
