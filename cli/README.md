# InspireSkill CLI

`inspire-skill` is the installable command-line interface and Python SDK for the Inspire compute platform. The package exposes the `inspire` executable.

```bash
python -m pip install inspire-skill
inspire --help
```

The public CLI resolves resources by name. Human-readable output and root `--json` mode expose names, aliases, readable state, and bounded collection metadata rather than internal handles. Use `--limit/-n` or `--all` where offered, and consult `inspire <group> <subcommand> --help` for command syntax.

`inspire account use <name>` sets the saved default account. Every command accepts `--account <name>` to override it for that invocation at the root, command-group, or subcommand level. Commands keep their selected account throughout execution. Switching the default account preserves each account's sessions, SSH connections, and resource caches.

Project documentation:

- [Project overview](https://github.com/realZillionX/InspireSkill/blob/main/README.md)
- [Agent Skill](https://github.com/realZillionX/InspireSkill/blob/main/SKILL.md)
- [Usage references](https://github.com/realZillionX/InspireSkill/tree/main/references)
- [Development guide](https://github.com/realZillionX/InspireSkill/blob/main/CONTRIBUTING.md)

## Python SDK

`inspire-skill` also provides synchronous (`InspireClient`) and asynchronous (`InspireAsyncClient`) Python clients, both importable directly from `inspire`. They share the same account configuration, resource models, and platform capabilities; the async client suspends at I/O boundaries and supports concurrent queries, event/log iteration, and streaming remote execution. `Accounts` provides standalone local account management. See the [Python SDK Reference](../references/sdk.md) for API details and examples.
