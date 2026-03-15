# SiteRedirect

![PHP](https://img.shields.io/badge/PHP-7%2B-777BB4?logo=php&logoColor=white)
![License](https://img.shields.io/badge/License-Unlicense-green)

Read in Portuguese: [README.pt-BR.md](README.pt-BR.md)

> **New version:** Redirect with access analytics in Google Firebase → [**SiteRedirect2**](https://github.com/dmslabsbr/SiteRedirect2)

---

**SiteRedirect** is a minimal URL redirect service for your web server. Define short aliases (e.g. `amazon`, `uber`) in a config file; visitors hit `yoursite.com/alias` and are sent to the target URL. No database—just PHP and Apache rewrite rules.

## Description

- One config file holds all alias → URL mappings.
- Apache (or compatible) rewrites clean paths like `/amazon` to `redir.php?go=amazon`.
- Optional debug view lists all aliases (protected by a special code).
- Fallback: requests without a valid alias can show a custom `index.html`.

## Install

1. Clone or copy this repo into the **document root** of your web server (Apache with `mod_rewrite` enabled).
2. Rename `htaccess` to `.htaccess`.
3. Edit `vai.php` and add or change your alias → URL entries.

## Files

| File | Purpose |
|------|--------|
| `vai.php` | Alias → URL map; edit this to add or change redirects. |
| `redir.php` | Main script: reads `vai.php`, sends `Location` header for matching alias. |
| `htaccess` | Rename to `.htaccess` so the server routes requests to `redir.php`. |
| `index.html` | Shown when the user requests the root or an unknown path (customize as needed). |

## Usage

- **Redirect:** `https://yourdomain.com/amazon` → redirects to the URL defined for `amazon` in `vai.php`.
- **Debug list:** `https://yourdomain.com/amazon?go=specialCode` (or the path you use for the special code in `redir.php`) lists all aliases and URLs.

## Config

- **Aliases:** Edit the `$vai` array in `vai.php`. Keys are aliases (lowercase in the script), values are full destination URLs.
- **Rewrite rules:** In `.htaccess` (from `htaccess`), the first rule sends `/{alias}` to `redir.php?go={alias}`. Adjust rules if your server or path layout differs.

## License

This project does not ship a license file; use and modify at your own discretion. The badge above is set to "Unlicense" as a generic placeholder until a license is chosen.
