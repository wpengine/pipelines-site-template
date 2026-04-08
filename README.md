# WP Engine Pipelines WordPress Starter

A template repository for building WordPress sites with WP Engine Pipelines.

## Overview

This repository provides a starting point for WordPress development with WP Engine Pipelines. It follows the **wp-content structure pattern** where you commit only your custom themes, plugins, and mu-plugins. WordPress core and platform dependencies are handled automatically by the build process in your WP Engine pipeline.

## Prerequisites

- [Composer](https://getcomposer.org/) installed locally

## Quick Start

1. Click **"Use this template"** to create your repository
2. Clone your new repository locally
3. Run `composer install` to download the starter theme
4. Add your plugins and themes (via Composer or manually)
5. Commit all files, including installed dependencies
6. Push to trigger a build

> **Note:** Remove `.github/CODEOWNERS` after creating your repo — it's used for template maintenance and isn't needed in your project.

## Repository Structure

```
├── plugins/          # Your WordPress plugins
├── themes/           # Your WordPress themes (required)
├── mu-plugins/       # Your must-use plugins
├── composer.json     # Dependency management
└── composer.lock     # Locked dependency versions
```

## Requirements

### Themes (Required)

At least one valid WordPress theme must be present in the `themes/` directory. The default TwentyTwentyFive theme is included via Composer.

### Plugins (Optional)

Place WordPress plugins in the `plugins/` directory, or install via Composer.

### Must-Use Plugins (Optional)

Place mu-plugins in the `mu-plugins/` directory. WP Engine's required mu-plugins are automatically installed during the pipeline's build process.

## What NOT to Include

The following are managed by WP Engine and should NOT be committed:

- WordPress Core (`wp-admin/`, `wp-includes/`, etc.)
- `wp-config.php`
- `uploads/`
- Object cache drop-in (`object-cache.php`)
- WP Engine mu-plugins

## Using Composer

This template uses [WPackagist](https://wpackagist.org/) to install plugins and themes from WordPress.org.

### Installing Dependencies

```bash
composer install
```

### Adding a Plugin

```bash
composer require wpackagist-plugin/plugin-name
```

### Adding a Theme

```bash
composer require wpackagist-theme/theme-name
```

### Important: Commit Dependencies

The pipeline's build process does **not** run `composer install`. You must commit all installed files (themes, plugins) to your repository. Use Composer for local dependency management, then commit the results.

## Local Development

For local development, you need a separate WordPress installation. This repository provides only wp-content files.

Recommended options:
- [Local by WP Engine](https://localwp.com/)
- Docker with a WordPress image
- Standard LAMP/LEMP stack

Symlink or copy this repository's directories into your local WordPress `wp-content/`.

## The WP Engine Pipeline

The following occurs when you push to a repository once you have configured a pipeline for it in the WP Engine User Portal:

1. The pipeline clones your code.
2. WP Engine's required plugins and mu-plugins are merged with your themes, plugins, and mu-plugins. WP Engine requirements overwrite committed code when paths conflict.
3. The pipeline packages the bundled code.
4. The package is deployed.

## Troubleshooting

### Push fails with HTTP 400 error

If your first push fails with an error like:

```text
error: RPC failed; HTTP 400 curl 22 The requested URL returned error: 400
fatal: the remote end hung up unexpectedly
```

This typically occurs when pushing large initial commits (themes with fonts/images). Increase Git's HTTP buffer size:

```bash
git config http.postBuffer 524288000
```

Then retry your push.

## License

MIT License - see [LICENSE](LICENSE) for details.
