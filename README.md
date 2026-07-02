# internal-icons

Static host for the [Bitwarden Custom Icon Service URL](https://bitwarden.com/help/self-host-icon-server/) client setting.
Serves `<domain>/icon.png` per request so Bitwarden entries render a chosen icon instead of the generic globe placeholder.

## Served URL

```
https://tw1stedsister.github.io/internal-icons/
```

Each domain gets its own subpath: `https://tw1stedsister.github.io/internal-icons/<domain>/icon.png`.

## Layout

```
internal-icons/
├── .nojekyll                  — disables Jekyll, files served as-is
├── example.com/
│   └── icon.png               — health-check placeholder
├── ff-a.local/                — add domains as needed
│   └── icon.png
├── db-a.local/
│   └── icon.png
└── ...
```

## Adding a new icon

1. Pick a fake domain name for the Bitwarden entry (e.g. `ff-a.local`, `pbi-a.internal`). Prefer abstract names that do not reveal internal system architecture — this repo is public.
2. Create matching folder: `mkdir <domain>`.
3. Put a PNG icon inside as exactly `icon.png` (16x16 to 128x128 recommended, transparent PNG preferred).
4. `git add . && git commit -m "add <domain> icon" && git push`.
5. In the Bitwarden entry, set URI to `https://<domain>` (matching the folder name).
6. Bitwarden client fetches `https://tw1stedsister.github.io/internal-icons/<domain>/icon.png`.

## Configuring Bitwarden

Bitwarden client (browser extension / desktop / mobile / web vault):

Settings → Options → **Custom Icon Service URL**:

```
https://tw1stedsister.github.io/internal-icons
```

Then restart the client or clear the icon cache. Entries whose URI matches a folder in this repo will render the custom icon.

## Notes

- Jekyll is disabled via `.nojekyll` so filenames starting with `_` or `.` are served as-is.
- Repo is public because GitHub Pages requires public repositories on the free tier. Use abstract fake domains for folder names — do not leak real hostnames of internal systems.
- Related tooling-improvement item: `TI-021` in `context-maintenance/context-engineering/context_pack/tooling_improvement_backlog.md`.
