# yt-dl-in-repo

Download YouTube videos into your repo by adding links to `urls.txt`.

## How it works

- Create `urls.txt` in the root.
- Each line: `VIDEO_URL QUALITY` (quality optional, e.g. `720`, `1080`, `best`).
- Commit and push. A GitHub Action runs, downloads videos, splits files over 90MB (GitHub's 100MB limit), and commits them into `downloads/`.

## One‑time setup

1. Go to **Settings** → **Actions** → **General** → **Workflow permissions** → select **Read and write permissions** → **Save**.
2. Create `urls.txt` with your links.
3. Commit & push.

## Example `urls.txt`

https://youtu.be/abc123 720
https://youtu.be/def456 1080
https://youtu.be/ghi789 best

## Notes

- Large files are split into `.zip`, `.z01`, `.z02` – combine with `zip -F` or any archive manager.
- To change quality globally, edit the workflow file.
