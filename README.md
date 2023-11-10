<h1 align="center">💸 Canine Club Invoicing System 💸</h1>
<p align="center">
    <a href="https://github.com/scottmckendry/ccinvoice/actions/workflows/test.yml">
        <img alt="GitHub Workflow Status (with event)" src="https://img.shields.io/github/actions/workflow/status/scottmckendry/ccinvoice/test.yml?style=for-the-badge&logo=github&label=CI&color=%237dcfff">
    </a>
    <a href="https://github.com/scottmckendry/ccinvoice/actions/workflows/deploy.yml">
        <img alt="GitHub Workflow Status (with event)" src="https://img.shields.io/github/actions/workflow/status/scottmckendry/ccinvoice/test.yml?style=for-the-badge&logo=github&label=CD&color=%23bb9af7">
    </a>
    <a href="https://github.com/scottmckendry/ccinvoice/blob/main/LICENSE">
        <img alt="License" src="https://img.shields.io/github/license/scottmckendry/ccinvoice?style=for-the-badge&logo=github&color=%239ece6a">
    </a>
</p>

<p align="center">
    A mobile-first web application I built for my wife's dog-walking business. Built with <a href="https://go.dev">Go</a> and <a href="https://htmx.org">HTMX</a><br><br>
    <img alt="demo" src="https://github.com/scottmckendry/ccinvoice/assets/39483124/cccc727d-b9b2-419b-9766-20116f1b2c87">
</p>

## 🚀 Deploying
To run the app in a docker container, you'll need to create a `.env` file in the root directory with the following environment variables:
```env
SMTP_HOST=smtp.example.com
SMTP_PORT=587
SMTP_USER=john@example.com
SMTP_PASS=P@ssw0rd
FROM_NAME=John Doe
FROM_ADDRESS=4 Privet Drive, Little Whinging, Surrey
FROM_CITY=London
ACCOUNT_NUMBER=12-3456-7890123-45
BASE_URL=http://invoices.example.com
```

I recommend using a docker-compose file to run the app. Here's an example:

```yaml
version: "3"
services:
  invoices:
    image: ghcr.io/scottmckendry/ccinvoice:main
    container_name: invoices
    networks:
    - traefik
    volumes:
    - /etc/localtime:/etc/localtime:ro
    - /var/run/docker.sock:/var/run/docker.sock
    - ./db.sqlite3:/app/db.sqlite3
    - ./.env:/app/.env
    ports:
        3000:3000
    restart: unless-stopped
```

This will run the app on port 3000. I recommend using [Traefik](https://traefik.io) as a reverse proxy. Take a look at my [setup guide](https://scottmckendry.tech/traefik-setup/) for more information.

> [!WARNING]\
> Do not expose the app to the internet without a reverse proxy running authentication middleware. The app does not have any authentication built in.

## 🧑‍💻 Development
To run the app locally, create a `.env` file matching the example above. Then use the docker-compose file in the root of the repository by running `docker compose up`. This will run the app on port 3000. You can then access the app at [http://localhost:3000](http://localhost:3000).

The project uses [air](https://github.com/cosmtrek/air) for live reloading. To run the app locally without docker, run `air` in the root of the repository.

## 🤝 Contributing
Pull requests are welcome. For major changes, please open an issue first to discuss what you would like to change.
