# TYPO3 Demo Project

This is a demonstration project used to show [DDEV](https://ddev.com/) features with TYPO3,
particularly `ddev share` and Git worktrees. It's based on the official Camino theme with TYPO3 CMS Base Distribution, but
this README documents the demo-specific setup rather than upstream TYPO3 usage.

## Related blog posts

* [DDEV Share with TYPO3](https://ddev.com/blog/ddev-share-with-typo3)
* [Git Worktree with TYPO3](https://ddev.com/blog/git-worktree-with-typo3)

## Notable configuration

* [config/sites/camino/config.yaml](config/sites/camino/config.yaml) uses `path: /` instead of
  `path: /camino`, and its `base` has no URL (just `/`), so the site works whether it's the only
  site on the project or is being shared under a dynamically generated URL.
* [.ddev/config.yaml](.ddev/config.yaml) defines `pre-share` and `post-share` hooks that rewrite
  the `base` (if needed) in each site's `config.yaml` to match the temporary share URL, then restore the
  original values afterward. This is what makes `ddev share` work cleanly with TYPO3's
  multi-site configuration.
* A `post-start` hook runs `composer install` automatically, so a fresh checkout (or new
  worktree) is ready to go as soon as `ddev start` finishes.

## Usage

* `ddev start`
* Use `ddev composer` instead of a locally installed `composer` for any Composer commands, so
  dependencies are installed with the PHP version and extensions configured in the DDEV
  container.

## License

GPL-2.0 or later
