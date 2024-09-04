# RSS FEED AGGREGATOR

This repository contains an RSS Feed Aggregator built using Go and PostgreSQL. The application aggregates RSS feeds from various sources, stores them in a PostgreSQL database, and provides an API to access and manage the feeds. The API can be tested using Postman.

## Features
- Aggregates RSS feeds from multiple sources.
- Stores feed data in a PostgreSQL database.
- Provides RESTful API endpoints for managing and accessing feeds.
- Supports operations like adding, updating, and deleting RSS feeds.
- Fetches the latest articles from subscribed feeds.
- Built with Go for high performance and concurrency.

## Prerequisites

1. [Go](https://go.dev/doc/install) (version 1.22 or later)
    ```bash
    $ wget https://go.dev/dl/go1.22.5.linux-amd64.tar.gz
    $ rm -rf /usr/local/go && tar -C /usr/local -xzf go1.23.0.linux-amd64.tar.gz
    $ export PATH=$PATH:/usr/local/go/bin
    $ go version
    ```

2. [PostgreSQL](https://www.postgresql.org/download/) (version 12 or later)
    ```bash
    $ sudo apt install postgresql postgresql-contrib
    $ sudo apt-get install pgadmin3
    $ psql --version
    ```

3. [Postman](https://www.postman.com/downloads/) (for API testing)
    ```
    $ curl -o- "https://dl-cli.pstmn.io/install/linux64.sh" | sh
    ```

### Steps to Run and Test the Application

1. #### Initialize the project

    ```bash
    $ go mod init github.com/roni-boiz/rss-aggregator
    ```

2. #### Install Dependencies
    ```bash
    go get github.com/joho/godotenv
    go get github.com/go-chi/chi
    go get github.com/go-chi/cors
    go install github.com/sqlc-dev/sqlc/cmd/sqlc@latest
    go install github.com/pressly/goose/v3/cmd/goose@latest
    ```

3. #### Import Dependencies
    ```bash
    $ go mod vendor
    $ go mod tidy
    ```

4. #### Generate SQL files
    ```
    $ sqlc generate
    ```

    #### Inside ./sql/schema
    
    ```
    $ goose postgres postgres://rssauthuser:postgres@localhost:5432/rssagg up
    ```

5. #### Run the project

    ```bash
    $ go build
    $ go run .
    - or -
    $ go build && ./rss-aggregator
    ```

> [!NOTE]
> Make sure to update **username** and **password** of postgres database in the `DB_URL` in `.env` file

6. #### Connect to databse

    ```bash
    $ sudo -u postgres psql -d rssagg
    ```

7. #### API Requests

    1. #### HEALTH

        image

    2. #### ERROR

        image

    3. #### Users

        POST

        image

        GET

        image


    4. #### Feeds

        POST
        
        image

        GET

        image

    5. #### Feed Follows

        POST

        image
        
        GET

        image

        DELETE

        image

    6. #### Post

        GET 

        image


8. #### Delete SQL files

    #### Inside ./sql/schema
    
    ```
    $ goose postgres postgres://rssauthuser:postgres@localhost:5432/rssagg down
    ```

> [!NOTE]
> Need to execute above command multiple time to delete all the SQL resources.
