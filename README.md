# Personal-Assistant-With-Python
import pyttsx3
import speech_recognition as sr
import webbrowser 
import datetime 
import wikipedia 
import os
import random

def takeCommand():
    r = sr.Recognizer()
    with sr.Microphone() as source:
		print('Listening')
    r.pause_threshold = 0.7
	  audio = r.listen(source)
   try:
			print("Recognizing")
			Query = r.recognize_google(audio, language='en-in')
			print("the command is printed=", Query)
			
   except Exception as e:
			print(e)
			print("Say that again sir")
			return "None"
		
  return Query

def speak(audio):
	engine = pyttsx3.init()
	voices = engine.getProperty('voices')
  engine.setProperty('voice', voices[0].id)
	engine.say(audio) 
	engine.runAndWait()

def tellDay():
	day = datetime.datetime.today().weekday() + 1
	Day_dict = {1: 'Monday', 2: 'Tuesday', 
				3: 'Wednesday', 4: 'Thursday', 
				5: 'Friday', 6: 'Saturday',
				7: 'Sunday'}
    if day in Day_dict.keys():
		day_of_the_week = Day_dict[day]
		print(day_of_the_week)
		speak("The day is " + day_of_the_week)


def tellTime():
	time = str(datetime.datetime.now())
  print(time)
	hour = time[11:13]
	min = time[14:16]
	speak("The time is sir" + hour + "Hours and" + min + "Minutes") 

def Hello():
	speak('''hello sir I am your personal assistant,jarvis.
		Tell me how may I help you''')


def Take_query():
	Hello()
	while(True):
		query = takeCommand().lower()
		if "open youtube" in query:
			speak("Opening youtube")
			webbrowser.open("www.youtube.com")
			continue
   elif "open google" in query:
			speak("Opening Google ")
			webbrowser.open("www.google.com")
			continue
			
   elif "which day it is" in query:
			tellDay()
			continue
		
   elif "what is the time now" in query:
			tellTime()
			continue
		
   elif "can we meet again" in query:
			speak("Ok Bye Sir Can we meet again soon")
			exit()
		
   elif "from wikipedia" in query:
			speak("Checking the wikipedia ")
			query = query.replace("wikipedia", " ")
			result = wikipedia.summary(query, sentences=4)
			speak("According to wikipedia")
			speak(result)
	 elif "tell me your name" in query:
			speak("I am Jarvis. Your personal Assistant")
		elif "stop jarvis" in query:
			speak("Ok sir")	
		elif "suggest a song for me" in query:
			speak("ok sir")
			webbrowser.open("https://www.youtube.com/watch?v=CS7hBHVGWs0")


if __name__ == '__main__':
	Take_query()
