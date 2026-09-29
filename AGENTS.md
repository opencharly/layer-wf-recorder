# AGENTS.md — layer-wf-recorder

Standalone candy repo for the `wf-recorder` layer — the wlroots Wayland screen
recorder that backs the `record:` check verb on sway. The candy lives in
`charly.yml` at the repo root: the `require:` on `plugin-record`, the per-distro
packages, the `check:` assertions, and the embedded `skill:` entity projected
into the marketplace corpus as `/charly-selkies:wf-recorder`.

Canonical files:

- `charly.yml` — the `wf-recorder:` candy entity and the `wf-recorder-skill:`
  skill entity.
- `CHANGELOG/` — per-CalVer release history.
- `.github/workflows/tag-on-merge.yml` — CalVer tag + `CHANGELOG/` on merge.
- `README.md` — user overview only; never agent guidance.

## Load these skills first (R0)

- `/charly-selkies:wf-recorder` — the owning skill. The `wlr-screencopy`
  contract, the `record:` verb integration, and why it does not work on
  selkies-desktop. Load before editing or troubleshooting the layer.
- `/charly-image:layer` — the candy authoring reference (`charly.yml` schema,
  `plan:` step verbs incl. `check:`, per-distro `distro:` arms, package/repo
  sections, service declarations). Load before editing any entity field or plan
  step.

## Build / validate / test

- The merge gate is the **org-wide** `charly/pr-validator` (required check
  `validate / validate`, defined in `opencharly/.github`); this repo has **no
  per-repo candy gate** and ships only `.github/workflows/tag-on-merge.yml`.
- The candy's `plan:` `check:` steps are the functional evidence — the binary at
  `/usr/bin/wf-recorder` and the registered package.
- The `require:` on `plugin-record` is load-bearing: without it the `record:`
  verb is not build-connected and a baked check SKIPs with `unknown verb
  "record"`. Keep the pin in step with the plugin.

## Modify this repo

- Edit the `wf-recorder:` candy entity AND the `wf-recorder-skill:` skill entity
  in `charly.yml` together. The skill is the projected usage source, so a
  behaviour change not mirrored in the skill leaves the corpus stale.
- The per-distro package list covers fedora / arch / omarchy; keep every arm in
  sync.
- New behaviour claims belong in the `plan:` as an observable `check:` step, and
  in the skill body.

## Landing

- PR-only. Every change lands through a pull request; the org-required
  `charly/pr-validator` validates the diff and body and arms native auto-merge on
  PASS. Direct pushes to `main` are blocked.
- History lives in `CHANGELOG/` (written by `tag-on-merge` at merge time); the PR
  body IS the changelog.
- The authoritative rulebook is the umbrella `AGENTS.md` in
  `opencharly/opencharly` and `charly/AGENTS.md` in the charly repo. Do not
  restate its rules here.
