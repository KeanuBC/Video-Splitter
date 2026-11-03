# Video Splitter - Setup & Installation

## 1. Requirements

- Python 3.9 or newer recommended
- FFmpeg
- FFprobe
- Tkinter

Tkinter is normally included with standard Python installations on Windows.

## 2. Install FFmpeg

Video Splitter requires both FFmpeg and FFprobe.

Download FFmpeg from:

https://ffmpeg.org/download.html

After installation, make sure the FFmpeg `bin` directory is added to your system PATH.

This directory should contain:

```text
ffmpeg.exe
ffprobe.exe
```

## 3. Verify Installation

Open Command Prompt and run:

```bash
ffmpeg -version
```

Then:

```bash
ffprobe -version
```

If both commands display version information, FFmpeg and FFprobe should be accessible.

If Windows reports that either command is not recognized, check your PATH configuration.

## 4. Project Files

A simple project structure:

```text
Video-Splitter/
├── video_splitter.py
├── README.md
├── SETUP.md
└── LICENSE
```

No additional Python packages are required by the script.

## 5. Configure Target Size

Open `video_splitter.py` and locate:

```python
TARGET_SIZE_MB = 9.9
```

Change the number to adjust the approximate target size of each segment.

For example:

```python
TARGET_SIZE_MB = 25
```

This would aim for segments around 25 MB.

## 6. Run the Program

Open Command Prompt in the project directory and run:

```bash
python video_splitter.py
```

A file-selection window will appear.

Select the video you want to split.

The program automatically creates an output directory beside the selected video.

## 7. Output Files

If your selected video is:

```text
Example.mp4
```

The output directory will be:

```text
Example_parts/
```

The resulting segments will be named:

```text
Example_part00.mp4
Example_part01.mp4
Example_part02.mp4
```

## 8. Important Notes

- The original video is not modified.
- Output segments are created using stream copying.
- No video re-encoding takes place.
- Segment sizes are estimates, not guaranteed limits.
- Keyframe placement can affect the final segment duration and size.
- Output is always MP4, so some source codecs may not be compatible.
- Existing output files may be overwritten.

## 9. Troubleshooting

### FFmpeg Is Not Recognized

Make sure FFmpeg is installed and its `bin` directory is included in your system PATH.

### FFprobe Is Not Recognized

Check that `ffprobe.exe` exists in the same FFmpeg `bin` directory and that the directory is included in PATH.

### No Video Was Selected

If you close the file-selection window without choosing a video, the program exits without splitting anything.

### Segment Sizes Are Larger or Smaller Than Expected

The target size is calculated using the video's overall bitrate. Actual sizes can vary because of variable bitrate encoding and keyframe-based splitting.

### The Program Fails to Read the Bitrate

Some files do not provide usable bitrate information. The current script expects FFprobe to return a numeric overall bitrate.

### Output Files Cannot Be Played

Some video or audio codecs may not be compatible with MP4 when copied directly. Stream copying does not convert incompatible codecs.
