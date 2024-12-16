# Uptime-Kuma-Web-API 🚀

## A REST API wrapper for [Uptime Kuma](https://github.com/louislam/uptime-kuma) using [Uptime-Kuma-API](https://github.com/lucasheld/uptime-kuma-api)

Forked from [Uptime Kuma Web API](https://github.com/eoNaho/Uptime-Kuma-Web-API) 🌱

---

## Endpoints 📡

![Alt text](./images/1.png)
![Alt text](./images/2.png)

---

## How to use it ⚙️

### Environment Variables 🌍

#### Required 🔑
You must define these ENV VARS to connect to your KUMA server.

- **KUMA_SERVER**: The URL of your Uptime Kuma instance. ex: `https://uptime.example.com`
- **KUMA_USERNAME**: The username of your Uptime Kuma user
- **KUMA_PASSWORD**: The password of your Uptime Kuma user
- **ADMIN_PASSWORD**: An admin password to access the API

#### Optional ⚡
Additional configuration variables:

- **ACCESS_TOKEN_EXPIRATION**: Minutes the access token should be valid. Defaults to 8 days.
- **SECRET_KEY**: A secret value to encode JWTs with

#### Note 📝:
Make sure to define your **ADMIN_PASSWORD**. Without it, you won’t be able to connect to the API.

You'll connect with the following credentials:

- **username** = admin
- **password** = `<ADMIN_PASSWORD>`

---

### Features ✨

- Multi-user Kuma API (without privilege yet) with a small SQLite database
- Easy to use REST API with most of the Uptime-Kuma features
- Swagger Docs for quick reference 📚
- Dockerized [UptimeKuma_RestAPI Image](https://hub.docker.com/repository/docker/medaziz11/uptimekuma_restapi)
- Multi-architecture support (amd64, arm64) ⚙️

---

### Example Docker Compose 🐳

You can create a Docker Compose file like this:

```yaml
version: "3.9"
services:
  kuma:
    container_name: uptime-kuma
    image: louislam/uptime-kuma:latest
    ports:
      - "3001:3001"
    restart: always
    volumes:
      - uptime-kuma:/app/data

  api:
    container_name: backend
    image: medaziz11/uptimekuma_restapi
    volumes:
      - api:/db
    restart: always
    environment:
      - KUMA_SERVER=http://kuma:3001
      - KUMA_USERNAME=test
      - KUMA_PASSWORD=123test.
      - ADMIN_PASSWORD=admin
    depends_on:
      - kuma
    ports:
      - "8000:8000"

volumes:
  uptime-kuma:
  api:
```

In order for the example to work, make sure to run **Kuma** first, create your Kuma username and password, and then re-run the Docker Compose file.

---

### Example CURL Script 📝

```bash

    TOKEN=$(curl -X -L 'POST' -H 'Content-Type: application/x-www-form-urlencoded' --data 'username=admin&password=admin' http://127.0.0.1:8000/login/access-token/ | jq -r ".access_token")

    curl -L -H 'Accept: application/json' -H "Authorization: Bearer ${TOKEN}" http://127.0.0.1:8000/monitors/

```

---

## Roadmap 📅

- [x] 🌱 Initial setup and integration with Uptime Kuma
- [x] 🛠️ Basic authentication and access control
- [x] 🕒 Modify cron jobs for improved scheduling and management
- [ ] 🚀 Add privilege support for multi-user authentication
- [ ] 🧑‍💻 Improve API documentation with additional examples
- [ ] 🔒 Add more security features (rate limiting, IP whitelisting)
- [ ] 🔧 Performance optimizations for handling larger datasets

---

## Links 🔗

- Original GitHub Repository: [Uptime Kuma](https://github.com/louislam/uptime-kuma) 🔥
- Original API Wrapper GitHub: [Uptime-Kuma-Web-API](https://github.com/eoNaho/Uptime-Kuma-Web-API) 🍴
- Docker Hub Image: [medaziz11/uptimekuma_restapi](https://hub.docker.com/repository/docker/medaziz11/uptimekuma_restapi) 🐳
```