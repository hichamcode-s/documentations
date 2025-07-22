    High performance and availablility API designed for generating YouTube video transcripts.

- How It Works :

   Send a POST request to the API with a single parameter: the url of the YouTube video. The API will process the video and return a full response that includes:

- [x] Transcript text with time-coded segments
- [x] Video title, duration, and upload date
- [x] Channel name and subscriber count
- [x] Video thumbnail and engagement stats (likes, views)
- [x] Combined plain-text transcript for easy indexing or summarization

If the video contains no transcript or captions, the API will indicate this in the response, along with a success flag for each video processed.

- Request Format
   - ```POST /youtube-transcript  ```
   - ```Content-Type: application/json  ```
   - ```Body { "url": "https://www.youtube.com/watch?v=example" } ```

- Response Example 
``` 
{
  "success": true,
  "playlistTitle": "...",
  "videoCount": 1,
  "transcriptionResults": [
    {
      "videoId": "abc123",
      "videoTitle": "...",
      "thumbnail": "...",
      "channelTitle": "...",
      "channelSubscribers": "...",
      "viewCount": "...",
      "likeCount": 359,
      "duration": 5397,
      "durationFormatted": "1:29:57",
      "uploadDate": "Jul 21, 2025",
      "hasTranscript": true,
      "success": true,
      "transcript": [
        {
          "text": "...",
          "offset": 0.28,
          "duration": 5.76
        }
      ]
    }
  ],
  "combinedText": "...",
  "source": "video"
} 
```