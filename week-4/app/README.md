# inet4031-week4 (Starter Files Reference Repo)

This repo is cloned directly by students in Part 1 of the Week 4 lab:

```
git clone https://github.com/INET4031-Labs/inet4031-week4.git temp-week4
mkdir -p week-4/app
mv temp-week4/* week-4/app/
mv temp-week4/.[!.]* week-4/app/ 2>/dev/null
rm -rf temp-week4
```

## What's here

`app/` — the incident tracking Flask application, updated for Week 4 to read
from and write to a real PostgreSQL database instead of an in-memory list:

- `app.py` — the Flask app. Connects using `DATABASE_URL` if it's set,
  otherwise builds a connection string from `POSTGRES_USER`,
  `POSTGRES_PASSWORD`, and `POSTGRES_DB` against host `db` (the Compose
  service name students define in Part 2). Students should find this while
  reading the code, per the Week 4 wiki. Also reads `PORT` (default `5000`)
  and `FLASK_SECRET_KEY` (default `dev`) from the environment.
- `requirements.txt` — Python dependencies (`Flask`, `psycopg2-binary`).
- `Dockerfile` — builds the image Compose's `build: ./app` expects. Writing a
  Dockerfile isn't this week's exercise (that was Week 2), so it ships ready
  to use.
- `.dockerignore` — keeps `.venv`, `.env`, and bytecode out of the build
  context.
- `templates/`, `static/` — the ticket UI (create a ticket, list tickets,
  change a ticket's status), unchanged in appearance from Week 3.

On startup the app creates a `tickets` table if it doesn't already exist.
Tickets now persist in Postgres, not in a Python list, that's what makes
Part 5's `docker compose down` / `docker compose up -d` round trip actually
keep a ticket around, closing the gap Week 3 ended on.

Do not add a `docker-compose.yml`, `.env.example`, or `.env` here, students
create those themselves in Parts 2-3 of the Week 4 lab.
