## RSS FEED COLLECTOR

In this project, I created a simple RSS feed collector with `Django` and `GraphQL`. It allows users to create an account and add RSS feed sources then it retruns the latest posts by periodically fetching them. I used `Redis` and `Celery` for background tasks and `docker` for deploy. This project aim is to provide only the back-end part.

## Requirements
 * Docker and Docker Compose

## Setting up the Project

```bash
sudo docker compose up --build
```

For refreshing feed manually:
```bash
docker compose exec web python3 manage.py refreshfeeds
```

## GraphQL
some curl example for graphql:
```bash
curl http://localhost:/graphql -H "Authorization: JWT $token" -d query="query { oneFeed(sourceId: $id) {title } }"

curl http://localhost:/graphql -H "Authorization: JWT $token" -d query="query allSources { allSources { name, id } }"

curl http://localhost:/graphql -H "Authorization: JWT $token" -d query='mutation addSource { addSource(input: { feedUrl: "https://rss.art19.com/apology-line"}) { ok } }'
```

Some graphql example query:

```bash
mutation createUser {
  createUser(username: "<your_username>", password: "<your_password>", email: "<your_email>") {
    token
    user {
      username
    }
  }
}

mutation verifyToken {
  verifyToken(token: "<your_token>") {
    payload
  }
}

mutation refreshToken {
  refreshToken(refreshToken: "<refresh_token>") {
    token
  }
}

mutation loginUser {
  tokenAuth(username: "<username>", password: "<password>") {
    token
  }
}

mutation addSource {
  addSource(token: "<your_token>") {
    ok
  }
}

mutation remvoeSource {
  remvoeSource(feedUrl: "<feed_url>") {
    ok
  }
}

query allSources {
  allSources
  {
    name,
    id
  }
}
```

## Contribution

Feel free to raise a issue or make a pull request to fix a bug or add a new feature.