# YouTube Recommendations Feature

## Overview

The YouTube Recommendations feature allows users to get curated YouTube video suggestions based on their health symptoms and wellness concerns. This feature integrates seamlessly with the Arogya Wellness Assistant to provide additional educational resources.

## Features

- 📺 **Symptom-Based Recommendations**: Get YouTube videos tailored to specific health concerns
- 🎯 **Smart Query Mapping**: Automatically maps symptoms to relevant video search queries
- 🔗 **Direct YouTube Links**: One-click access to YouTube videos
- 📱 **Responsive Design**: Works on desktop, tablet, and mobile devices
- ⚡ **No API Key Required**: Works with built-in mock service (can be upgraded with YouTube API)

## Components

### Backend

#### `healthbackend/services/youtube_recommendations.py`

The core service for YouTube recommendations with two modes of operation:

**Mock Mode (Default)**:

- No API key required
- Provides search queries and links to YouTube search results
- Instantly available without external dependencies

**YouTube API Mode (Optional)**:

- Requires YouTube Data API v3 key
- Provides actual video metadata (thumbnails, descriptions, channel info)
- Higher quality results with video details

**Key Methods**:

```python
YouTubeRecommendationService.get_recommendations(symptom, max_videos=5)
# Returns: symptom, queries, and video recommendations

YouTubeRecommendationService.get_recommendations_with_youtube_api(symptom, api_key, max_videos=5)
# Returns: detailed video metadata from YouTube
```

### Frontend

#### `wellness-frontend/src/components/YouTubeRecommendations.jsx`

React component for displaying and fetching YouTube recommendations.

**Props**:

- `symptom` (string): The health symptom to get recommendations for
- `isVisible` (boolean): Whether to show the component by default (default: false)

**Features**:

- Toggle button to fetch recommendations
- Grid display of video cards
- Loading and error states
- Direct links to YouTube videos

#### `wellness-frontend/src/styles/YouTubeRecommendations.css`

Styling for the YouTube recommendations component with:

- YouTube-inspired color scheme (red accents)
- Responsive grid layout
- Smooth animations and transitions
- Mobile-optimized design

### API Endpoint

#### `POST /youtube-recommendations`

Fetches YouTube video recommendations for a given symptom.

**Request**:

```json
{
  "symptom": "fever",
  "max_videos": 5
}
```

**Response (Mock Mode)**:

```json
{
  "symptom": "fever",
  "queries": [
    "how to reduce fever naturally",
    "fever relief remedies",
    "fever management at home"
  ],
  "videos": [
    {
      "title": "Video: how to reduce fever naturally",
      "query": "how to reduce fever naturally",
      "searchUrl": "https://www.youtube.com/results?search_query=how+to+reduce+fever+naturally",
      "description": "Educational videos about how to reduce fever naturally",
      "type": "search_collection"
    }
  ]
}
```

**Response (YouTube API Mode)**:

```json
{
  "symptom": "fever",
  "queries": [...],
  "videos": [
    {
      "title": "How to Reduce Fever Naturally",
      "videoId": "abc123xyz",
      "url": "https://www.youtube.com/watch?v=abc123xyz",
      "thumbnail": "https://i.ytimg.com/vi/abc123xyz/medium.jpg",
      "description": "In this video...",
      "channelTitle": "Health Channel",
      "publishedAt": "2024-01-15T10:30:00Z"
    }
  ],
  "success": true
}
```

## Symptom-to-Query Mapping

The service includes built-in mappings for common symptoms:

| Symptom        | Search Queries                                                                             |
| -------------- | ------------------------------------------------------------------------------------------ |
| fever          | how to reduce fever naturally, fever relief remedies, fever management at home             |
| cough          | home remedies for cough, dry cough treatment, cough relief exercises                       |
| headache       | migraine relief exercises, tension headache remedies, headache treatment at home           |
| cold           | common cold natural remedies, flu vs cold treatment, cold recovery tips                    |
| blood_pressure | high blood pressure management, hypertension natural remedies, blood pressure control diet |
| diabetes       | diabetes management, blood sugar control diet, diabetes prevention tips                    |
| anxiety        | anxiety relief techniques, breathing exercises for anxiety, meditation for anxiety         |
| yoga           | beginner yoga for flexibility, yoga for stress relief, morning yoga routine                |
| And more...    | See complete mapping in youtube_recommendations.py                                         |

## Usage

### For Users

1. **Enter Symptoms**: In the WellnessPage, enter your health concerns in the "Your Current Health Concern" section
2. **Click "YouTube Recommendations"**: A button appears below the form
3. **View Videos**: Click the button to see recommended YouTube videos for your symptom
4. **Watch Videos**: Click "Watch on YouTube" to open the video in a new tab

### For Developers

#### Using Mock Mode (Default)

```python
from healthbackend.services.youtube_recommendations import YouTubeRecommendationService

# Get recommendations
recommendations = YouTubeRecommendationService.get_recommendations("fever", max_videos=5)
print(recommendations)
```

#### Using YouTube API Mode

1. **Get YouTube API Key**:

   - Go to [Google Cloud Console](https://console.cloud.google.com)
   - Create a project and enable YouTube Data API v3
   - Create an API key

2. **Update Backend**:

```python
# Add to .env
YOUTUBE_API_KEY=your_api_key_here

# In app.py
from healthbackend.config.settings import YOUTUBE_API_KEY

# Update endpoint to use API mode
recommendations = YouTubeRecommendationService.get_recommendations_with_youtube_api(
    symptom=symptom,
    api_key=YOUTUBE_API_KEY,
    max_videos=max_videos
)
```

## Integration with WellnessPage

The YouTube recommendations component is integrated into the WellnessPage component:

```jsx
<YouTubeRecommendations symptom={symptoms} isVisible={false} />
```

This displays a button next to the "Generate Guidance" button that users can click to fetch recommendations.

## Customization

### Add New Symptom Mappings

Edit `youtube_recommendations.py` to add new symptom mappings:

```python
SYMPTOM_TO_QUERIES = {
    "your_symptom": [
        "search query 1",
        "search query 2",
        "search query 3"
    ],
    # ... existing mappings
}
```

### Styling

Customize the look by modifying `YouTubeRecommendations.css`:

- **Colors**: Update gradient colors in `.youtube-recommendations-btn`, `.watch-btn`
- **Layout**: Modify `grid-template-columns` in `.videos-grid`
- **Sizes**: Adjust padding, margins, and font sizes as needed

### Video Count

Change the default number of videos displayed:

```jsx
// In WellnessPage.jsx or where component is used
<YouTubeRecommendations symptom={symptoms} maxVideos={10} />
```

And update the component to accept the prop:

```jsx
function YouTubeRecommendations({ symptom, isVisible = false, maxVideos = 5 }) {
  // ... update fetch call to use maxVideos
}
```

## Error Handling

The component handles various error scenarios:

- **No symptom entered**: Shows message to enter symptom first
- **Network errors**: Displays error message with retry button
- **Empty results**: Shows message and retry option
- **API failures**: Gracefully falls back with user-friendly messages

## Performance Considerations

- **Client-side caching**: Results are cached in component state
- **Lazy loading**: Videos are only fetched when user clicks the button
- **Responsive images**: YouTube provides optimized thumbnail sizes
- **No blocking calls**: Async operations prevent UI freezing

## Future Enhancements

1. **YouTube API Integration**: Upgrade to use official YouTube API for better metadata
2. **Video Categories**: Filter by educational, medical, yoga, fitness, etc.
3. **Favorites**: Allow users to save favorite videos
4. **Playlists**: Create personalized wellness playlists
5. **Transcripts**: Display video transcripts for better accessibility
6. **User Ratings**: Show community ratings and comments
7. **Language Support**: Multi-language video recommendations

## Troubleshooting

### Videos not loading?

1. Check browser console for errors (F12 → Console)
2. Verify backend is running and `/youtube-recommendations` endpoint is accessible
3. Ensure symptom field is not empty
4. Try clicking "Try Again" or refresh the page

### Want actual YouTube video metadata?

1. Get a YouTube Data API key from Google Cloud Console
2. Add it to your `.env` file as `YOUTUBE_API_KEY`
3. Update the endpoint to use `YouTubeRecommendationService.get_recommendations_with_youtube_api()`

### Component not appearing?

1. Ensure `YouTubeRecommendations.jsx` is imported in WellnessPage
2. Check that CSS file is imported
3. Verify the component is included in JSX render

## Files Modified/Created

```
healthbackend/
  ├── app.py (modified - added endpoint and import)
  └── services/
      └── youtube_recommendations.py (created)

wellness-frontend/
  ├── src/
  │   ├── components/
  │   │   ├── WellnessPage.jsx (modified - added component)
  │   │   └── YouTubeRecommendations.jsx (created)
  │   └── styles/
  │       └── YouTubeRecommendations.css (created)
```

## API Quota & Limits

**Mock Mode**: Unlimited (no external calls)

**YouTube API Mode** (if upgraded):

- Free tier: 10,000 quota units per day
- Each search request costs ~100 units
- Allows ~100 requests per day with free tier

For high-volume applications, consider YouTube API paid tier.
