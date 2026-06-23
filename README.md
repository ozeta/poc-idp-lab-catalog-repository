# poc-idp-lab-catalog-repository

Source of truth for the Backstage catalog in the IDP lab.

This repository contains:

- Catalog bootstrap and entity data under `catalog/`
- Software templates under `templates/`
- Template content files used by Backstage Scaffolder

Backstage is configured to ingest this repo starting from:

- `catalog/locations.yaml`

## How Backstage Reads This Repository

Backstage points to this URL:

- `https://github.com/HylandSandbox/poc-idp-lab-catalog-repository/blob/hyland-sandbox/catalog/locations.yaml`

The bootstrap location then references all catalog data and templates in this repo.

## Repository Structure

```text
catalog/
	locations.yaml
	entities.yaml
	org.yaml
	shopping-platform/
		shopping-platform.yaml
		(entity YAML files per component)
docs/
	index.md
	catalog.md
	structure.md
	templates.md
	troubleshooting.md
templates/
	repo-template/
		template.yaml
		content/
			catalog-info.yaml
			CODEOWNERS
			README.md
	csharp-repo-template/
		template.yaml
		content/
			catalog-info.yaml
			CODEOWNERS
			readme.md
	python-repo-template/
		template.yaml
		content/
			catalog-info.yaml
			CODEOWNERS
			mkdocs.yml
			README.md
			docs/
	group-test-template/
		template.yaml
		content/
			catalog-info.yaml
			CODEOWNERS
			README.md
```

## Catalog Bootstrap

Current bootstrap file:

- `catalog/locations.yaml`

It references:

- `./entities.yaml`
- `./shopping-platform/shopping-platform.yaml`
- `./org.yaml`
- `../templates/repo-template/template.yaml`
- `../templates/csharp-repo-template/template.yaml`
- `../templates/python-repo-template/template.yaml`
- `../templates/group-test-template/template.yaml`
- `../catalog-info.yaml`

Important: paths in `catalog/locations.yaml` are relative to `catalog/`, so do not prefix with `catalog/` again.

## Allowed Entity Kinds

Backstage must allow these kinds for this location:

- `Component`
- `System`
- `API`
- `Resource`
- `Location`
- `User`
- `Group`
- `Template`

If `User`, `Group`, or `Template` are not allowed, ingestion warnings will appear and those entities will be skipped.

## Branching and Target Branch

The catalog branch is selected in the Backstage location URL itself.

The POC currently reads from the `hyland-sandbox` branch.

Example:

- hyland-sandbox branch: `.../blob/hyland-sandbox/catalog/locations.yaml`
- Main branch: `.../blob/main/catalog/locations.yaml`
- Feature branch: `.../blob/feature/my-branch/catalog/locations.yaml`

`catalog.import.pullRequestBranchName` is unrelated to ingestion target branch. It is only used when Backstage creates import PRs.

## Templates Included

### 1) New Repository with README

- Template file: `templates/repo-template/template.yaml`
- Creates a GitHub repository under the **HylandSandbox** organization
- Adds `README.md`, `CODEOWNERS`, and `catalog-info.yaml`
- Registers the new component in Backstage via `catalog:register`

### 2) New C# Repository Foundation

- Template file: `templates/csharp-repo-template/template.yaml`
- Creates a GitHub repository under the **HylandSandbox** organization for C# projects
- Adds governance and starter files
- Registers the new component in Backstage via `catalog:register`

### 3) New Python Repository Foundation

- Template file: `templates/python-repo-template/template.yaml`
- Creates a GitHub repository for Python projects with TechDocs, engineering governance, and repo standards files
- Adds `README.md`, `CODEOWNERS`, `mkdocs.yml`, `catalog-info.yaml`, and a starter `docs/` folder
- Registers the new component in Backstage via `catalog:register`

### 4) New Group Test Repository

- Template file: `templates/group-test-template/template.yaml`
- Creates a GitHub repository for group testing under the **HylandSandbox** organization
- Adds `README.md`, `CODEOWNERS`, and `catalog-info.yaml`
- Registers the new component in Backstage via `catalog:register`

1. Edit files under `catalog/` and/or `templates/`.
2. Open a pull request.
3. Merge to the branch used by Backstage.
4. Backstage refreshes and ingests updated entities.

## Troubleshooting

### Warning: no matching files found with duplicated path

Example:

- `.../catalog/catalog/entities.yaml`

Cause:

- Wrong relative target in `catalog/locations.yaml`.

Fix:

- Use `./entities.yaml`, not `./catalog/entities.yaml`.

### Warning: entity is not of an allowed kind

Example:

- `Entity user:default/guest ... is not of an allowed kind`

Cause:

- Backstage `catalog.rules` does not include `User`/`Group`/`Template`.

Fix:

- Add missing kinds in Backstage config rules.

## Notes

- Keep entity references consistent (`owner`, `system`, etc.).
- Prefer small and reviewable PRs for catalog changes.
- Treat this repo as platform-critical configuration.
