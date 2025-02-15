AI Username Generator

Overview

The AI Username Generator is an interactive Python-based tool designed to generate unique usernames, accept user ratings, and improve its suggestions over time using a machine learning model. It provides customization options for username formats, incorporates user feedback, and allows downloading rated usernames for personal use.

Features

Unlimited Username Generation:

Generate as many usernames as needed with customizable options.

AI-Powered Suggestions:

Username quality is predicted using a Random Forest Regressor.

Ratings provided by the user help refine future suggestions.

Customization Options:

Define the number of letters in the username.

Optionally include numbers and special characters.

Rating System:

Rate generated usernames (1-5 stars) to provide feedback.

AI uses this feedback to improve its predictions and future suggestions.

Export Functionality:

Save rated usernames to a CSV file (username_ratings.csv) for easy reference.

Interactive Interface:

Stylish and user-friendly design with animations and buttons.

Prerequisites

Python Libraries:

ipywidgets

pandas

sklearn

nltk

Installation:

pip install ipywidgets pandas scikit-learn nltk

NLTK Word Corpus:

Ensure the NLTK word corpus is downloaded using the following command in Python:

import nltk
nltk.download("words")

How It Works

Username Generation:

Combines random adjectives and nouns to form a username.

Customization options allow including numbers and special characters.

User Ratings:

After generating a username, rate its quality (1-5 stars).

Ratings are stored and used to train the AI model.

AI Model:

A RandomForestRegressor predicts the quality of usernames.

The model retrains after every 5 ratings to improve its suggestions.

Exporting Data:

Save all rated usernames in username_ratings.csv for offline use.

Usage Instructions

Run the Script:

Execute the Python file in Jupyter Notebook or another environment supporting ipywidgets.

Interactive Widgets:

Adjust the number of letters in the username.

Toggle options to include numbers or special characters.

Click the "Generate Username" button to create a new username.

Rate Usernames:

Rate the generated username using the slider.

Click "Save Rating" to store the feedback and update the AI model.

Download Usernames:

Click the "Download Usernames" button to save rated usernames as a CSV file.

Code Highlights

Username Generation:

def generate_username(num_letters, include_number, include_special_char):
    adjective = random.choice(adjectives)
    noun = random.choice(nouns)
    combined = (adjective + noun)[:num_letters]
    number = str(random.randint(10, 99)) if include_number else ""
    special_char = random.choice("!@#$%^&*") if include_special_char else ""
    username = f"{combined}{number}{special_char}"
    return adjective, noun, number, special_char, username

AI Quality Prediction:

def predict_username_quality(adjective, noun, number, special_char):
    if len(data["Rating"]) < 5:
        return random.uniform(3, 5)
    try:
        return model.predict([[hash(adjective), hash(noun), int(number) if number else 0, hash(special_char) if special_char else 0]])[0]
    except NotFittedError:
        return random.uniform(3, 5)

Data Export:

def on_download_click(change):
    df = pd.DataFrame(data)
    df.to_csv("username_ratings.csv", index=False)
    with output_area:
        display(HTML("<p class='success-message'>💾 Usernames saved to 'username_ratings.csv'!</p>"))

Files

Main Script: The Python file implementing the username generator.

Exported Data: Rated usernames saved in username_ratings.csv.

Future Enhancements

Add more advanced AI models for enhanced predictions.

Integrate additional customization options (e.g., theme-based username generation).

Implement a standalone desktop or web application for broader accessibility.

