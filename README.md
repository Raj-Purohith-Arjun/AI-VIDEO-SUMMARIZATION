# YouTube Video Summarizer with Mixtral, Whisper, and GPT-3

This project leverages the power of language models like GPT-3, Whisper, and Mixtral, combined with AWS infrastructure, to efficiently process and summarize YouTube videos. The system uses Whisper for accurate audio transcription, GPT-3 for generating concise video summaries, and AWS EC2 instances to minimize latency during large model execution. Additionally, a dynamic quiz generation system is implemented using Flask, HTML, and JavaScript to engage users with video content.

## Prerequisites

Before you begin, ensure that you have the necessary setup:

- Python (>=3.6)
- `whisper` library (for audio transcription)
- `openai` library (for GPT-3 integration)
- `pytube` library (for downloading YouTube videos)
- AWS EC2 instances for model deployment

You should also set up your OpenAI API key and AWS credentials appropriately.

## Script Overview

### 1. Downloading YouTube Video

The process starts with downloading the audio from a YouTube video. The `pytube` library is used to fetch the video, select the audio-only stream, and save it as an audio file for further processing.

```python
from pytube import YouTube

youtube_video = YouTube(YOUTUBE_VIDEO_URL)
streams = youtube_video.streams.filter(only_audio=True)
# selecting the lowest quality audio stream
stream = streams.first()
stream.download(filename=OUTPUT_AUDIO)



2. Audio Transcription with Whisper
Next, the audio is transcribed into text using Whisper. This allows us to convert speech into text efficiently, enabling the summarization step.

import whisper

model = whisper.load_model(WHISPER_MODEL)
transcript = model.transcribe(OUTPUT_AUDIO.as_posix())
transcript = transcript['text']
print(f'Transcript generated: \n{transcript}')



3. Summarization with GPT-3
The transcribed text is then passed to GPT-3 for summarization. The model processes the text to create a concise summary, including a title and key points from the video.


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


4. Dynamic Quiz Generation and Feedback
In addition to summarization, the project includes a dynamic quiz generation system implemented using Flask, HTML, and JavaScript. Users can interact with the video summary by answering questions based on the content, and their responses are stored in a database for analysis.


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

5. AWS EC2 Integration for Model Deployment
To minimize latency and efficiently handle large models, the project uses AWS EC2 instances. The models (Whisper, GPT-3) are deployed on EC2 instances to ensure high availability and performance.

Usage
Set up your OpenAI API key and AWS credentials.
Install the required Python libraries (whisper, openai, pytube) using pip.
Replace YOUTUBE_VIDEO_URL with the link to the YouTube video you want to summarize.
Run the script using python summarize_youtube_videos.py.

Sample Output
For the podcast Joe Rogan with Dave Chappelle discussing 'Hollywood is Not Real Life', the system generates the following summary:

'''
Title: The Realities of Fame and the Importance of Being True to Yourself

Summary:
This conversation explores the nature of fame and the pressures that come with it. The speaker argues that celebrities, despite their public personas, are human and not immune to flaws. The discussion includes a personal narrative on finding purpose beyond fame, emphasizing authenticity and personal growth. A strong message about forgiveness and living a meaningful life is conveyed, challenging the pursuit of fame as an ultimate goal.

Introduction: The conversation reflects on fame and authenticity, focusing on self-discovery.

- The illusion of celebrity perfection
- Rejecting fame as the ultimate life goal
- The importance of staying true to oneself

Conclusion: A call for embracing authenticity and meaningful success beyond fame.
'''



For any questions or suggestions, feel free to reach out:

Raj Purohith Arjun
email: raj2001@tamu.edu
LinkedIn: https://www.linkedin.com/in/raj-purohith-arjun-20a652200
