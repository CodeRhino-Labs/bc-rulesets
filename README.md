# CodeRhino Labs — Business Central Rulesets

This repository hosts curated ruleset files (.ruleset.json) for Microsoft Dynamics 365 Business Central (AL) development. These rulesets help teams standardize code quality by configuring the built-in AL code analyzers (CodeCop, UICop, AppSourceCop, and PerTenantExtensionCop) in a consistent, repeatable way across projects.

> Current default: `coderhino.default.ruleset.json` — a sensible baseline suitable for most Business Central extension projects.

## What’s inside

- `coderhino.default.ruleset.json` — CodeRhino’s baseline ruleset intended for general AL extension development. Start here and tailor as needed for your team or solution.
- Additional rulesets may be added over time (e.g., stricter AppSource-ready profiles, UI-focused profiles, or tenant-specific profiles).

## Ruleset format (quick reference)

Ruleset files are JSON and typically include:

- `name`: A friendly name for the ruleset
- `description`: Optional context/purpose
- `rules`: An array of rule overrides, where each entry contains at minimum:
  - `id`: Analyzer rule ID (e.g., `AA0001`, `AA0137`, etc.)
  - `action`: One of `Error`, `Warning`, `Info`, or `None`
  - `justification` (optional): Explain why this rule is overridden

Example:

```json
{
  "name": "YourProject Rules",
  "description": "Tweaks on top of the CodeRhino default baseline",
  "rules": [
    { "id": "AA0001", "action": "Warning" },
    { "id": "AA0002", "action": "None", "justification": "Legacy pattern allowed in this solution" }
  ]
}
```

Tip: Start with `coderhino.default.ruleset.json`, copy it into your repo, and only change the rules that need to differ. Keep the rationale for any relaxations or tightenings documented (in the file’s `description` and/or your repo docs).

## Choosing a ruleset

- General extension development: Use `coderhino.default.ruleset.json`.
- AppSource-bound solutions: Consider stricter severities for AppSourceCop and UICop rules.
- Per-tenant solutions: Focus on PerTenantExtensionCop and tailor rules to tenant policies.

If you need a variant that isn’t here yet, copy the default, adjust, and contribute it back as a new file.

## Contributing

- Naming: Use a clear, scoped name like `<org>.<profile>.ruleset.json` (e.g., `coderhino.appsource.ruleset.json`).
- Consistency: Prefer additive/explicit changes over broad `None` suppressions. Provide a short `description` and per-rule `justification` where helpful.
- Validate: Point an AL workspace to your ruleset via `al.ruleSetPath` and verify analyzer output before opening a PR.
- PRs: Include a brief summary explaining the intent (e.g., “stricter UI checks”, “relaxed naming for legacy objects”).

## Notes

- This repository is not affiliated with Microsoft.
- Rule IDs and availability can change with AL Language extension updates. Keep your extension up to date and adjust rulesets accordingly.
- JSON files do not support comments; prefer `description` and `justification` fields and/or this README for documentation.

---

Questions or suggestions? Open an issue or a pull request. Happy coding! 👋
