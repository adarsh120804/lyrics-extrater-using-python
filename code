import tkinter as tk
from tkinter import simpledialog, messagebox
import requests
from bs4 import BeautifulSoup

# Function to fetch lyrics using Lyrics.ovh API
#This function takes two inputs—song title and artist name—and sends a GET request to the Lyrics.ovh API to fetch the song's lyrics.
def fetch_lyrics(song_title, artist_name):
    try:
        api_url = f"https://api.lyrics.ovh/v1/{artist_name}/{song_title}"
        response = requests.get(api_url)
        data = response.json()

        if "lyrics" in data:
            return data["lyrics"]
        else:
            return "Lyrics not found. Please check the song and artist name."
    except Exception as e:
        return str(e)


# Function to display lyrics in the text box
def display_lyrics():
    song_title = song_entry.get()
    artist_name = artist_entry.get()

    if song_title and artist_name:
        lyrics = fetch_lyrics(song_title, artist_name)
        lyrics_display.delete("1.0", tk.END)  # Clear previous lyrics
        lyrics_display.insert(tk.END, lyrics)
        '''
        
        '''
    else:
        messagebox.showwarning("Input Error", "Please enter both song title and artist name.")


# Function to fetch lyrics using web scraping (optional)
def fetch_lyrics_web_scraping(song_title, artist_name):
    try:
        search_url = f"https://search.azlyrics.com/search.php?q={song_title} {artist_name}"
        response = requests.get(search_url)
        soup = BeautifulSoup(response.text, 'html.parser')
        link = soup.find('a', href=True, text=True)

        if link:
            lyrics_page = requests.get(link['href'])
            lyrics_soup = BeautifulSoup(lyrics_page.text, 'html.parser')
            lyrics = lyrics_soup.find("div", {"class": None, "id": None}).get_text()
            return lyrics
        else:
            return "Lyrics not found through web scraping."
    except Exception as e:
        return str(e)


# GUI Setup
root = tk.Tk()
root.title("Lyrics Extractor")
# Song Title Entry
tk.Label(root, text="Song Title:").pack(padx=10, pady=5)
song_entry = tk.Entry(root, width=40)
song_entry.pack(padx=10, pady=5)

root.configure(bg="#D0F0C0") 
# Artist Name Entry
tk.Label(root, text="Artist Name:").pack(padx=10, pady=5)
artist_entry = tk.Entry(root, width=40)
artist_entry.pack(padx=10, pady=5)

# Button to Fetch Lyrics
fetch_button = tk.Button(root, text="Fetch Lyrics", command=display_lyrics)
fetch_button.pack(padx=10, pady=10)

# Text box to display lyrics
lyrics_display = tk.Text(root, height=15, width=60, wrap=tk.WORD)
lyrics_display.pack(padx=10, pady=10)

footer_frame = tk.Frame(root, bg="#2e3d4f", padx=10)
footer_frame.pack(side="bottom", fill="x")

footer_label = tk.Label(footer_frame, text="Copyright 2023 Next24Tech. All rights reserved.\nAddress: Goregaon, Gondia, 441801 India \nPhone no: +91 9112327362", 
                        font=("Arial", 12), fg="#ffffff", bg="#4CAF50", anchor="w")
footer_label.pack()

root.mainloop()
