# publik.ae
Website source for publik.ae


1. Download the current project to your local machine

Since SFTP is connected:

Use an SFTP client (like FileZilla, WinSCP, or Cyberduck).

Connect to your server using the SFTP credentials.

Navigate to your Laravel project folder (usually something like /home/adminer/htdocs/publik.ae or /var/www/publik.ae).

Download the entire folder to your local machine.

⚠️ Make sure you don’t overwrite .env on your local yet if you want local testing, because production .env contains live credentials.

2. Set up your local environment

Install PHP, Composer, MySQL, and Node.js/npm on your local machine if not already installed.

Navigate to your downloaded project folder and run:

composer install
npm install
npm run dev  # if your project uses frontend assets


Copy .env from the server (or create a .env.local) and adjust for your local environment (DB credentials, cache, etc.).

Generate a local app key:

php artisan key:generate


If your project uses migrations:

php artisan migrate

3. Make your code changes locally

Edit controllers, views, routes, etc., in your favorite IDE.

Test everything locally to ensure your changes work. You don’t want to break the live site.

You can use a local server with:

php artisan serve


Open http://127.0.0.1:8000 in your browser to verify changes.

4. Prepare for deployment

Before uploading changes:

Pull only changed files — don’t overwrite the vendor folder or storage folder unless necessary.

Optional: use Git for version control (highly recommended) for tracking changes.

5. Upload changes via SFTP

Connect to your server via SFTP.

Upload only the files you modified. Typical files you’ll update:

app/ (controllers, models)

resources/views/ (Blade templates)

routes/web.php or routes/api.php

public/ (if any JS/CSS changed)

Do not overwrite .env unless you intend to change live config.

6. Run server-side commands

After uploading, SSH into your server (CloudPanel usually gives SSH access):

Clear cache to make Laravel see the changes:

php artisan config:clear
php artisan route:clear
php artisan view:clear
php artisan cache:clear


If you changed migrations or database, run:

php artisan migrate --force


--force is required on production to run migrations without prompt.

7. Verify changes

Visit your live site and test all modified functionality.

Use different browsers or incognito mode to avoid cached assets.

If you changed CSS/JS, run:

php artisan view:clear
php artisan config:clear


and clear browser cache.

8. Optional: Use a better workflow

Use Git for deployment. Push your changes to a Git repo, and then pull them on the server. This avoids overwriting things by mistake.

Use php artisan env:production or set APP_ENV=production in .env to ensure proper production environment.

💡 Quick Summary of SFTP Workflow:

Download project → work locally → test locally

Modify code → verify locally

Upload changed files → clear Laravel caches

Verify live site
