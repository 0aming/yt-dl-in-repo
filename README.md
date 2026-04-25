# yt-dl-in-repo

Download YouTube (and 1800+ other sites) videos directly into your GitHub repo by writing URLs in `urls.txt`.

## Setup

1. **Enable write permissions for Actions**  
   Go to `Settings` → `Actions` → `General` → `Workflow permissions` → select `Read and write permissions` → `Save`.

2. **Add YouTube cookies (required to avoid bot blocks)**  
   - Export cookies from your browser as Netscape format (use extension like "Get cookies.txt LOCALLY").  
   - Encode `cookies.txt` to base64 (one line):  
     `base64 -w 0 cookies.txt`  
   - In your repo: `Settings` → `Secrets and variables` → `Actions` → `New repository secret`.  
     Name: `YOUTUBE_COOKIES`  
     Value: paste the long base64 string.  

## Usage

1. Create `urls.txt` in the root of your repo.  
2. Each line: `VIDEO_URL QUALITY` (quality optional: `360`, `480`, `720`, `1080`, `best`).  
   Example:
   - https://youtu.be/abc123 720
   - https://youtu.be/def456 1080
   - https://youtu.be/ghi789 best

3. Commit and push `urls.txt`. The workflow will trigger automatically (only when this file changes).

## Output

- Downloaded files appear in the `downloads/` folder.  
- If a video is larger than 90MB (GitHub’s soft limit), it is automatically split into `.part1.rar`, `.part2.rar`, … volumes.  
- To reassemble: extract `part1.rar` with any archive tool (WinRAR, 7-Zip, `unrar`).  

## Checking the result

- Go to the `Actions` tab → click the latest workflow run to see logs.  
- After a successful run, go back to the `Code` tab → open the `downloads/` folder to find your files.

## Cookie expiration

YouTube cookies expire after a few months. When downloads start failing with a `Sign in to confirm you’re not a bot` error, you need to refresh the cookie:  
- Export a fresh `cookies.txt` from your browser.  
- Re‑encode it to base64 and update the `YOUTUBE_COOKIES` secret.  

## Beyond YouTube

Because this tool uses `yt-dlp`, it supports **over 1800 sites** including Twitter, Instagram, Twitch, TikTok, Vimeo, SoundCloud, and many more. For most of them, just put the URL in `urls.txt` – no extra config needed. Some sites may require their own cookies (same method as YouTube).

## License

MIT
