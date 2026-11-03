# TypeScript examples — general-purpose, illustrative

These snippets are independent fragments, not a complete Angular or Node.js application.

## SRP — validation and transport are separate concerns

```typescript
export function isValidUsername(value: string): boolean {
  return /^[a-z0-9_]{3,20}$/i.test(value);
}
```

A UI component can call this pure validation rule while an API client handles transport. Do not split them into separate services unless the boundary is useful.

## OCP — real exporters can share a meaningful contract

```typescript
interface Formatter { format(lines: string[]): string; }
const plainText: Formatter = { format: lines => lines.join('\n') };
const markdownList: Formatter = {
  format: lines => lines.map(line => `- ${line}`).join('\n')
};
```

Prefer an explicit conditional for a small stable set. Avoid factories and registries until they solve a demonstrated problem.

## LSP — structural compatibility is not behavioral compatibility

```typescript
interface NameFormatter {
  // Contract: accepts any string, including empty strings.
  format(value: string): string;
}
const badFormatter: NameFormatter = {
  format(value) {
    if (!value) throw new Error('Empty value'); // Breaks stated contract.
    return value.trim();
  }
};
```

The type checker won't detect a behavioral contract violation. Test the promised edge cases.

## ISP — focused interfaces for distinct consumers

```typescript
type Article = { id: string; title: string };
interface ArticleReader { getById(id: string): Promise<Article | null>; }
interface ArticleWriter { save(article: Article): Promise<void>; }
```

A read-only view shouldn't need a mutation contract when it doesn't use one.

## DIP — isolate an external storage boundary

```typescript
interface PreferencesStore { load(): Promise<string | null>; }
class ThemeService {
  constructor(private readonly store: PreferencesStore) {}
  loadTheme() { return this.store.load(); }
}
```

Dependency injection can provide an implementation, but creating an interface for a stable pure calculation is not automatically beneficial.
