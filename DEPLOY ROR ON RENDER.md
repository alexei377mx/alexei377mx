# Deploy Ruby on Rails on Render (Free, Dockerfile)

## Table of Contents

1. [Create a Database in Neon](#1-create-a-database-in-neon)
2. [Adjust Your Rails Project](#2-adjust-your-rails-project)
   * 2.1 [Seeds and Credentials (if needed)](#21-seeds-and-credentials-if-needed)
   * 2.2 [Dockerfile](#22-dockerfile)
   * 2.3 [docker-entrypoint](#23-docker-entrypoint)
   * 2.4 [database.yml](#24-databaseyml)
3. [Configure Render](#3-configure-render)
---

## 1. Create a Database in Neon

* Create a new project at [Neon.tech](https://console.neon.tech).
* Copy the `DATABASE_URL` provided by Neon (example:
  `postgres://user:password@host/dbname`).

---

## 2. Adjust Your Rails Project

### 2.1 Seeds and Credentials (if needed)

* Update `db/seeds.rb` as required.

* Edit your local credentials:

```bash
EDITOR="code --wait" bin/rails credentials:edit
```

### 2.2 Dockerfile

Make sure to expose port **3000** in your `Dockerfile`:

```dockerfile
# Start server via Thruster by default, this can be overwritten at runtime
EXPOSE 3000
CMD ["./bin/thrust", "./bin/rails", "server"]

```

### 2.3 docker-entrypoint

Modify `bin/docker-entrypoint` to also run seeds on each startup:

```bash
#!/bin/bash -e

# If running the rails server then create or migrate existing database
if [ "${@: -2:1}" == "./bin/rails" ] && [ "${@: -1:1}" == "server" ]; then
  ./bin/rails db:prepare
  ./bin/rails db:seed

  # Optional: Load ActionCable schema if the project uses ActionCable with PostgreSQL
  RAILS_ENV=${RAILS_ENV:-production} bin/rails runner "
    ActiveRecord::Base.establish_connection(:cable)
    load Rails.root.join('db/cable_schema.rb')
  "
fi

exec "${@}"
```

### 2.4 database.yml

Adjust the production configuration so that all roles use the same Neon `DATABASE_URL`:

```yml
production:
  primary:
    url: <%= ENV["DATABASE_URL"] %>
  cache:
    url: <%= ENV["DATABASE_URL"] %>
  queue:
    url: <%= ENV["DATABASE_URL"] %>
  cable:
    url: <%= ENV["DATABASE_URL"] %>

```

---

## 3. Configure Render

1. In the [Render dashboard](https://render.com):

   * **New → Web Service**
   * Connect your **Git repository**
   * Language: **Docker**
   * Instance Type: **Free**
   * Add environment variables:
     * `RAILS_MASTER_KEY` → copy the contents of your `config/master.key`
     * `DATABASE_URL` → paste the Neon connection without the `psql` prefix.
   * Advanced:
     * `Health Check Path` → paste `/up`

Render will build your image from the `Dockerfile` and deploy your Rails app.
