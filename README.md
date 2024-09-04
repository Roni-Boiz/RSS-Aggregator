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
    $ go get github.com/joho/godotenv
    $ go get github.com/go-chi/chi
    $ go get github.com/go-chi/cors
    $ go install github.com/sqlc-dev/sqlc/cmd/sqlc@latest
    $ go install github.com/pressly/goose/v3/cmd/goose@latest
    ```

3. #### Import Dependencies
    ```bash
    $ go mod vendor
    $ go mod tidy
    ```

4. #### Generate SQL Schemas
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

        ![healthz](https://github.com/user-attachments/assets/49016aaf-4780-4182-9704-223b3d5e45bd)

    2. #### ERROR

        ![err](https://github.com/user-attachments/assets/fa19a486-45fb-4e5d-a493-8a02b8704066)

    3. #### USERS

        POST

        ![users_post](https://github.com/user-attachments/assets/46aa1fa6-1349-4d30-bddc-779cea2a26a7)

        GET

        ![users_get](https://github.com/user-attachments/assets/9e908d92-0809-46ae-8b58-30897d61f965)

    4. #### FEEDS

        POST
        
        ![feeds_post](https://github.com/user-attachments/assets/f86d92c0-8e75-49b2-9cde-a076962da1e4)

        GET

        ![feeds_get](https://github.com/user-attachments/assets/74388701-2816-4f80-8b84-08fe3a4efe6c)


    5. #### FEED FOLLOWS

        POST

        ![feedfollows_post](https://github.com/user-attachments/assets/2f23c388-40bf-41b2-80d8-02ac99fee27e)
        
        GET

        ![feedfollows_get](https://github.com/user-attachments/assets/0c112c3f-b560-4947-a314-680a940c304a)

        DELETE

        ![feedfollows_delete](https://github.com/user-attachments/assets/2b8c387a-2b16-4c4b-9127-6c8fcf2f7202)

    6. #### POST

        GET 

        ![posts_get](https://github.com/user-attachments/assets/cefda5f5-8583-47a2-970f-b81528375373)


8. #### Delete SQL files

    #### Inside ./sql/schema
    
    ```
    $ goose postgres postgres://rssauthuser:postgres@localhost:5432/rssagg down
    ```

> [!NOTE]
> Need to execute above command multiple time to delete all the SQL schemas.
