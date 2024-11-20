# AI Video Summarizer with Mixtral, Whisper, and GPT-3

This project leverages the power of language models like GPT-3, Whisper, and Mixtral, combined with AWS infrastructure, to efficiently process and summarize YouTube videos. The system uses Whisper for audio transcription, GPT-3 for generating concise video summaries, and AWS EC2 instances to minimize latency during large model execution. Additionally, a dynamic quiz generation system is implemented using Flask, HTML, and JavaScript to engage users with video content.

## Prerequisites

Before you begin, ensure you have the following:

- Python (>= 3.6)
- `whisper` library (for audio transcription)
- `openai` library (for GPT-3 integration)
- `pytube` library (for downloading YouTube videos)
- AWS EC2 instances for model deployment

Set up your OpenAI API key and AWS credentials appropriately.

## Script Overview

### 1. Downloading YouTube Video

The process starts by downloading the audio from a YouTube video using the `pytube` library. This fetches the audio-only stream and saves it for further processing.

```python
from pytube import YouTube

youtube_video = YouTube(YOUTUBE_VIDEO_URL)
streams = youtube_video.streams.filter(only_audio=True)
# selecting the lowest quality audio stream
stream = streams.first()
stream.download(filename=OUTPUT_AUDIO)
