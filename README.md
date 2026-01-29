import speech_recognition as sr
import pyttsx3
import smtplib
from geopy.geocoders import Nominatim
from datetime import datetime

# Initialize text-to-speech engine
engine = pyttsx3.init()

def speak(text):
    engine.say(text)
    engine.runAndWait()

def get_location():
    geolocator = Nominatim(user_agent="sos_alert_app")
    location = geolocator.geocode("Your address or use GPS module")
    return location.address if location else "Location unavailable"

def send_email_alert(location):
    sender_email = "your_email@example.com"
    receiver_email = "emergency_contact@example.com"
    password = "your_email_password"

    subject = "🚨 Emergency SOS Alert"
    body = f"Emergency alert triggered at {datetime.now().strftime('%Y-%m-%d %H:%M:%S')}\nLocation: {location}"

    message = f"Subject: {subject}\n\n{body}"

    try:
        with smtplib.SMTP_SSL("smtp.gmail.com", 465) as server:
            server.login(sender_email, password)
            server.sendmail(sender_email, receiver_email, message)
        speak("Emergency alert sent successfully.")
    except Exception as e:
        speak("Failed to send alert.")
        print(f"Error: {e}")

def listen_for_command():
    recognizer = sr.Recognizer()
    with sr.Microphone() as source:
        speak("Listening for SOS command...")
        audio = recognizer.listen(source)

    try:
        command = recognizer.recognize_google(audio).lower()
        print(f"Command received: {command}")
        if "help" in command or "sos" in command:
            location = get_location()
            send_email_alert(location)
        else:
            speak("No emergency command detected.")
    except sr.UnknownValueError:
        speak("Could not understand the command.")
    except sr.RequestError as e:
        speak("Speech recognition service failed.")
        print(f"Error: {e}")

if __name__ == "__main__":
    listen_for_command()
