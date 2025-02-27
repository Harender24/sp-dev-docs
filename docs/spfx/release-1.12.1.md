---
title: SharePoint Framework v1.12.1 release notes
description: Release notes for the SharePoint Framework v1.12.1 release
ms.date: 04/16/2021
ms.prod: sharepoint
localization_priority: Priority
---
# SharePoint Framework v1.12.1 release notes

This release introduces a new property & event in the Web Part API to detect the rendering width (and changes), improved support for Microsoft Teams solutions, and updates supported versions of Node.js.

**Released:** TBD Q2, 2021

[!INCLUDE [spfx-release-candidate](../../includes/snippets/spfx-release-candidate.md)]

## Upgrading projects from v1.11.0 to v1.12.1

1. In the project's **package.json** file, identify all SPFx v1.11.0 packages. For each SPFx package:
    1. Uninstall the existing v1.11.0 package:

        ```console
        npm uninstall @microsoft/{spfx-package-name}@1.11.0
        ```

    1. Install the refreshed v1.12 {version-release} package:

        ```console
        npm install @microsoft/{spfx-package-name}@1.12.1 --save --save-exact
        ```

> [!TIP]
> The [CLI for Microsoft 365](https://aka.ms/o365cli) provides an easy step-by-step guidance to [upgrade](https://pnp.github.io/cli-microsoft365/cmd/spfx/project/project-upgrade/) your solutions to latest SharePoint Framework version.

## New features and capabilities

- The **Sync to Teams** button in the Tenant App Catalog will use the Teams app manifest defined in the solution if present to create and publish a Teams app package to Microsoft Teams. If an app manifest file is not present, SharePoint will dynamically generate one.
  - *See [Deployment options for SharePoint Framework solutions for Microsoft Teams](deployment-spfx-teams-solutions.md) for more details.*
- A new API has been added to the SPFx web part class to determine the rendered width of a web part and optionally handle an event when it changes.
  - *See [Determine the rendered web part size](web-parts/basics/determine-web-part-width.md) for more details.*
- Preliminary support for Microsoft Teams meeting apps with the SharePoint Framework - full support is pending a fix for server side regression

## Changes in this release

- Add support for **Node.js v12.13.x & v14.15.x**nvm 
  - *See [Set up your SharePoint Framework development environment](set-up-your-development-environment.md) for details.*
  - **Gulp v4** (installed globally) is required (*see [Regarding Gulp versions & Node.js v12+](#gulp-versions--nodejs-v12) for details*)
- For all projects:
  - Update the default version of TypeScript to **v3.7** (*via **@microsoft/rush-stack-compiler-3.7** v0.2.3*)
  - Update the **Gulp** version used to **v4.0.2**
- For projects that use React:
  - Update the React NPM packages (**react** & **react-dom**) to **v16.9.0**.
  - Update the Office UI Fabric React NPM package / Microsoft Fluent UI (**office-ui-fabric-react**) to **v7.156.0**.
- The default location for resources used in deployments changed from `./temp/deploy` to `./releases/assets`. For projects created prior to SPFx v1.12.1, you should update the **./config/deploy-azure-storage.json** file property `workingDir` to the new location: `"workingDir": "./release/assets/"`. For more information, see [Deploy your SharePoint client-side web part to Azure CDN: Configure Azure Storage account details](web-parts/get-started/deploy-web-part-to-cdn.md#configure-azure-storage-account-details).

## Deprecations and removed items in this release

- **Gulp v3** is not supported (*neither globally nor locally installed*) when using Node.js v12+.
- **Local workbench is deprecated** - This is the last release that will include support for the local workbench.
- This is the last release that will include a single generator that works for on-prem and SharePoint Online.  You'll still be able to create projects for on-prem, just by using the older generator.

### Gulp versions & Node.js v12+

Gulp v3 isn't supported with Node.js v12+ (*ref [gulpjs/gulp/#2324](https://github.com/gulpjs/gulp/issues/2324)*).

This is not a change with SPFx. Its mentioned here to bring attention to it as this SPFx release adds support for Node.js v12.
