# layer-wf-recorder

Wayland screen recorder for wlroots compositors, for OpenCharly desktop images.

The `wf-recorder` candy installs [wf-recorder](https://github.com/ammen99/wf-recorder),
the wlroots screen-capture recorder. It captures frames via the
`wlr-screencopy` protocol and encodes to MP4/MKV using system ffmpeg, and backs
the `record:` check verb's desktop mode on `sway-desktop`.

## What it provides

| Property | Value |
|---|---|
| Layer / candy | `wf-recorder` |
| Packages | `wf-recorder` (fedora / arch / omarchy) |
| Binary | `/usr/bin/wf-recorder` |
| Requires | `plugin-record` (the `record:` check verb) |
| Service / port | none |

## How to use it

Compose the layer by pinning this repo in a box's `candy:` list — typically
transitively through the `sway-desktop` metalayer:

```yaml
my-desktop-box:
  candy:
    base: fedora
    candy:
      - '@github.com/opencharly/layer-wf-recorder:v2026.245.1357'
```

Then, inside the desktop session:

```bash
wf-recorder -f output.mp4          # record to MP4
wf-recorder -f output.mp4 --audio  # with audio
wf-recorder -f output.mp4 -r 60    # 60fps
# Stop with Ctrl-C
```

The `record:` check verb drives the same binary declaratively — a `record: start`
step with `record_mode: desktop` auto-detects wf-recorder, and `record: stop`
with `artifact:` copies the `.mp4` out.

The candy's `plan:` asserts the binary at `/usr/bin/wf-recorder` and the package
registered.

## Layout

- `charly.yml` — the `wf-recorder:` candy entity (the `require:` on
  `plugin-record`, the per-distro packages, the `check:` assertions) and the
  embedded `wf-recorder-skill:` skill entity.
- `CHANGELOG/` — per-CalVer release history.
- `.github/workflows/tag-on-merge.yml` — CalVer tag + `CHANGELOG/` on merge.
- `README.md` — this user overview.

## Related

- Owning skill: `/charly-selkies:wf-recorder`
- `/charly-check:record` — the `record:` check verb (`record_mode: desktop` auto-detects wf-recorder)
- `/charly-selkies:wl-record-pixelflux` — alternative for selkies-desktop
- `/charly-selkies:wl-screenshot-grim` — screenshot companion (same `wlr-screencopy` protocol)
- `/charly-selkies:sway-desktop` — parent metalayer
- [`opencharly/charly`](https://github.com/opencharly/charly) — the charly CLI and image builder
- [`opencharly/opencharly`](https://github.com/opencharly/opencharly) — the umbrella
