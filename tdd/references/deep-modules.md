# Deep Modules

From "A Philosophy of Software Design":

Deep modules have a small interface and substantial implementation behind it.

```text
┌─────────────────────┐
│   Small Interface   │
├─────────────────────┤
│                     │
│  Deep Implementation│
│                     │
└─────────────────────┘
```

Shallow modules expose a large surface area with little value behind it.

```text
┌─────────────────────────────────┐
│       Large Interface           │
├─────────────────────────────────┤
│  Thin Implementation            │
└─────────────────────────────────┘
```

When designing an interface, ask:

- Can the number of methods be reduced?
- Can parameters be simplified?
- Can more complexity be hidden inside the module?
