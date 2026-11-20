# Laravel10-Vue-Survey-App

The beginning of a survey application with a Laravel 10 backend and a separate Vue 3 single-page frontend.

## Context

A learning project started by Oleksandr Karabudka in August 2023 (work on 1 and 2 August) to practise building a Vue 3 SPA next to a Laravel API. Only the frontend foundation was built: project setup, routing, state store, styling and the first views. The survey logic and the backend API were not implemented.

## Features

- Vue 3 SPA in `vue/` with views for login, registration, dashboard and surveys.
- Two layouts: `AuthLayout` for guest pages and `DefaultLayout` for the authenticated area.
- Route guard: pages marked `requiresAuth` redirect to the login page when there is no token in the store; logged-in users are redirected away from guest pages.
- Vuex store with a `user` state (`data`, `token`) prepared for authentication.
- UI built with Tailwind CSS, Headless UI and Heroicons.
- Laravel 10 backend scaffold with Sanctum installed; no custom API endpoints yet.

## Tech stack

- PHP 8.1+, Laravel 10, Laravel Sanctum
- Vue 3, Vue Router 4, Vuex 4, Vite
- Tailwind CSS, @headlessui/vue, @heroicons/vue
- MariaDB 10.5, Redis, MailHog
- Docker Compose (nginx, PHP-FPM 8.2)

## Architecture

- Backend and frontend are separate: the Laravel app sits in the repository root, the Vue app in `vue/` with its own `package.json` and Vite config.
- Frontend structure: `vue/src/router` (routes and guard), `vue/src/store` (Vuex), `vue/src/components` (layouts), `vue/src/views` (pages).
- The intended token-based flow is visible in the router guard and store, but login and registration are not yet connected to the backend.

## Getting started

Backend (requires Docker and Docker Compose):

```bash
sh docker/conf/ssl/generate.sh        # create the local self-signed TLS certificate
cp .env.example .env                  # then adjust the DB_* values
docker compose up -d web db           # web starts php and mailhog as dependencies
docker compose exec php composer install
docker compose exec php php artisan key:generate --ansi
docker compose exec php php artisan migrate
```

When using the `db` container, set `DB_HOST=db` in `.env`. The backend is served at http://localhost.

Frontend:

```bash
cd vue
npm install
npm run dev
```

Vite prints the local URL of the SPA.

## Testing

Only the default Laravel example tests are included; the Vue app has no tests.

```bash
docker compose exec php php artisan test
```

## Status

Archived, snapshot of 2023: an unfinished learning project (only the frontend skeleton was built). For a finished full-stack example see [media-app](https://github.com/okarabudka/media-app).

## License

MIT, see [LICENSE](LICENSE).
