# ORM query patterns: conditional, project-first examples

These snippets illustrate questions to ask, not defaults to impose. Check installed provider/version, generated query and existing conventions before copying.

## C# / EF Core: projection and materialization boundary

```csharp
// Example: read-only listing; assumes the caller does not need tracked entities.
var summaries = await db.Articles
    .AsNoTracking()
    .Where(a => a.IsPublished)
    .OrderByDescending(a => a.PublishedAt)
    .ThenByDescending(a => a.Id)
    .Select(a => new ArticleSummary(a.Id, a.Title))
    .Take(pageSize)
    .ToListAsync(cancellationToken);
```

Inspect generated SQL, provider translation, filters and whether tracking/relationship fix-up is required. Moving `.ToList()` before filtering changes the execution boundary and may have large costs.

## Python / Django: avoid per-row author fetches

```python
# Example where Article.author is a foreign key and is used for each row.
articles = (
    Article.objects
    .filter(is_published=True)
    .select_related("author")
    .order_by("-published_at", "-id")[:page_size]
)
for article in articles:
    print(article.author.display_name)
```

`select_related` is generally for single-valued relationships; inspect generated queries and whether related data is actually needed. For multi-valued relationships, different prefetch approaches may be suitable.

## TypeScript / ORM-agnostic batching

```typescript
// Conceptual: avoid one author query per article.
const articles = await store.findArticles(filter);
const authorIds = [...new Set(articles.map(a => a.authorId))];
const authors = await store.findAuthorsByIds(authorIds);
const byId = new Map(authors.map(a => [a.id, a]));
const result = articles.map(a => ({
  id: a.id,
  title: a.title,
  authorName: byId.get(a.authorId)?.displayName ?? null
}));
```

Verify ID type consistency, missing authors, ordering, data-access scope, batching parameter limits and error behavior. This is not a prescription to replace an already-efficient join.

## Cross-language lesson

A good query pattern is a result of matching *observed query behavior and consumer contracts* to the capabilities of the installed stack. Neither raw SQL, eager-loading, nor repositories are universally best.
