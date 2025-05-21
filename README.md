# IMT_542_G8
# RomCom Discovery Information Structure Documentation

## About

This information system is designed to help users who love romantic comedy movies discover titles based on emotional states, personal preferences, and social signals. It targets a broad audience seeking family-friendly (G, PG, PG-13) rom-coms for entertainment, mood uplift, or community connection through shared experiences. Users can access movie metadata, mood tags, user-generated reviews, and participate in recommendation threads for a personalized discovery journey.

## Methodology

- Metadata is aggregated from trusted movie APIs such as TMDb and OMDb.
- Controlled vocabularies and taxonomies are defined for moods, genres, ratings, and platform availability to ensure consistent tagging.
- A NoSQL database (MongoDB or Firebase Firestore) is used to flexibly store movies, user data, and dynamic tags.
- Community contributions enrich the dataset via reviews, mood tags, and recommendation threads.
- RESTful API endpoints expose movie metadata, user preferences, and reviews.
- Authentication is managed with Firebase Auth or OAuth2 providers to secure user data.
- Search capabilities use Algolia or ElasticSearch for fuzzy matching and mood-based queries.
- The system is hosted on cloud platforms like Firebase or AWS for scalability and reliability.
- Frontend is built using React.js or a similar responsive framework to support multiple devices.

## Access

Users can interact with the system through the following steps:

1. Visit the homepage to browse featured romantic comedies and use mood-based filters.
2. Use the search page to find movies by mood, platform, or memory keywords (e.g., “cozy,” “Netflix,” “red-haired lead”).
3. Navigate to movie detail pages displaying metadata, user reviews, and mood tags.
4. Register or log in to save favorites, customize mood preferences, and contribute to community discussions.
5. Submit reviews and add mood tags to improve the recommendation engine.
6. Third-party developers can query the RESTful API endpoints for programmatic access to movie and user data.
7. API requests and responses use standard JSON formatting for easy integration.

## Structure

### Media Items Schema

| Field               | Description                    | Controlled Vocabulary / Input Type                      |
|---------------------|-------------------------------|---------------------------------------------------------|
| Title               | Movie title                   | Free text                                               |
| Summary             | Brief plot overview           | Free text                                               |
| Year                | Year of release               | YYYY format                                            |
| Director(s)         | Film directors                | Free text (optionally authority-controlled)            |
| Main Characters     | Protagonists and key roles    | Free text                                              |
| Rating              | MPAA content rating           | G, PG, PG-13                                           |
| Average Rating      | Community-generated score     | Numeric (e.g., 1–5 stars)                              |
| Mood Tags           | Emotional tone or situational | Cozy, Empowering, Post-breakup, Light-hearted, etc.    |
| Platform Availability | Streaming platforms          | Netflix, Hulu, Tubi, Amazon Prime, YouTube, etc.       |
| Genre Tags          | Romantic comedy sub-genres    | Classic, Teen, Holiday, LGBTQ+, Musical, etc.           |
| User Reviews        | Community-contributed reviews | Free text with optional mood/genre tags                 |

### User Schema

| Field               | Description                   | Controlled Vocabulary / Input Type                      |
|---------------------|-------------------------------|---------------------------------------------------------|
| Username            | Unique user identity          | Alphanumeric                                           |
| Saved List          | Watchlist or favorites        | Linked media items                                     |
| Mood Preferences    | Personalized mood filters     | Selected from Mood Tags                                |
| Review Tags         | Emotional tags on reviews     | Same as Mood Tags                                     |
| Thread Contributions | Community recommendations    | Linked to movie or mood contexts                        |

## Example Request & Response

### Request

```http
GET /api/movies?mood=Cozy HTTP/1.1
Host: yourapi.example.com
Accept: application/json

{
  "movies": [
    {
      "title": "Love Actually",
      "summary": "Follows the lives of eight very different couples in dealing with their love lives during a frantic month before Christmas in London.",
      "year": "2003",
      "directors": ["Richard Curtis"],
      "main_characters": ["Hugh Grant", "Liam Neeson", "Emma Thompson"],
      "rating": "PG-13",
      "average_rating": 4.5,
      "mood_tags": ["Cozy", "Holiday", "Hopeful"],
      "platform_availability": ["Netflix", "Amazon Prime"],
      "genre_tags": ["Classic", "Holiday"],
      "user_reviews": [
        {
          "username": "romcomFan99",
          "review": "Perfect feel-good movie for the holidays!",
          "tags": ["Cozy", "Hopeful"]
        }
      ]
    }
  ]
}

