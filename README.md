# Music-Recommender-System

![CI](https://github.com/aayxshkumar/music-recommender/actions/workflows/ci.yml/badge.svg)

Music recommendation notebook built on a Spotify track dataset and the Spotify Web API. It was my 4th-semester university project.

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/aayxshkumar/music-recommender/blob/main/Aayush_Kumar's_Recommender.ipynb)

## What the notebook does

- Loads Spotify track and genre CSVs and adds a decade column to the tracks.
- Standardises the audio features of the genre data, groups genres into 10 k-means clusters and plots them in 2D with t-SNE (plotly).
- Groups songs into 20 k-means clusters and plots them in 2D with PCA.
- Looks up songs by name through the Spotify Web API ([spotipy](https://spotipy.readthedocs.io/)), averages their audio features and recommends the dataset songs closest to that average by cosine distance.

## Requirements

- Google Colab, or Jupyter with Python 3. The notebook was last saved with Python 3.9.7; CI checks its imports on Python 3.12 with the versions in `requirements.txt`.
- The dataset: the notebook reads `data.csv`, `data_w_genres.csv`, `data_by_year.csv` and `data_by_artist.csv` from a `spotify_data/` folder. These file names match the Kaggle dataset [vatsalmavani/spotify-dataset](https://www.kaggle.com/datasets/vatsalmavani/spotify-dataset), which needs a Kaggle account to download. The data is not included in this repo.
- Spotify API credentials: create an app in the [Spotify developer dashboard](https://developer.spotify.com/dashboard) and set `SPOTIPY_CLIENT_ID` and `SPOTIPY_CLIENT_SECRET` (names in `.env.example`).

The song lookup calls Spotify's Audio Features endpoint. Spotify [restricted that endpoint for new apps in November 2024](https://developer.spotify.com/blog/2024-11-27-changes-to-the-web-api), so the recommendation cells may fail with a newly created app.

## Setup and usage

```bash
git clone https://github.com/aayxshkumar/music-recommender.git
cd music-recommender
python3 -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
```

Put the CSVs in `spotify_data/`, set the two Spotify variables in the environment the notebook runs in (in a notebook cell, `%env SPOTIPY_CLIENT_ID=...` works), then open `Aayush_Kumar's_Recommender.ipynb`. In Colab the notebook mounts Google Drive; skip that cell when running locally.

## CI

CI installs `requirements-dev.txt`, validates the notebook JSON with nbformat and checks that every library the notebook imports can be imported. It does not run the notebook.
