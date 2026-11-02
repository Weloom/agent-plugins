# Weloom agent plugins

A repository-backed marketplace containing `ss-md-dotnet-engineering`: eight opinionated skills for C# and .NET engineering.

## Install

### GitHub Copilot app

Open **Customize**, use the marketplace settings control to add:

```text
https://github.com/Weloom/agent-plugins
```

Find `ss-md-dotnet-engineering` in **Browse**, install it, confirm it is enabled under **Installed**, and start a fresh session.

### Copilot in VS Code

Run **Chat: Manage Plugin Marketplaces > Add Marketplace...**, add the repository URL above, and install the plugin from **Customize > Browse**.

### GitHub Copilot CLI

```powershell
copilot plugin marketplace add Weloom/agent-plugins
copilot plugin install ss-md-dotnet-engineering@weloom-agent-plugins
```

Marketplace name: `weloom-agent-plugins`.

Do not enable overlapping local and repository-hosted copies simultaneously. Marketplace registration makes the package discoverable; installation and enablement are separate actions.

## Included skills

- `domain-guided-development`
- `dotnet-architecture`
- `refactoring-guidance`
- `performance-review`
- `functional-csharp`
- `clean-code-guidance`
- `clean-comments`
- `normalize-whitespace`

Skill descriptions define their intended activation. Comment cleanup and whitespace normalization require explicit invocation. Clients may namespace skill names by plugin.

## Compatibility and limits

The package uses Agent Plugins 1.0, with shared skill content and Copilot-specific C# instructions. Local package installation and skill loading have been verified in the GitHub Copilot app; this Git-hosted distribution still needs client installation testing.

Claude Code uses different plugin manifests and marketplace discovery. This release does not provide Claude Code packaging or claim verified Claude compatibility. Visual Studio plugin installation is not supported by this package.

The plugin supplies guidance, not deterministic enforcement. It does not configure editor settings, install formatters, or provide MCP servers. Project instructions and verification requirements still apply.

## Maintenance

Edit the shared skill files and references together. Keep each skill's local links within its directory. Match the plugin manifest's identity, description, and version in the marketplace catalog before publishing an update.

The guidance draws on engineering concepts described in the literature named in the manifest. No source books or PDFs are included. No third-party endorsement is implied.
