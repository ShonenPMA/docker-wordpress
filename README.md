# DOCKER WORDPRESS PHPMYADMIN MAILHOG NGINX SSL

Use WordPress locally with Docker using [Docker compose](https://docs.docker.com/compose/)


## Instructions

<details>
 <summary>Requirements</summary>

+ [Docker](https://www.docker.com/get-started)
+ [mkcert](https://github.com/FiloSottile/mkcert) for creating the SSL cert.

Install mkcert:

```
brew install mkcert
brew install nss # if you use Firefox
```

</details>

<details>
 <summary>Setup</summary>

 ### Setup Environment variables

Both step 1. and 2. below are required:

#### 1. For Docker and Wordress (Required step)

Copy `.env.example` in the project root to `.env` and edit your preferences.

Example:

```dotenv
DOMAIN=myapp.local
MYSQL_ROOT_PASSWORD=root
MYSQL_DATABASE=wordpress
MYSQL_USER=wordpress
MYSQL_PASSWORD=wordpress

PHPMYADMIN_PORT=8080
WORDPRESS_PORT=8000
```

#### 2. Create a SSL cert:

Run mkcert ${DOMAIN} in docker/nginx/certs

Example:

```shell
mkcert myapp.local
```

#### 3. Make sure your `/etc/hosts` file has a record for used domains.

```
sudo nano /etc/hosts
```

Add your selected domain like this:

```
127.0.0.1 myapp.local
```

</details>

<details>
<summary>Run</summary>

# Run docker-compose

```shell
docker-compose up -d
```
## Wordpress

🚀 Open [https://myapp.local](https://myapp.local) in your browser

## PhpMyAdmin

PhpMyAdmin comes installed as a service in docker-compose.

🚀 Open [http://127.0.0.1:8080/](http://127.0.0.1:8080/) in your browser

## MailHog

MailHog comes installed as a service in docker-compose.

🚀 Open [http://127.0.0.1:8025/](http://127.0.0.1:8025/) in your browser
</details>

<details>
<summary>Extra for WLS</summary>

# Install mkcert ( [source](https://www.haveiplayedbowie.today/blog/posts/secure-localhost-with-mkcert/))

1. Install mkcert on Windows - I used Chocolatey for this
2. Run `mkcert -install`
3. Install mkcert on Ubuntu WSL - for fun I decided to clone the repository and build it from source using Go
4. Run `mkcert -install` on Ubuntu
5. Back in a Windows PowerShell terminal I run `mkcert -CAROOT` to find out where the certificates were created on Windows. I copied these.
6. On Ubuntu run `mkcert -CAROOT` and then explorer.exe to open File Explorer on Windows at the Ubuntu directory.
7. Paste the certificates from step 5
8. Run `mkcert -CAROOT` again on Ubuntu (I'm not sure if this step is neccessary but it works!)
9. Create certificates on WSL e.g. mkcert example.com "*.example.com" localhost
10. Configure nginx or Apache to use the generated certificates


</details>