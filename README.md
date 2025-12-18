Twenty CRM on Coolify
=====================

Self-host **Twenty CRM** on your own infrastructure using **Coolify**, with Docker, PostgreSQL, Redis, and automatic HTTPS via Traefik.

This repository provides a **Coolify-ready `twenty-docker-compose.yml`** that lets Coolify fully manage networking, domains, and TLS certificates.


🚀 Features
-----------

-   Open-source CRM (Twenty)

-   Coolify-native deployment

-   Automatic HTTPS (Traefik + Let's Encrypt)

-   PostgreSQL 16

-   Redis 7

-   Persistent storage for uploads and database

-   Worker service for background jobs

-   Production-ready defaults



📦 Requirements
---------------

-   A server with **Coolify** installed

-   A domain name pointing to your Coolify server

-   Docker (managed by Coolify)

-   Optional:

    -   SMTP credentials (for email)

    -   Google / Microsoft OAuth credentials



🧱 Stack
--------

-   **Twenty CRM** -- `twentycrm/twenty`

-   **PostgreSQL** -- `postgres:16-alpine`

-   **Redis** -- `redis:7-alpine`

-   **Reverse Proxy** -- Traefik (via Coolify)



📁 Repository Structure
-----------------------

```
.
├── docker-compose.yml
├── README.md
└── LICENSE

```


⚙️ Deployment (Coolify)
-----------------------

### 1\. Create a new Resource

-   Application type: **Docker Compose Empty**

-   Copy + Paste the `twenty-docker-compose.yaml` 


### 2\. Configure Domain

In **Coolify → Domains**:

-   Add your domain:

    ```
    crm.yourdomain.com

    ```

-   Enable **HTTPS**

-   Let Coolify handle certificates

Coolify will automatically inject:

-   `SERVICE_FQDN_SERVER`

-   `SERVICE_URL_SERVER`


### 3\. Environment Variables

In **Coolify → Configure → Environment Variables**, set at minimum:

```
SERVER_URL=https://crm.yourdomain.com
APP_SECRET=replace_me_with_a_random_string_minimum_32_characters

```

#### Optional (Email)

```
EMAIL_DRIVER=smtp
EMAIL_SMTP_HOST=smtp.yourprovider.com
EMAIL_SMTP_PORT=587
EMAIL_SMTP_USER=your_user
EMAIL_SMTP_PASSWORD=your_password
EMAIL_FROM_ADDRESS=contact@yourdomain.com
EMAIL_SYSTEM_ADDRESS=system@yourdomain.com

```

#### Optional (OAuth)

```
AUTH_GOOGLE_CLIENT_ID=
AUTH_GOOGLE_CLIENT_SECRET=
AUTH_GOOGLE_CALLBACK_URL=https://crm.yourdomain.com/auth/google/callback

AUTH_MICROSOFT_CLIENT_ID=
AUTH_MICROSOFT_CLIENT_SECRET=
AUTH_MICROSOFT_CALLBACK_URL=https://crm.yourdomain.com/auth/microsoft/callback

```


### 4\. Deploy

Click **Deploy** in Coolify.

Initial startup may take a few minutes while:

-   Database initializes

-   Migrations run

-   Worker starts


🩺 Health Checks
----------------

-   Application health endpoint:

    ```
    /healthz

    ```

Coolify uses this to determine container readiness.


🔐 Security Notes
-----------------

-   **Change `APP_SECRET`** before production use

-   Use HTTPS only (handled automatically by Coolify)

-   Back up your database volume regularly

-   Restrict Coolify access to trusted users


🛠 Customization
----------------

Common things you may want to customize:

-   Email provider (SMTP)

-   OAuth providers (Google / Microsoft)

-   Storage backend (local vs S3-compatible)

-   Disable migrations or cron jobs (advanced)


🧩 Troubleshooting
------------------

### App doesn't start

-   Ensure `APP_SECRET` is set

-   Check database health logs

-   Wait for migrations to complete

### Domain not routing

-   Confirm domain DNS points to the Coolify server

-   Verify domain is added in Coolify

-   Ensure HTTPS is enabled

### OAuth login fails

-   Callback URLs must match **exactly**

-   Ensure `SERVER_URL` uses HTTPS


📄 License
----------

This project is licensed under the **MIT License**.

See the `LICENSE` file for details.

* * * * *

🙌 Credits
----------

-   [Twenty CRM](https://twenty.com/)

-   [Coolify](https://coolify.io/)
