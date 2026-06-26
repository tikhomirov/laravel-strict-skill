# Laravel Strict — Claude Skill

A Claude Code skill for reviewing and improving PHP/Laravel code based on:

- **[`nunomaduro/essentials`](https://github.com/nunomaduro/essentials)** — strict models, auto eager loading, immutable dates, fake sleep, prevent stray requests, opinionated pint/rector configs.
- **[`nunomaduro/larastan`](https://github.com/nunomaduro/larastan)** — PHPStan generics for Eloquent relations.
- **[Dandy Style](https://github.com/rwsite/dandy-style)** — practical readability over architecture religion.
- **Laravel core team practices** — `#[Scope]` attribute, enum cast, actions pattern.
- **Livewire security** — `#[Locked]`, `boot()` vs `mount()`, `AuthorizationException` handling.

The skill is structured like [Dandy Style](https://github.com/rwsite/dandy-style): a small `SKILL.md` with principles, a `recipe-map.md` to navigate by smell, a `source-map.md` to trace each recipe to its origin, and 28 compact recipes in `recipes/`.

## Install

### Global install (recommended)

```bash
git clone https://github.com/tikhomirov/laravel-strict-skill.git \
  ~/.agents/skills/laravel-strict

# Add symlink for Claude Code
ln -s ../../.agents/skills/laravel-strict \
  ~/.claude/skills/laravel-strict
```

### Per-project install

```bash
git clone https://github.com/tikhomirov/laravel-strict-skill.git \
  .agents/skills/laravel-strict
```

## Usage

### Direct invocation

```
/laravel-strict
```

Runs a 5-minute shallow scan of the project and returns 3–5 likely improvement areas. See `quick-audit.md` for the workflow.

### Contextual invocation

Mention the skill inside another task:

> "Review this Livewire component for security using laravel-strict."

The agent picks the matching recipes from `recipe-map.md` and applies them.

## Structure

```
laravel-strict/
├── SKILL.md              ← principles, invocation modes, working formula
├── recipe-map.md         ← smell → recipe
├── source-map.md         ← source → recipe (essentials / larastan / dandy / livewire)
├── 16-point-checklist.md ← audit backbone (13 essentials + 3 livewire)
├── quick-audit.md        ← 5-minute shallow scan workflow
└── recipes/              ← 28 compact recipes (700B–2.5K each)
    ├── strict-models.md
    ├── auto-eager-load.md
    ├── unguard.md
    ├── immutable-dates.md
    ├── force-https.md
    ├── safe-console.md
    ├── asset-prefetch.md
    ├── prevent-stray-requests.md
    ├── fake-sleep.md
    ├── password-defaults.md
    ├── make-action.md
    ├── pint-config.md
    ├── rector-config.md
    ├── final-readonly.md
    ├── scope-attrs.md
    ├── phpdoc-generics.md
    ├── enums-cast.md
    ├── actions-pattern.md
    ├── query-builder.md
    ├── pest-migration.md
    ├── detect-n-plus-one.md
    ├── audit-passwords.md
    ├── audit-mass-assignment.md
    ├── lw-locked.md
    ├── lw-boot-vs-mount.md
    ├── lw-authorization-exception.md
    ├── lw-ownership-scope.md
    └── lw-audit.md
```

## Core principle

> Do not look for code to fit a recipe. First find a real problem. Then choose the smallest set of recipes that solves it.

**Working formula:** *Project first. Pain second. Recipe third. Small safe action last.*

When in doubt: do less, but verify with `make ci-fix && make ci` (or your project's equivalent).

## Loading limits

- **Contextual mode** — load at most 1–3 recipes.
- **Review mode** — load `recipe-map.md`, then recipes after detecting smells.
- **Commit mode** — inspect changed files first, load the recipe that matches the smell.
- **Never** load all recipes "just in case".

## Contributing

1. Find a real smell in the wild.
2. Add a recipe under `recipes/` using the existing structure (Source / Problem / Bad signs / How to fix / Before / After / When not / Related).
3. Register it in `recipe-map.md` and `source-map.md`.
4. If it covers a new domain, update `16-point-checklist.md` and bump the score denominator.
5. Keep recipes under 2.5 KB.

## Credits

- Nuno Maduro — [`nunomaduro/essentials`](https://github.com/nunomaduro/essentials), [`nunomaduro/larastan`](https://github.com/nunomaduro/larastan)
- Dandy Code community — Dandy Style book and skill design
- Laravel core team — `#[Scope]`, enum cast, action patterns
- Livewire security article — <https://rwsite.ru/livewire-i-bezopasnost-tri-uyazvimosti-kotorye-legko-propustit/>

## License

MIT.