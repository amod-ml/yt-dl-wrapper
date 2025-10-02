# ytdl - A Powerful yt-dlp Wrapper

<p align="center">
  <strong>A user-friendly bash wrapper for yt-dlp that simplifies downloading videos and audio with automatic transcription support from 1000+ websites.</strong>
</p>

## Features

- **Video Download Mode** - Downloads best quality video with modern codec preference (VP9/AV1)
- **Audio Download Mode** - Extracts and converts audio to MP3 (128kbps)
- **Automatic Transcriptions** - Downloads subtitles and auto-generated transcriptions separately
- **Configurable Subtitle Languages** - Choose specific language or download all available
- **Organized Downloads** - Defaults to ~/Downloads directory, customizable output location
- **Privacy-Focused** - No cookies, no cache, full anonymity
- **Multi-Platform Support** - Works with YouTube, Facebook, Instagram, TikTok, Twitter, Vimeo, and 1000+ other sites
- **Clean CLI** - User-friendly command-line interface
- **Modern Codecs** - Prefers VP9 and AV1 codecs when available
- **Linux Native** - Built for Linux environments

## Prerequisites

Before using ytdl, ensure you have the following installed:

- `yt-dlp` - The download engine
- `ffmpeg` - For audio/video processing

### Installation on Arch/Manjaro

```bash
paru -S yt-dlp ffmpeg
```

### Installation on Debian/Ubuntu

```bash
sudo apt install yt-dlp ffmpeg
```

## Installation

1. Clone the repository:
```bash
git clone https://github.com/amod-ml/yt-dl-wrapper.git
cd yt-dl-wrapper
```

2. Make the script executable:
```bash
chmod +x ytdl
```

3. (Optional) Add to your PATH:
```bash
# Add to ~/.bashrc or ~/.zshrc
export PATH="$PATH:/path/to/yt-dl-wrapper"
```

Or create a symlink:
```bash
sudo ln -s /path/to/yt-dl-wrapper/ytdl /usr/local/bin/ytdl
```

## Usage

### Basic Commands

```bash
# Download video with English subtitles (default)
./ytdl https://www.youtube.com/watch?v=dQw4w9WgXcQ

# Explicitly specify video mode
./ytdl -v https://www.youtube.com/watch?v=dQw4w9WgXcQ

# Download video with Spanish subtitles
./ytdl -v -l es https://www.youtube.com/watch?v=dQw4w9WgXcQ

# Download video with all available subtitles
./ytdl -v -l all https://www.youtube.com/watch?v=dQw4w9WgXcQ

# Download to custom directory
./ytdl -o ~/Videos https://www.youtube.com/watch?v=dQw4w9WgXcQ

# Download audio only (converts to MP3 128kbps with transcription)
./ytdl -a https://www.youtube.com/watch?v=dQw4w9WgXcQ

# Download audio with Spanish transcription
./ytdl -a -l es https://www.youtube.com/watch?v=dQw4w9WgXcQ

# Interactive mode - prompts for URL
./ytdl
./ytdl -a

# Show help
./ytdl -h
```

### Command-Line Options

| Option | Description |
|--------|-------------|
| `-v, --video` | Download video (default mode). Prefers VP9/AV1 codecs, downloads best quality, includes subtitles/transcriptions |
| `-a, --audio` | Download audio only. Converts to MP3 128kbps format. Includes transcription as .txt file if available |
| `-l, --lang LANG` | Subtitle language code (default: en). Examples: en, es, fr, de, ja, ko, pt, etc. Use 'all' for all available languages |
| `-o, --output DIR` | Output directory (default: ~/Downloads). Downloads will be saved to this directory |
| `-h, --help` | Show help message |

## Supported Platforms

ytdl works with 1000+ websites including:

- **Video Platforms**: YouTube, Vimeo, Dailymotion
- **Social Media**: Facebook, Instagram, TikTok, Twitter/X
- **Streaming**: Twitch, YouTube Live
- **Educational**: Coursera, Khan Academy, Udemy
- **News**: CNN, BBC, NBC
- And many more!

For a complete list of supported sites, run:
```bash
yt-dlp --list-extractors
```

## Examples

### Download a YouTube video with English subtitles
```bash
./ytdl https://www.youtube.com/watch?v=dQw4w9WgXcQ
```
This will download:
- Video file (best quality, VP9/AV1 preferred)
- English subtitle file (.srt format)
- Auto-generated transcription if manual subtitle unavailable

### Download with specific language subtitles
```bash
# French subtitles
./ytdl -l fr https://www.youtube.com/watch?v=dQw4w9WgXcQ

# Japanese subtitles
./ytdl -l ja https://www.youtube.com/watch?v=dQw4w9WgXcQ

# All available languages
./ytdl -l all https://www.youtube.com/watch?v=dQw4w9WgXcQ
```

### Download to custom directory
```bash
# Download to Videos folder
./ytdl -o ~/Videos https://www.youtube.com/watch?v=dQw4w9WgXcQ

# Download to specific path
./ytdl -o /media/external/downloads https://www.youtube.com/watch?v=dQw4w9WgXcQ

# Combine with other options
./ytdl -a -o ~/Music https://www.youtube.com/watch?v=dQw4w9WgXcQ
```

### Download Instagram video
```bash
./ytdl https://www.instagram.com/p/ABC123/
```

### Download Facebook video
```bash
./ytdl https://www.facebook.com/watch/?v=123456789
```

### Extract audio from a video
```bash
./ytdl -a https://www.youtube.com/watch?v=dQw4w9WgXcQ
```
This will download and convert the audio to MP3 format at 128kbps, along with the transcription as a .txt file if available.

### Download TikTok video
```bash
./ytdl https://www.tiktok.com/@username/video/1234567890
```

## Technical Details

### Video Mode
- **Format Selection**: `bestvideo[vcodec^=vp9]+bestaudio/bestvideo[vcodec^=av01]+bestaudio/bestvideo+bestaudio/best`
- **Codec Preference**: VP9 → AV1 → Best Available
- **Subtitles**: Downloads all available subtitles in SRT format
- **Auto-Subtitles**: Downloads auto-generated transcriptions
- **Privacy**: `--no-cookies --no-cache-dir`

### Audio Mode
- **Format Selection**: `bestaudio/best`
- **Output Format**: MP3
- **Audio Quality**: 128kbps
- **Transcription**: Downloads and converts subtitles to plain .txt format
- **Processing**: FFmpeg audio extraction and conversion

## Troubleshooting

### "Missing required dependencies" error
Install the required packages:
```bash
paru -S yt-dlp ffmpeg  # Arch/Manjaro
sudo apt install yt-dlp ffmpeg  # Debian/Ubuntu
```

### "Invalid URL format" error
Ensure your URL starts with `http://` or `https://`

### Downloads fail for certain sites
Some sites may have restrictions. Try:
1. Updating yt-dlp: `yt-dlp -U` or `paru -S yt-dlp`
2. Checking if the site is supported: `yt-dlp --list-extractors | grep sitename`

### No transcriptions downloaded
Not all videos have transcriptions available. The script will download them if they exist, but won't fail if they're absent.

## Output Files

### Default Output Location
By default, all downloads are saved to `~/Downloads`. You can change this with the `-o` option.

### Video Mode
- `VideoTitle.ext` - Video file (usually .mp4, .webm, or .mkv)
- `VideoTitle.LANG.srt` - Subtitle file in specified language (e.g., VideoTitle.en.srt, VideoTitle.es.srt)

### Audio Mode
- `AudioTitle.mp3` - Audio file in MP3 format (128kbps)
- `AudioTitle.LANG.txt` - Transcription in plain text format (e.g., AudioTitle.en.txt, AudioTitle.es.txt)

## Contributing

Contributions are welcome! Feel free to:
- Report bugs
- Suggest new features
- Submit pull requests

## License

MIT License

Copyright (c) 2025 amod-ml

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.

## Acknowledgments

- Built on top of [yt-dlp](https://github.com/yt-dlp/yt-dlp)
- Uses [FFmpeg](https://ffmpeg.org/) for media processing

## Contact

- GitHub: [@amod-ml](https://github.com/amod-ml)
- Email: amodsahabandu@icloud.com

---

<p align="center">
  <strong>Made for command-line enthusiasts</strong>
</p>
