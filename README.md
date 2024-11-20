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


import whisper

model = whisper.load_model(WHISPER_MODEL)
transcript = model.transcribe(OUTPUT_AUDIO.as_posix())
transcript = transcript['text']
print(f'Transcript generated: \n{transcript}')





import openai

system_prompt = "Assume the role of a summarization expert."
user_prompt = f"""Generate a concise summary of the text below.
Text: {transcript}

Provide a title, and make sure the summary includes the main points.
Use bullet points for key details, and conclude with a brief summary."""
  
response = openai.ChatCompletion.create(
    model='gpt-3.5-turbo',
    messages=[
        {'role': 'system', 'content': system_prompt},
        {'role': 'user', 'content': user_prompt}
    ],
    max_tokens=4096,
    temperature=1
)

summary = response['choices'][0]['message']['content']





# Example Flask code for handling quiz responses
from flask import Flask, request, render_template

app = Flask(__name__)

@app.route('/submit_quiz', methods=['POST'])
def submit_quiz():
    # Store user responses in the database
    user_data = request.form['quiz_responses']
    store_user_data(user_data)
    return render_template('quiz_results.html', user_data=user_data)

def store_user_data(data):
    # Placeholder for storing data
    pass




python summarize_youtube_videos.py



Title: The Realities of Fame and the Importance of Being True to Yourself

Summary:
This conversation explores the nature of fame and the pressures that come with it. The speaker argues that celebrities, despite their public personas, are human and not immune to flaws. The discussion includes a personal narrative on finding purpose beyond fame, emphasizing authenticity and personal growth. A strong message about forgiveness and living a meaningful life is conveyed, challenging the pursuit of fame as an ultimate goal.

Introduction: The conversation reflects on fame and authenticity, focusing on self-discovery.
- The illusion of celebrity perfection
- Rejecting fame as the ultimate life goal
- The importance of staying true to oneself

Conclusion: A call for embracing authenticity and meaningful success beyond fame.




### Contact
### For any questions or suggestions, feel free to reach out:

### Raj Purohith Arjun
### Email: raj2001@tamu.edu
### LinkedIn: Raj Purohith Arjun

