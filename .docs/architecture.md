# Architecture

The framework organizes a project into scopes. A project scope holds project-wide context and rules;
component scopes hold everything specific to one component. Each scope has exactly one canonical
entry point, and its documentation lives with it.

```text
Project
│
├── Repository
│      │
│      └── .docs
│
├── Assets
│
└── Other Components
```

Components point upward to the project scope rather than restating project-wide rules. A component
may specialize what the project scope defines, but never contradict it.
