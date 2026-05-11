---
title: Install DevRev CLI
type: developer-doc
status: stable
source: developer.devrev.ai
category: snapin-development
source_url: https://developer.devrev.ai/snapin-development/references/cli-install
last_updated: 2026-05-11
summary: "The DevRev CLI is a command-line interface tool that simplifies working with the DevRev REST APIs."
---

# Install DevRev CLI

References

# Install DevRev CLI

The DevRev CLI is a command-line interface tool that simplifies working with the DevRev REST APIs.

The installation of the DevRev CLI via Homebrew (for MAC), dpkg (for Linux) is no longer supported.

If you have previously installed the DevRev CLI using these deprecated methods, you must uninstall the earlier version then reinstall with the current version.

```
sudo dpkg -r devrev
```

```
brew uninstall devrev
```

## [Install the DevRev CLI](#install-the-devrev-cli)

Install using npm:

```
npm install -g devrev
```

This installs the DevRev CLI globally, making it available from any directory.

Supported architecture: Windows amd64

## [Install](#install)

1. Download the [Windows executable](https://github.com/devrev/cli/releases/latest).
2. Unzip the downloaded file and add the path to the environment variable.
3. Add the directory to the system PATH variable under **System Properties** > **This PC** > **Properties**.
4. In the System window, click **Advanced system settings** > **Environment Variables** > **Path** > **Edit**.
5. In the **Edit environment variable** window, click **New**. Enter the path to the directory you want to add. For example: `C:\Program Files\devrev\`.
6. Click **OK** to save the changes. Close all remaining windows by clicking **OK**.

You may need to restart your computer for the changes to take effect.

Upon completion of the installation, confirm its success by checking the version of the DevRev CLI.

```
devrev --version
```

This command presents the currently installed version of the DevRev CLI, thereby verifying its successful installation.

## [Uninstall the DevRev CLI](#uninstall-the-devrev-cli)

Uninstall using npm:

```
npm uninstall -g devrev
```

1. Remove the path from the environment variable.
2. Delete the downloaded executable file and its folder.

Last updated on

[Snap-in triggered by an external source

Previous Page](/snapin-development/tutorials/triggered-external-source)[DevRev CLI reference

Next Page](/snapin-development/references/cli)

## Source
- DevRev developer docs: [Install DevRev CLI](https://developer.devrev.ai/snapin-development/references/cli-install)
