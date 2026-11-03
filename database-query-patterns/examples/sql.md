# Generic SQL examples (illustrative)

The examples use `articles`, `authors`, and `comments`; column names and syntax must be adapted to the actual database and schema.

## 1. Projection, filtering and stable ordering

```sql
-- Avoid fetching whole rows when a listing only needs a few fields.
-- Bind :author_id and :limit through the database driver (syntax varies).
SELECT a.id, a.title, a.published_at
FROM articles AS a
WHERE a.author_id = :author_id AND a.is_published = TRUE
ORDER BY a.published_at DESC, a.id DESC
LIMIT :limit;
```

Potential benefit: fewer bytes/materialized fields. Verify correct authorization and support for booleans/placeholders/`LIMIT` in the target dialect. Index candidates require an actual plan and write-cost assessment.

## 2. One-to-many join can duplicate parent rows

```sql
-- Danger if you expect one row per article:
SELECT a.id, a.title
FROM articles AS a
JOIN comments AS c ON c.article_id = a.id
WHERE c.is_approved = TRUE;
```

If the requirement is *articles with at least one approved comment*, a semi-join often matches the intended semantics:

```sql
SELECT a.id, a.title
FROM articles AS a
WHERE EXISTS (
    SELECT 1
    FROM comments AS c
    WHERE c.article_id = a.id AND c.is_approved = TRUE
);
```

Do not substitute `EXISTS` if the consumer actually needs one row per comment.

## 3. Keyset pagination (when sequential navigation is required)

```sql
-- Assumes non-null timestamps and descending (published_at, id).
-- :cursor_time and :cursor_id come from the final row of the previous page.
SELECT id, title, published_at
FROM articles
WHERE is_published = TRUE
  AND (published_at < :cursor_time
       OR (published_at = :cursor_time AND id < :cursor_id))
ORDER BY published_at DESC, id DESC
LIMIT :limit;
```

For a first page, omit the cursor predicate. Keep all original filters, ordering and access scope on every page. Handle nullable sort keys and index support explicitly; keyset does not guarantee an immutable snapshot under concurrent writes.

## 4. Transactional write example: conceptual guard

A read-then-insert uniqueness check alone is racy under concurrency. If uniqueness is required, enforce it with an actual database unique constraint and handle conflicts according to project policy. Do not add a transaction or index without reviewing deployment and existing data.
