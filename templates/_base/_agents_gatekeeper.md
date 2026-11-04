# Gatekeeper policy

The owner's standing policy for the `engineering-loop` gate: `mise run loop:approvals`
reads this block (the engineering loop's SKILL.md § Settings has every key), and
loop.md § Approvals says what the seed's policy does. It is YAML: `key: value`
under a section name, a list one item per line. Quote a value that starts with
`*` or reads as another type (`no`, `on`, `1.10`). A key or section the loop
doesn't know is refused, naming it.

## Policy

```yaml
spec:
  # specs approved by policy, with no owner record; any other waits for the owner
  auto:
    - bug
    - follow-up
    - sub-issue
{% if not include_ci %}
loop:
  ci: false
{% endif %}
# practice:
#   the skill that fills a stage this project changes, one key each, such as
#   spec: brainstorming; a stage left out runs its default

risk:
  verifier: true
  paths:
    - .github/**
    - CODEOWNERS
    - docs/agents/loop.md
    - docs/agents/gatekeeper.md

# bot:
#   renovate:   # deps:renovate's routine group, run on your token: see loop.md § Approvals
#     branch: renovate/
#     paths:
#       - uv.lock
#       - package-lock.json
#       - pyproject.toml
#       - package.json
#       - mise.toml
#       - .github/workflows/*.yml
```
