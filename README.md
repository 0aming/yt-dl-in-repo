# yt-dl-in-repo

A simple tool that downloads YouTube (and maybe other sites) videos into your GitHub repo. Uses [yt-dlp](https://github.com/yt-dlp/yt-dlp) and [aria2](https://github.com/aria2/aria2) for fast downloads.

## Setup

0. **fork this repo**

1. **Give Actions write permission**  
   Go to your repo: `Settings` → `Actions` → `General` → `Workflow permissions` → select `Read and write permissions` → `Save`.

2. **Get YouTube cookies** (to avoid bot errors)  
   - Use a browser extension like "Get cookies.txt LOCALLY" to export cookies in `Netscape` format.
   > For detailed instructions on how to export your YouTube cookies, please refer to the [yt-dlp wiki](https://github.com/yt-dlp/yt-dlp/wiki/Extractors#exporting-youtube-cookies).
   - Convert to a single‑line base64 string: `base64 -w 0 cookies.txt`  
   - In your repo: `Settings` → `Secrets and variables` → `Actions` → `New repository secret`  
     Name: `YOUTUBE_COOKIES`  
     Value: paste the base64 string.

## Usage

Place your links in `urls.txt`. Each line: a video URL, optionally followed by a quality number. Supported qualities: `360`, `480`, `720`, `1080`, `best` (default is `best`).

Example:
- https://youtu.be/abc123 720
- https://youtu.be/def456 
- https://youtu.be/ghi789 best

Then commit and push. The workflow runs **only when `urls.txt` changes**.

## Output

Downloaded files go into the `downloads/` folder. If a file is larger than 90MB (GitHub’s 100MB limit), it gets split into `.part1.rar`, `.part2.rar`, etc. To reassemble, extract `part1.rar` with any archive tool (WinRAR, 7-Zip, `unrar`).

## Checking the result

- Go to the `Actions` tab → click the latest workflow run to see logs.  
- When it finishes, go back to the `Code` tab → open the `downloads/` folder.

## Beyond YouTube

Because this uses [yt-dlp](https://github.com/yt-dlp/yt-dlp), it works with 1800+ sites (Twitter, Instagram, Twitch, TikTok, Vimeo, SoundCloud, etc.). For most, just paste the URL. Some may need their own cookies (same method as YouTube).


# ⚠️ **!!! COOKIES EXPIRE !!!**  
 After ~3-5 months, the secret `YOUR_COOKIES` becomes invalid.  
 → Export a fresh `cookies.txt` (Netscape format)  
 → Encode to base64 (`base64 -w 0 cookies.txt`)  
 → Update the secret in your repo `Settings`.
 
## Acknowledgments

- Inspired by [github-sandbox](https://github.com/maanimis/github-sandbox) by [Meisam Maani](https://github.com/maanimis). The idea of triggering downloads via commit messages comes from that project.
