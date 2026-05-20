# Chronos-Reader
# Political Ad Performance Predictor

A machine learning pipeline that collects historical political ad data, extracts features, and predicts how a new draft ad will perform before it goes public.

## Project Structure

```
political-ad-ml/
├── data/
│   ├── raw/
│   │   └── videos/         # Downloaded video files
│   └── processed/          # Cleaned CSVs ready for training
├── scripts/
│   ├── collect_youtube.py  # Pull video IDs + metrics from YouTube
│   ├── collect_facebook.py # Pull ads from Facebook Ad Library
│   ├── download_videos.py  # Download video files locally
│   └── clean_data.py       # Validate and clean the dataset
├── .env.example
├── requirements.txt
└── README.md
```

## Setup

### 1. Clone the repo

```bash
git clone https://github.com/YOUR_USERNAME/political-ad-ml.git
cd political-ad-ml
```

### 2. Install dependencies

```bash
pip install -r requirements.txt
```

### 3. Configure API keys

Copy the example env file and fill in your keys:

```bash
cp .env.example .env
```

Then edit `.env` with your credentials:

- **YouTube API Key**: Get one at [Google Cloud Console](https://console.cloud.google.com). Enable the YouTube Data API v3.
- **Facebook Access Token**: Apply for access at [Facebook Ad Library API](https://www.facebook.com/ads/library/api).

### 4. Run the pipeline in order

```bash
python scripts/collect_youtube.py
python scripts/collect_facebook.py
python scripts/download_videos.py
python scripts/clean_data.py
```

After running all four scripts, you will have:
- `data/raw/video_ids.csv` — raw YouTube search results
- `data/raw/fb_ads.csv` — Facebook political ad data
- `data/raw/videos/` — downloaded MP4 files
- `data/processed/clean_dataset.csv` — final cleaned dataset ready for Phase 2

## API Rate Limits

- YouTube Data API v3 has a daily quota of 10,000 units. Each search costs 100 units and each video metrics call costs 1 unit per video.
- Facebook Ad Library API allows up to 200 requests per hour.

## Notes

- Only videos between 15 seconds and 5 minutes are kept, filtering out non-ad content.
- Videos with zero views are dropped as they are likely private or removed.
- The Facebook data only returns impression and spend ranges, not exact numbers.

## Coming Soon

- Phase 2: Feature extraction (visual embeddings, transcription, emotion detection)
- Phase 3: Model training
- Phase 4: Draft video prediction interface
