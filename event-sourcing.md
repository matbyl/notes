# Event-sourcing
A way to store data in an immutable audit log that is typically interpreted and projected into a domain model.

I seems common that the event stream is abstracted on the database level, e.g. in PostgreSQL:

```postgresql
CREATE TABLE event {
    id          SERIAL      PRIMARY_KEY,
    stream_id   BIGINT      NOT NULL,
    version     BIGINT      NOT NULL,
    data        JSONB       NOT NULL,
    UNQUE (stream_id, version)
}```
