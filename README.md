# medicore-patient-service

Patient profile service for the **MediCore** healthcare platform
([monorepo](https://github.com/Vamshikrishna720/medicore)).

## Highlights

- Profile CRUD scoped to the JWT identity (`X-User-Id` / `CurrentUser`) — patients only ever touch their own data; ADMIN can list and soft-delete
- **Soft delete** (`active` + `deactivatedAt`) — medical history is retained for compliance
- JPQL pagination, unique index on `user_id`, profile fields incl. blood group, allergies, chronic conditions
- `/internal/patients/by-user/{userId}` Feign endpoint for appointment-service

## Endpoints (via gateway, `/api`)

| Method | Path | Access |
|---|---|---|
| POST/GET/PUT | `/patients/me` | PATIENT |
| GET | `/patients` (paged) | ADMIN |
| GET | `/patients/{id}` | ADMIN or owning PATIENT |
| PATCH | `/patients/{id}/status?active=` | ADMIN |
| GET | `/internal/patients/by-user/{userId}` | internal token |

## Run

```bash
mvn spring-boot:run          # :8082 (needs MySQL + Eureka)
```

Swagger: `http://localhost:8082/swagger-ui/index.html`
