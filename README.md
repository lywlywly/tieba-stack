# tieba-stack

Docker Compose stack for:

- `services/archive`: [Python Tieba archiver](https://github.com/lywlywly/tieba-archive)
- `services/viewer`: [Next.js Tieba viewer](https://github.com/lywlywly/tieba-viewer)
- PostgreSQL 16

Default services:

- `postgres`
- `viewer`

`archive` is opt-in and started manually.

## Setup

```bash
git submodule update --init --recursive
cp .env.example .env
mkdir -p output
touch blacklist.txt
```

Edit `.env` and set at least `BDUSS` and `FORUM_NAMES`.

## Run

Start PostgreSQL and the viewer:

```bash
docker compose up
```

Viewer: `http://localhost:3000`

Run the crawler manually when needed. On first run, do this once to initialize and populate the database:

```bash
docker compose --profile archive up archive
```

Stop the crawler:

```bash
docker compose stop archive
```

Stop everything:

```bash
docker compose down
```

## Notes

- PostgreSQL data is stored in the `postgres_data` volume.
- Archived files are stored in `./output`.
- `blacklist.txt` is mounted to `/app/blacklist.txt` in the archive container.
