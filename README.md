# 2000.moi

Small static browser game for <https://2000.moi>.

The joke: `20 x 100 = 2000`, and in French `vingt-cent` sounds like
`Vincent`.

## Project Shape

- `index.html` contains the full app: markup, CSS, and JavaScript.
- `og-image.png` is the social preview image.
- There is no build step and no package install.

## Local Preview

Opening `index.html` directly works. For a browser served over HTTP:

```sh
python3 -m http.server 8000
```

Then open <http://127.0.0.1:8000>.

## UI Notes

- Keep static surfaces flat.
- Use drop shadows only on interactive controls, so shadow means clickability.
- Current interactive shadow classes are `.chip`, `.hold`, and `.again`.
- The main hold control supports pointer input and the spacebar.

## Deploy

Production is served by Caddy from `/opt/2000.moi` on the `stockage` VPS.

After pushing `main`, deploy by pulling the repo on the VPS:

```sh
git push origin main
ssh stockage "sudo git -C /opt/2000.moi pull --ff-only origin main"
curl -I https://2000.moi
```

If the VPS pull fails because local files changed, inspect the diff before
resetting anything.

## Quick Checks

```sh
rg -n "box-shadow|text-shadow|drop-shadow|filter:\\s*drop-shadow" index.html
```

Shadow declarations should remain limited to the interactive controls.
