# C# examples — general-purpose, illustrative

These independent snippets demonstrate choices, not a complete runnable application. No business-specific frameworks or internal code are assumed.

## SRP — parsing and notifications change for different reasons

**Problem:** An import operation both parses records and sends notifications, forcing the same component to change for unrelated policies.

```csharp
// Conceptual anti-example: responsibilities are coupled.
public sealed class CsvImportService
{
    public void Import(string csv)
    {
        // ParseCsv(csv);
        // SaveRecords(...);
        // SendNotification(...);
    }
}
```

**Focused alternative:** Isolate reusable parsing logic; keep orchestration where workflow decisions belong.

```csharp
public static class CsvParser
{
    public static string[] ParseLines(string csv) =>
        csv.Split('\n', StringSplitOptions.RemoveEmptyEntries);
}
```

A separate orchestration component can call the parser, existing persistence mechanisms, and notification facility. Splitting is useful only if the policies genuinely change independently; it is not a rule to create one class per line.

## OCP — extend only for real variation

```csharp
public interface ITextExporter
{
    string Export(IEnumerable<string> lines);
}
public sealed class PlainTextExporter : ITextExporter
{
    public string Export(IEnumerable<string> lines) => string.Join("\n", lines);
}
public sealed class CsvTextExporter : ITextExporter
{
    public string Export(IEnumerable<string> lines) =>
        string.Join("\n", lines.Select(s => "\"" + s.Replace("\"", "\"\"") + "\""));
}
```

This seam can help when multiple formats are actively maintained. A short switch is often better for a closed, stable set. The snippet illustrates variation, not a production-grade CSV specification.

## LSP — preserve the published contract

```csharp
public interface INameFormatter
{
    // Contract: accepts null or empty strings and returns a non-null string.
    string Format(string? name);
}
public sealed class StrictNameFormatter : INameFormatter
{
    // BAD: rejects input expressly allowed by the contract.
    public string Format(string? name) =>
        name is null ? throw new ArgumentNullException(nameof(name)) : name.Trim();
}
```

Fix by supporting the promised input or defining a distinct contract. Verify all valid input classes, not just the happy path.

## ISP — clients should depend only on what they need

```csharp
public sealed record Article(int Id, string Title);
public interface IArticleReader
{
    Article? GetById(int id);
}
public interface IArticleWriter
{
    void Save(Article article);
}
```

Split only where read-only and write consumers are genuinely distinct, not by reflex.

## DIP — isolate external details at an actual boundary

```csharp
public interface IArticleStore
{
    Article? Find(int id);
}
public sealed class ArticleDisplayService
{
    private readonly IArticleStore store;
    public ArticleDisplayService(IArticleStore store) => this.store = store;
    public string TitleFor(int id) => store.Find(id)?.Title ?? "Not found";
}
```

The abstraction is useful when storage is an external detail with a meaningful change or test boundary. Don't create an interface for every pure helper.
