# Discourse deployment

I used [this](https://github.com/discourse/discourse/blob/main/docs/INSTALL-cloud.md) document as a refrence for deployment.

⚠️ WARNING: I DEPLOYED THIS WITHOUT EMAIL AND TLS/HTTPS FUNCTIONALITY ONLY TO TEST IT IN MY LOCAL, ITS NOT SECURE FOR DEPLOYMENT ON PRODUCTION ENVIRONMENTS

Prerequisites:

- a Linux server
- Docker Installed
- 4GB RAM
- 2 CORE CPU

## Steps

1. become root (or just use sudo)
2. clone the docker discourse repo and cd:

   ```txt
   git clone https://github.com/discourse/discourse_docker.git && cd discourse_docker
   ```

3. run discourse-setup script with the command `./discourse-setup --skip-connection-test` (used for local deployments), then you should be prompted for these inputs:

   ```txt
    Hostname for your Discourse? [discourse.eryx.    localhost]: YOUR_DISCOURSE_DOMAIN

    Email address for admin account(s)? [dummy@mail.com]: DUMMY_EMAIL

    SMTP server address? [DUMMY]: DUMMY

    SMTP port? [587]: 587

    SMTP user name? [7569f6001@smtp-brevo.com]: DUMMY

    SMTP password? [5gkLmaM8H7n4Qq6K]: DUMMY

    notification email address? [noreply@mailtest.unnamed0. shop]: DUMMY

    Optional email address for Let's Encrypt warnings?  (ENTER to skip) [me@example.com]: *press enter*

    Optional MaxMind Account ID (ENTER to continue without  MAXMIND GeoLite2 geolocation database) [123456]: *press enter*
   ```

   note: you probably only need to set your discourse domain (first question) if you don't want the email functionality.

4. after the app.yml got generated (we can see in the terminal logs), we should ctrl-c from the discourse-setup and go edit the `./containers/app.yml` with our editor of choice and comment these two specified lines:

   ```yaml
    templates:
      #- "templates/web.ssl.template.yml"
      #- "templates/web.letsencrypt.ssl.template.yml"
   ```

   as you can see in the commented two lines, we don't want https/tls, because we are running in local and the domain isn't resolvable over the internet.

5. we should rebuild the app (and wait for tooooo long):

   ```sh
   ./launcher rebuild app
   ```

   note: everytime you change settings, you should rebuild the app.

6. after the app is built, we can see the container named `app` is up, now we should create our `admin` user from the command line, this is used to bypass the email functionality.

   ```sh
   ./launcher enter app
   ```

7. and then we type `rake admin:create` to create the admin account, you will be presented with a form like below:

   ```txt
    Email:  dummy@mail.com    
    Password:  somepass
    Repeat password: somepass
   ```

    note: you can use the email line as username too, because you will be prompted to login with "email" which
8. remember your domain name that you specified in step 3?, type the domain in your browser, and login with your `email/username` and password that you specified
9. profit 💲💲💲.
