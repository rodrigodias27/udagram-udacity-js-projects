# Udagram API

- [Udagram API](#udagram-api)
  - [About The Project](#about-the-project)
  - [Built With](#built-with)
  - [Getting Started](#getting-started)
    - [Prerequisites](#prerequisites)
    - [Preparing](#preparing)
    - [Running server](#running-server)
  - [API documentation](#api-documentation)
  - [License](#license)

## About The Project

This application is a simple feed which is possible to create users and post to feed.

## Built With

- [Node](https://nodejs.org) - Javascript Runtime
- [Express](https://expressjs.com/) - Javascript API Framework

## Getting Started

### Prerequisites

- Node v14.15.1 (LTS) or more recent. While older versions can work it is advisable to keep node to latest LTS version
- npm 6.14.8 (LTS) or more recent, Yarn can work but was not tested for this project
- AWS CLI v2, v1 can work but was not tested for this project

### Preparing

- Install requirements
```bash
npm install
```
- Create a file named .env and write theese variables there:
```txt
# Environment
ENV=dev

# DATABASE CREDENTIALS
POSTGRES_HOST=127.0.0.1
POSTGRES_DB=postgres
POSTGRES_USERNAME=udagram
POSTGRES_PASSWORD=udagram123
POSTGRES_PORT=5432

# AWS
AWS_BUCKET=<name of s3 bucket>
AWS_ACCESS_KEY_ID=<programatic key id>
AWS_SECRET_ACCESS_KEY=<programatic access key>
AWS_REGION=<region>

# JWT CONFIG
JWT_SECRET=t9fnhHSV8qds

# APP
URL=http://locahost
PORT=8080
```

- Start database
  - If you are familiar with docker-compose you just need to run command
  ```bash
  docker-compose up
  ```
  Database will be served on http://localhost:5432

  - Or you can create database and user manually
  ```sql
  CREATE USER udagram;
  CREATE DATABASE postgres;
  GRANT ALL PRIVILEGES ON DATABASE postgres TO usagram;
  ```

### Running server

```bash
npm run dev
```
Server will be served on http://localhost:8080/api/v0/

## API documentation

API documentation in on file [./docs/API.md](./docs/API.md)

## License

[License](../LICENSE.txt)
