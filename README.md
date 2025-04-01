# raina_ai.py
import speech_recognition as sr
import os
import time
import subprocess

# Initialize recognizer class (for recognizing the speech)
recognizer = sr.Recognizer()

# Function to listen for voice commands
def listen():
    with sr.Microphone() as source:
        print("Listening for command...")
        audio = recognizer.listen(source)
        command = ""
        try:
            command = recognizer.recognize_google(audio)
            print(f"Command received: {command}")
        except sr.UnknownValueError:
            print("Sorry, I did not understand that.")
        except sr.RequestError:
            print("Sorry, I am unable to connect to Google Speech service.")
        return command.lower()

# Function to lock the phone (specific for Android - you may need to adjust this based on the app you are using)
def lock_phone():
    print("Locking the phone...")
    os.system("input keyevent 26")  # Simulates pressing the power button to lock
    time.sleep(1)

# Function to unlock the phone (specific for your device setup)
def unlock_phone():
    print("Unlocking the phone...")
    # Here you can add your code to unlock the phone if possible
    # For example, simulate pressing the power button and swipe
    os.system("input keyevent 26")
    time.sleep(1)
    os.system("input swipe 300 1000 300 500")  # Simulate swipe to unlock (optional)

# Main function to start AI assistant
def main():
    print("Raina AI is now active. Say 'lock' to lock the phone, or 'unlock' to unlock.")
    
    while True:
        command = listen()
        if 'lock' in command:
            lock_phone()
        elif 'unlock' in command:
            unlock_phone()
        elif 'exit' in command:
            print("Exiting Raina AI.")
            break
        else:
            print("Sorry, I can only lock or unlock the phone.")
        time.sleep(2)

if __name__ == "__main__":
    main()
