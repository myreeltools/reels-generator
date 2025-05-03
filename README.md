from gtts import gTTS
from moviepy.editor import *
import gradio as gr

def generate_video(text):
    tts = gTTS(text)
    tts.save("audio.mp3")
    clip = TextClip(text, fontsize=70, color='white', size=(1280,720)).set_duration(5)
    audioclip = AudioFileClip("audio.mp3")
    videoclip = clip.set_audio(audioclip)
    videoclip.write_videofile("output.mp4", fps=24)
    return "output.mp4"

gr.Interface(fn=generate_video, inputs="text", outputs="video").launch()
