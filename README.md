# Practical 7 – Student Management API (FastAPI)

A small REST API built with **FastAPI** to manage students, with request validation (Pydantic) and automated tests (pytest).

## Features

- `GET /` – health check
- `GET /students` – list all students
- `POST /students` – add a student (`201 Created`)
  - `name`: string, at least 2 characters
  - `roll_no`: string, must be unique (duplicate returns `409 Conflict`)
  - `marks`: number between 0 and 100 (otherwise `422 Unprocessable Entity`)
- `GET /students/{student_id}` – get one student (`404 Not Found` if missing)

Data is stored in an in-memory list, so it resets whenever the server restarts.

## Project structure

```
Practical-7/
├── main.py            # FastAPI app and endpoints
├── test_main.py       # pytest tests
├── requirements.txt
├── .gitignore
└── README.md
```

## Setup

```bash
python3 -m venv venv
source venv/bin/activate      # Windows: venv\Scripts\activate
pip install -r requirements.txt
```

## Run the server

```bash
uvicorn main:app --reload
```

- API: http://127.0.0.1:8000
- Interactive docs (Swagger UI): http://127.0.0.1:8000/docs

## Example requests

```bash
curl -X POST http://127.0.0.1:8000/students \
  -H "Content-Type: application/json" \
  -d '{"name": "Aarav", "roll_no": "MCA101", "marks": 85}'

curl http://127.0.0.1:8000/students
curl http://127.0.0.1:8000/students/1
```

## Run the tests

```bash
pytest -v
```
