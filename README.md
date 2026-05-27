<p align="center">
  <a href="https://github.com/akaUNik/confluence-markdown-exporter"><img src="logo.png" alt="confluence-markdown-exporter"></a>
</p>
<p align="center">
    <em>Export Confluence pages, page trees, spaces, or whole organizations to Markdown for Obsidian, Gollum, Azure DevOps (ADO), Foam, Dendron and more.</em>
</p>
<p align="center">
  <a href="https://github.com/akaUNik/confluence-markdown-exporter/actions/workflows/python-build.yml"><img src="https://github.com/akaUNik/confluence-markdown-exporter/actions/workflows/python-build.yml/badge.svg" alt="Build Python package"></a>
  <a href="https://github.com/akaUNik/confluence-markdown-exporter/actions/workflows/release.yml"><img src="https://github.com/akaUNik/confluence-markdown-exporter/actions/workflows/release.yml/badge.svg" alt="Build and publish to PyPI"></a>
  <a href="https://pypi.org/project/confluence-markdown-exporter" target="_blank">
    <img src="https://img.shields.io/pypi/v/confluence-markdown-exporter?color=%2334D058&label=PyPI%20package" alt="PyPI version">
   </a>
  <a href="https://hub.docker.com/r/spenhouet/confluence-markdown-exporter" target="_blank">
    <img src="https://img.shields.io/docker/v/spenhouet/confluence-markdown-exporter?sort=semver&label=Docker%20Hub&color=2496ED&logo=docker&logoColor=white" alt="Docker Hub version">
   </a>
  <a href="https://spenhouet.github.io/confluence-markdown-exporter/" target="_blank">
    <img src="https://img.shields.io/badge/docs-online-blue" alt="Documentation">
   </a>
</p>

## What it does

Exports individual pages, pages with descendants, entire Confluence spaces, or every space in an organization via the Atlassian API into clean Markdown. Skips unchanged pages by default, re-exporting only what has changed since the last run.

Supported targets include Obsidian, Gollum, Azure DevOps (ADO) wikis, Foam, Dendron, and anything else that consumes Markdown.

Highlights:

- Confluence Cloud, Server, and Data Center URL formats
- Markdown export for rich text, tables, links, images, attachments, task lists, panels, status badges, labels, and page metadata
- Optional sidecar export for open inline and page comments
- Page Properties and Page Properties Report conversion for plain Markdown, YAML front matter, Obsidian Dataview, or Meta Bind workflows
- draw.io, PlantUML, and Markdown Extensions macro support
- Configurable paths, filenames, attachment handling, link style, cleanup, retries, and target-system presets
- Atlassian API token, PAT, scoped-token Cloud gateway, and per-instance client / CA certificate configuration

Full feature list, configuration reference, and target-system presets live in the **[documentation site](https://spenhouet.github.io/confluence-markdown-exporter/)**.

## Quickstart

### 1. Install

**macOS and Linux**

```bash
curl -LsSf uvx.sh/confluence-markdown-exporter/install.sh | sh
```

**Windows**

```powershell
powershell -ExecutionPolicy ByPass -c "irm https://uvx.sh/confluence-markdown-exporter/install.ps1 | iex"
```

Installing a specific version:

```bash
curl -LsSf uvx.sh/confluence-markdown-exporter/5.1.1/install.sh | sh
```

Alternative install methods (PyPI via `pip` / `uv`, prebuilt Docker image) are covered in the [installation docs](https://spenhouet.github.io/confluence-markdown-exporter/installation) and the [Docker page](https://spenhouet.github.io/confluence-markdown-exporter/docker).

> **Using the Docker image?** Steps 2 and 3 below use the local `cme` CLI. Inside the Docker image there is no interactive `cme config` menu; you supply a pre-defined config (mounted JSON file or `CME_*` environment variables) and run a single export command per container invocation. See the [Docker page](https://spenhouet.github.io/confluence-markdown-exporter/docker) for the non-interactive flow.

Install from a local checkout:

```sh
git clone https://github.com/akaUNik/confluence-markdown-exporter.git
cd confluence-markdown-exporter
uv tool install --force .
```

For development, install it in editable mode so source changes are picked up without reinstalling:

```sh
uv tool install --editable --force .
```

### Uninstall

If you installed with the curl / PowerShell installer or `uv tool install`:

```sh
uv tool uninstall confluence-markdown-exporter
```

If you installed with `pip`:

```sh
pip uninstall confluence-markdown-exporter
```

If you used Docker:

```sh
docker image rm spenhouet/confluence-markdown-exporter
```

### 2. Authenticate

Set Confluence credentials interactively (URL, username, API token / PAT, optional certificate paths):

```sh
cme config edit auth.confluence
```

See [Authentication](https://spenhouet.github.io/confluence-markdown-exporter/configuration/authentication) for token scopes and Jira setup.

### 3. Export

```sh
# A single page
cme pages <page-url>

# A page and all its descendants
cme pages-with-descendants <page-url>

# An entire space
cme spaces <space-url>

# Every space of an organisation
cme orgs <base-url>
```

All export commands accept multiple URLs. Singular aliases are also available: `cme page`, `cme page-with-descendants`, `cme space`, and `cme org`.

Output goes to the configured `export.output_path` (current directory by default).

## Common configuration

```sh
# Open the full interactive menu
cme config

# Set common options directly
cme config set export.output_path=./output
cme config set export.page_href=wiki
cme config set export.comments_export=all

# Inspect config and diagnostics
cme config list
cme config path
cme bugreport
```

Configuration can also be overridden per session with `CME_` environment variables, for example `CME_EXPORT__OUTPUT_PATH=/tmp/export`. Authentication is URL-keyed, so use `cme config edit auth.confluence` / `auth.jira` for credentials, scoped-token Cloud IDs, and per-instance client or CA certificates.

## Documentation

The full documentation lives at **<https://spenhouet.github.io/confluence-markdown-exporter/>** and includes:

- [Installation](https://spenhouet.github.io/confluence-markdown-exporter/installation) (curl / PowerShell / pip / uv)
- [Usage guide](https://spenhouet.github.io/confluence-markdown-exporter/usage): pages, descendants, spaces, orgs, output layout
- [Feature list](https://spenhouet.github.io/confluence-markdown-exporter/features): supported Confluence content, macros, and add-ons
- [Configuration](https://spenhouet.github.io/confluence-markdown-exporter/configuration): config commands, ENV vars, full option reference
- [Target-system presets](https://spenhouet.github.io/confluence-markdown-exporter/configuration/target-systems): Obsidian, Azure DevOps, …
- [Docker](https://spenhouet.github.io/confluence-markdown-exporter/docker): prebuilt images for non-interactive / CI use
- [CI / non-interactive use](https://spenhouet.github.io/confluence-markdown-exporter/configuration/ci)
- [Compatibility](https://spenhouet.github.io/confluence-markdown-exporter/compatibility) and [Troubleshooting](https://spenhouet.github.io/confluence-markdown-exporter/troubleshooting)

## Contributing

If you would like to contribute, please read [our contribution guideline](CONTRIBUTING.md).

## License

This tool is an open source project released under the [MIT License](LICENSE).
