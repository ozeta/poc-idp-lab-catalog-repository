# Templates

## 1) New Repository with README

- File: `templates/repo-template/template.yaml`
- Creates a GitHub repository
- Adds `README.md`, `CODEOWNERS`, and `catalog-info.yaml`
- Registers the new component in Backstage via `catalog:register`

## 2) New C# Repository Foundation

- File: `templates/csharp-repo-template/template.yaml`
- Creates a GitHub repository for C# projects
- Adds governance and starter files
- Registers the new component in Backstage via `catalog:register`

## 3) New Python Repository Foundation

- File: `templates/python-repo-template/template.yaml`
- Creates a GitHub repository for Python projects
- Adds TechDocs, engineering governance, and repo standards files
- Registers the new component in Backstage via `catalog:register`

## 4) New Group Test Repository

- File: `templates/group-test-template/template.yaml`
- Creates a new GitHub repository for group testing, owned by the HylandSandbox organization
- Default CODEOWNERS set to `@HylandSandbox`
- Adds `README.md`, `CODEOWNERS`, and `catalog-info.yaml`
- Registers the new component in Backstage via `catalog:register`
