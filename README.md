AI Video Summarizer with Mixtral, Whisper, and GPT-3

This project is a comprehensive solution for processing and summarizing YouTube videos. It utilizes a combination of advanced language models like GPT-3, Whisper, and Mixtral, along with AWS infrastructure, to handle the audio and video data efficiently. The workflow starts with downloading and transcribing audio from YouTube videos, followed by summarizing the content using GPT-3, and ends with providing an interactive quiz based on the video content. All models and services are deployed on AWS EC2 instances to ensure high availability and low latency.

Key Components:
YouTube Video Downloading:
The project leverages the pytube library to download YouTube videos, specifically fetching the audio stream. The audio is then saved locally for transcription.
Audio Transcription with Whisper:
Whisper, an automatic speech recognition (ASR) model, is used to transcribe the audio from the YouTube video into text. This step converts spoken content into machine-readable text for further analysis.
Summarization with GPT-3:
After transcription, the text is fed to OpenAI’s GPT-3, which processes the content and generates a concise summary. The system provides a title, key points, and a short conclusion in bullet-point format.
Dynamic Quiz Generation and Feedback:
The project includes a dynamic quiz generation system built using Flask, HTML, and JavaScript. The quiz questions are generated based on the video content, allowing users to interact with the summary and test their understanding. User responses are stored for analysis.
AWS EC2 Integration:
AWS EC2 instances are used for deploying the models (Whisper, GPT-3), ensuring that large models run efficiently and with minimal latency. The cloud infrastructure guarantees high availability and scalability.
How It Works:
Downloading the YouTube Video:

The process begins by using pytube to download the audio from the specified YouTube video URL. Only the audio stream is selected for transcription.
Transcribing Audio with Whisper:

The downloaded audio file is processed by Whisper, which transcribes the audio into text. The text is returned and stored for summarization.
Summarizing with GPT-3:

The transcribed text is sent to GPT-3 for summarization. GPT-3 processes the content and returns a brief summary, including key points, a title, and a conclusion. The summary is structured to be concise and easily understandable.
Interactive Quiz Generation:

A Flask-based web application is used to handle quiz submissions. The quiz is dynamically generated based on the summary of the video. After the user submits their responses, the data is stored for future analysis or feedback.
Deployment on AWS EC2:

To handle large model sizes and minimize latency, both Whisper and GPT-3 models are deployed on AWS EC2 instances. This setup ensures high performance, especially when processing long or complex videos.
Usage Instructions:
Set up the necessary credentials:

Make sure to set up your OpenAI API key and AWS credentials before running the system.
Install required Python libraries:

You will need the following libraries: whisper, openai, pytube, and flask. These can be installed using pip:
Copy code
pip install whisper openai pytube flask
Replace video URL:

In the script, replace the placeholder YOUTUBE_VIDEO_URL with the actual link to the YouTube video you want to summarize.
Run the script:

Execute the script using Python:
Copy code
python summarize_youtube_videos.py
Sample Output:
For a podcast episode like Joe Rogan with Dave Chappelle discussing 'Hollywood is Not Real Life', the generated summary might look like this:

vbnet
Copy code
Title: The Realities of Fame and the Importance of Being True to Yourself

Summary:
This conversation explores the nature of fame and the pressures that come with it. The speaker argues that celebrities, despite their public personas, are human and not immune to flaws. The discussion includes a personal narrative on finding purpose beyond fame, emphasizing authenticity and personal growth. A strong message about forgiveness and living a meaningful life is conveyed, challenging the pursuit of fame as an ultimate goal.

Introduction: The conversation reflects on fame and authenticity, focusing on self-discovery.

- The illusion of celebrity perfection
- Rejecting fame as the ultimate life goal
- The importance of staying true to oneself

Conclusion: A call for embracing authenticity and meaningful success beyond fame.
Conclusion:
This project provides a powerful tool for processing and summarizing YouTube videos, utilizing cutting-edge language models (Whisper, GPT-3) to ensure accuracy and efficiency. With the added feature of dynamic quiz generation, users can engage with the content and reinforce their learning. The use of AWS EC2 instances for deployment ensures the system is scalable and can handle large video data with minimal latency.

Contact Information:
For any questions or suggestions, feel free to reach out to:

Raj Purohith Arjun
Email: raj2001@tamu.edu
LinkedIn: Raj Purohith Arjun
