# Developer Guide

## What this repo is

The README.md is the protocol specification. Changes to README.md are changes to GBDP itself.

The `docs/` folder applies GBDP to its own development — decisions made while building the protocol, conventions the protocol follows, and the architecture of the repo structure.

## Working on this repo

1. Read `CONTRIBUTING.md` to identify the change class.
2. For Class 1/2: draft a decision in `docs/decisions/` before writing any content changes.
3. Update `README.md` or `docs/` as appropriate.
4. Ensure `AI.md` is current if the operational rules changed.
5. Open a PR.

## Using the bootstrapper

Copy the bash block from Section 7 of `README.md` and run it in a new directory. It creates the full folder structure, root files, and genre templates in one pass.

## Testing a change to the bootstrapper

Run the bash block in a temp directory and verify the output:

```bash
mkdir /tmp/gbdp-test && cd /tmp/gbdp-test
# paste and run the bootstrapper block
ls -R
```
