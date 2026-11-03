# Video Splitter

A lightweight Python utility that splits large video files into smaller MP4 segments using FFmpeg.

Video Splitter automatically calculates an approximate segment duration based on the video's bitrate and a configurable target file size.

## Features

- **Graphical file selection:** Choose a video using a file-selection window.
- **Automatic bitrate detection:** Uses FFprobe to inspect the video's overall bitrate.
- **Automatic segment timing:** Calculates an estimated duration for each segment.
- **No re-encoding:** Copies existing streams instead of re-encoding the video.
- **Quality preservation:** Avoids additional compression from re-encoding.
- **Automatic output folders:** Creates a folder beside the selected video.
- **Sequential filenames:** Numbers each output segment automatically.

## Supported Input Selections

- MP4
- MOV
- AVI
- MKV
- WEBM

The actual codecs and streams must also be compatible with the MP4 output container.

## Default Settings

| Setting | Default |
|---|---|
| Target segment size | 9.9 MB |
| Output format | MP4 |
| Video processing | Stream copy |
| Output location | Beside the source video |

To change the target size, edit:

```python
TARGET_SIZE_MB = 9.9
```

## Requirements

- Python 3
- FFmpeg
- FFprobe

Both FFmpeg and FFprobe must be installed and accessible through your system PATH.

See [SETUP.md](SETUP.md) for installation instructions.

## Usage

Run the script:

```bash
python video_splitter.py
```

A file-selection window will appear.

1. Select the video you want to split.
2. The program reads the video's bitrate.
3. It estimates how long each segment should be.
4. FFmpeg creates the segments.
5. The finished parts are saved in a new folder beside the original video.

## Output Structure

For a video named `Example.mp4`, the output will look like:

```text
Example_parts/
├── Example_part00.mp4
├── Example_part01.mp4
├── Example_part02.mp4
└── Example_part03.mp4
```

## How It Works

The program uses FFprobe to retrieve the video's overall bitrate.

It then estimates the segment duration using:

```text
Target segment bits / Total bitrate = Segment duration
```

FFmpeg uses stream copying (`-c copy`) to split the video without re-encoding it.

## Important Limitations

- The target size is approximate. Actual segment sizes may differ.
- FFmpeg generally cuts at available video keyframes, which can affect segment duration and file size.
- The script always produces MP4 output, regardless of the original extension.
- Some codecs, subtitles, or other streams may not work correctly in an MP4 container.
- Files with missing or unavailable bitrate information may cause the script to fail.
- Existing output files with matching names may be overwritten.

## License

This project is licensed under the MIT License.
