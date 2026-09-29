# AI Username Generator

An interactive notebook tool that generates usernames from dictionary words, collects your ratings, and learns to predict how much you'll like new ones.

**Live demo:** https://username-generator-web.vercel.app

## Features
- Builds usernames as *Adjective + noun* from the NLTK `words` corpus, cut to the number of letters you choose
- Optional two-digit number and special character (`!@#$%^&*`)
- Shows a predicted quality score (★) for each username
- Rate usernames from 1 to 5; after more than 5 ratings the model is retrained on your feedback
- Save and download your rated usernames as `username_ratings.csv`

## Tech stack
- **Notebook:** Python, ipywidgets, NLTK, pandas, scikit-learn `RandomForestRegressor` (`ai_username_generator.ipynb`)
- **Web version:** HTML, CSS and JavaScript (`web/`). It uses a 10,000-word sample of the NLTK list. Instead of the random forest on hashed words, it uses a small k-nearest-neighbour regressor running in the browser. As in the notebook, the score is random between 3 and 5 until you have 5 ratings.

## Run locally
```bash
pip install nltk pandas scikit-learn ipywidgets notebook
jupyter notebook ai_username_generator.ipynb
```
Web version: serve the `web/` folder, e.g. `npx serve web`. It needs a server because it loads `words.json`.

---

Portfolio: [khuwaish-portfolio.vercel.app](https://khuwaish-portfolio.vercel.app) · Built by **Khuwaish Goyal**
