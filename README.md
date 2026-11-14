# Kiss Goodnight

Finish the day with your work saved, unused development tools stopped, and a short note for tomorrow.

Kiss Goodnight is a Codex skill for the servers, previews, simulators, and background jobs left over from development work. It uses the tools and permissions available in your Codex session to identify what belongs to finished work, stop it gracefully, and verify the result. Its instructions guide Codex's decisions, so results depend on the model, the available evidence, and access to your machine.

## Install

Download or clone this repository, then copy its folder into a Codex skills directory. Name the copied folder `kiss-goodnight`, with `SKILL.md` directly inside it.

| Scope | Location |
| --- | --- |
| All projects | `.agents/skills/kiss-goodnight` inside your home directory |
| One project | `.agents/skills/kiss-goodnight` inside that project |

On Windows, your home directory is normally `%USERPROFILE%`. On macOS and Linux it is `~`. Codex detects installed skills automatically. Restart Codex if it does not appear. [Codex skills documentation](https://developers.openai.com/codex/skills)

## Use

Start with a preview of the cleanup.

```text
$kiss-goodnight check only
```

When you are ready to clean up, invoke the skill.

```text
$kiss-goodnight
```

You can also name a project, protect a resource you still need, or wait for a job.

```text
$kiss-goodnight for this project, keep the preview on port 3000 running
$kiss-goodnight after the screenshots finish
```

Keep the Codex session running while it waits and cleans up. The resulting handoff tells you what stopped, what is still running, and what needs attention before you quit Codex or power off.

## Cleanup decisions

- Development servers, preview servers, simulators, watchers, and automation browsers qualify when Codex can link them to finished work and establish that they are no longer needed.
- Active jobs, previews still needed for review, shared services, and uncertain processes stay running. Check-only requests produce a report.
- Stopping a resource requires a fresh check of its identity and dependencies. A reused process ID or newly started task changes the decision.
- Source changes, generated files, caches, databases, and volumes are preserved. Cloud changes, Git writes, and shutting down the computer need a separate request.
- The handoff stays in the chat by default, with relevant outputs, pending reviews, and a next step. Sensitive command arguments and credentials are omitted.

## Compatibility and validation

Use a Codex session with tools that can inspect and control the machine where your work runs. A remote container may have a different process list from your laptop. Visibility into other chats varies by Codex surface and available integrations. The skill reports what it cannot verify.

Validation includes skill discovery on macOS, an independent review of the behavioral scenarios in [tests/scenarios.md](tests/scenarios.md), and a macOS test with two disposable local servers. Check-only preserved both servers. Cleanup stopped the finished task's server, kept the active server running, and preserved both saved output files.

Linux and Windows guidance is included, but live cleanup on those systems remains untested. No additional plugin or executable helper is required by the skill.

## Reporting an issue

Include your operating system, Codex surface, the request you made, and what happened. Redact credentials, private URLs, and personal paths from logs or command lines before posting them. For cleanup bugs, include whether the process belonged to an active task or was shared with another project.

## License

Licensed under the [MIT License](LICENSE).
