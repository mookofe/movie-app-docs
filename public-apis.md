#Public API Endpoints
###**List of endpoints:**

|URL|Method|Description|
---|---|---
**Authentication:**||
[https://apis.sans-movies.org/authentication/v1/login](#authenticate-user)|POST|Authenticate User
**Movies:**||
https://apis.sans-movies.org/movies/v1/movies|GET|Get list of movies
https://apis.sans-movies.org/movies/v1/movies|POST|Create movie
https://apis.sans-movies.org/movies/v1/movies/{id}|GET|Get movie details
https://apis.sans-movies.org/movies/v1/movies/{id}|PUT|Update Movie
https://apis.sans-movies.org/movies/v1/movies/{id}|DELETE|Delete Movie


---
###Authenticate user:

```
POST https://apis.sans-movies.org/authentication/v1/login
```

**Payload:**

```
{
	"email": "admin@sans-movies.org",
	"password": "Passw0rd"
}
```

**Response:**

```
{
    "accessToken": "eyJraWQiOiI0XC9...",
    "expiresIn": 3600,
    "tokenType": "Bearer",
    "refreshToken": "eyJjdHkiOiJKV1QiLCJlbm...",
    "idToken": "eyJraWQiOiJXeEE5c2hLMVNI..."
}
```
---

###Get list of movies:
```
GET https://apis.sans-movies.org/movies/v1/movies?orderBy=releaseYear&orientation=asc&skip=0&limit=10
```

**Headers:**

Name|Type|Required|Description
---|---|---|---
Authorization|String|Yes| idToken from authentication endpoint

**Query Parameters:**

Name|Type|Required|Acepted values|Default|Description
---|---|---|---|---|---
orderBy|String|No|title,format,length,releaseYear,rating||Column name you want to order the list of movies
orientation|String|No|asc,desc||Ordering orientation, ascending or descending
skip|Integer|No|> 0|0|Number of rows to skip
limit|Integer|No|1-100|20|Number of rows to retreive

**Response:**

```
{
    "data": [
        {
            "id": 1,
            "title": "The Terminator",
            "format": "DVD",
            "length": 107,
            "releaseYear": 1984,
            "rating": 4
        },
        {
            "id": 2,
            "title": "Terminator 2: Judgment Day",
            "format": "DVD",
            "length": 137,
            "releaseYear": 1991,
            "rating": 5
        }
    ],
    "meta": {
        "skipped": 0,
        "totalRows": 2
    }
}
```
---
###Create movie:
```
POST https://apis.sans-movies.org/movies/v1/movies
```

**Headers:**

Name|Type|Required|Description
---|---|---|---
Authorization|string|Yes| idToken from authentication endpoint

**Payload:**

```
{
    "title": "Terminator 2: Judgment Day",
    "format": "DVD",
    "length": 137,
    "releaseYear": 1991,
    "rating": 5
}
```

**Body Parameters:**

Name|Type|Required|Acepted values|Default|Description
---|---|---|---|---|---
title|String|Yes|Lenth length between 1 and 50 characters]||Movie title
format|String|Yes|["VHS", "DVD", "Streaming"]||Movie format
length|Integer|Yes|0-500||Movie length in minutes
releaseYear|Integer|Yes|1800-2100||Movie release year
rating|Integer|Yes|1-5||Movie rating

**Response:**

```
{
    "id": 2,
    "title": "Terminator 2: Judgment Day",
    "format": "DVD",
    "length": 137,
    "releaseYear": 1991,
    "rating": 5,
    "metadata": {
        "rated": "R",
        "dateReleased": "1991-07-03T00:00:00+00:00",
        "genre": "Action, Sci-Fi",
        "director": "James Cameron",
        "writers": "James Cameron, William Wisher",
        "plot": "A cyborg, identical to the one who failed to kill Sarah Connor, must now protect her teenage son, John Connor, from a more advanced and powerful cyborg.",
        "posterUrl": "https://m.media-amazon.com/images/M/MV5BMGU2NzRmZjUtOGUxYS00ZjdjLWEwZWItY2NlM2JhNjkxNTFmXkEyXkFqcGdeQXVyNjU0OTQ0OTY@._V1_SX300.jpg",
        "imdbRating": 8.5,
        "rottenTomatoesRating": 93,
        "boxOffice": 198116802
    }
}
```

---

###Get movie details
```
GET https://apis.sans-movies.org/movies/v1/movies/{id}
```

**Headers:**

Name|Type|Required|Description
---|---|---|---
Authorization|string|Yes| idToken from authentication endpoint

**Query Parameters:**

Name|Type|Required|Description
---|---|---|---|---|---
id|Integer|Yes|Movie identifier

**Response:**

```
{
    "id": 2,
    "title": "Terminator 2: Judgment Day",
    "format": "DVD",
    "length": 137,
    "releaseYear": 1991,
    "rating": 5,
    "metadata": {
        "rated": "R",
        "dateReleased": "1991-07-03T00:00:00+00:00",
        "genre": "Action, Sci-Fi",
        "director": "James Cameron",
        "writers": "James Cameron, William Wisher",
        "plot": "A cyborg, identical to the one who failed to kill Sarah Connor, must now protect her teenage son, John Connor, from a more advanced and powerful cyborg.",
        "posterUrl": "https://m.media-amazon.com/images/M/MV5BMGU2NzRmZjUtOGUxYS00ZjdjLWEwZWItY2NlM2JhNjkxNTFmXkEyXkFqcGdeQXVyNjU0OTQ0OTY@._V1_SX300.jpg",
        "imdbRating": 8.5,
        "rottenTomatoesRating": 93,
        "boxOffice": 198116802
    }
}
```

---
###Update movie:
```
PUT https://apis.sans-movies.org/movies/v1/movies/2
```

**Headers:**

Name|Type|Required|Description
---|---|---|---
Authorization|string|Yes| idToken from authentication endpoint

**Payload:**

```
{
    "title": "Terminator 2: Judgment Day",
    "format": "DVD",
    "length": 137,
    "releaseYear": 1991,
    "rating": 5
}
```

**Body Parameters:**

Name|Type|Required|Acepted values|Default|Description
---|---|---|---|---|---
title|String|Yes|Lenth length between 1 and 50 characters]||Movie title
format|String|Yes|["VHS", "DVD", "Streaming"]||Movie format
length|Integer|Yes|0-500||Movie length in minutes
releaseYear|Integer|Yes|1800-2100||Movie release year
rating|Integer|Yes|1-5||Movie rating

**Response:**

```
{
    "id": 2,
    "title": "Terminator 2: Judgment Day",
    "format": "DVD",
    "length": 137,
    "releaseYear": 1991,
    "rating": 5,
    "metadata": {
        "rated": "R",
        "dateReleased": "1991-07-03T00:00:00+00:00",
        "genre": "Action, Sci-Fi",
        "director": "James Cameron",
        "writers": "James Cameron, William Wisher",
        "plot": "A cyborg, identical to the one who failed to kill Sarah Connor, must now protect her teenage son, John Connor, from a more advanced and powerful cyborg.",
        "posterUrl": "https://m.media-amazon.com/images/M/MV5BMGU2NzRmZjUtOGUxYS00ZjdjLWEwZWItY2NlM2JhNjkxNTFmXkEyXkFqcGdeQXVyNjU0OTQ0OTY@._V1_SX300.jpg",
        "imdbRating": 8.5,
        "rottenTomatoesRating": 93,
        "boxOffice": 198116802
    }
}
```

---
###Delete movie:
```
DELETE https://apis.sans-movies.org/movies/v1/movies/2
```

**Headers:**

Name|Type|Required|Description
---|---|---|---
Authorization|string|Yes| idToken from authentication endpoint


**Response:**

```
Status: 204 No Content
```