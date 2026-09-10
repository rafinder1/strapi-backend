# Strapi Backend

Strapi uruchamiany w Docker Compose wraz z PostgreSQL.


## Pierwsze uruchomienie

Uzupełnij plik:

```text
backend/.env
```

o wymagane zmienne środowiskowe i sekrety Strapi.

Następnie uruchom:

```bash
docker compose --env-file backend/.env up -d --build
```

Sprawdź status kontenerów:

```bash
docker compose ps
```

Podejrzyj logi Strapi:

```bash
docker compose logs -f strapi
```

## Zmienne środowiskowe

Lokalne zmienne środowiskowe znajdują się w:

```text
backend/.env
```

Plik `.env` zawiera sekrety i **nie powinien być commitowany do repozytorium**.

Do repozytorium należy dodać:

```text
backend/.env.example
```

Plik `.env.example` powinien zawierać jedynie przykładowe wartości, bez prawdziwych sekretów.

Przykładowa struktura:

```text
.
├── compose.yaml
└── backend/
    ├── .env
    ├── .env.example
    ├── Dockerfile
    ├── package.json
    ├── package-lock.json
    ├── config/
    ├── src/
    └── ...
```

## Docker

Projekt wykorzystuje wieloetapowy (`multi-stage`) Docker build:

1. **deps** – instalacja zależności Node.js,
2. **builder** – budowanie aplikacji Strapi,
3. **runner** – uruchomienie gotowej aplikacji.

Do uruchomienia produkcyjnego kontener korzysta z:

```bash
npm run start
```

## Bezpieczeństwo

Nie commituj do repozytorium:

* `backend/.env`,
* haseł do PostgreSQL,
* `APP_KEYS`,
* `JWT_SECRET`,
* `ADMIN_JWT_SECRET`,
* `API_TOKEN_SALT`,
* `TRANSFER_TOKEN_SALT`,
* `ENCRYPTION_KEY`,
* innych sekretów produkcyjnych.

W środowisku CI/CD sekrety powinny być przechowywane jako **CI/CD Secrets / Environment Variables** i przekazywane do aplikacji podczas deployu.
