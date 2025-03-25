
### Step 4: Configure WordPress
1. Open your browser and go to `http://localhost:90/wordpress` (or the folder name you used).
2. Select your preferred language.
3. WordPress will prompt you to enter database details:
   - **Database Name**: The name of the database you created (e.g., `wordpress`).
   - **Username**: `root` (default MySQL username in XAMPP).
   - **Password**: Leave this blank (default XAMPP MySQL password is empty).
   - **Database Host**: `localhost`.
   - **Table Prefix**: Default is `wp_`.
4. Click **Submit**, then **Run the Installation**.

### Step 5: Complete WordPress Setup
1. Enter your website details:
   - **Site Title**: Your site's name.
   - **Username**: Your admin username.
   - **Password**: A strong password for admin login.
   - **Email**: Your email address.
2. Click **Install WordPress**.
3. After installation, you can log in to your WordPress dashboard at `http://localhost:90/wordpress/wp-admin` with the credentials you created.
After completeing aove listed step-4 and step-5, i was doing below:
So when i was trying to restore actual required website backup DB first into my dummy testDB(created a DB inside phpadmin at localhost:90 so that i can login into localhost:90/wordpress).
I have installed a database plugin named WP-DBManager which contains options like Backup Db, Manage Backup, Empty, Repair, Optimize DB.
Even after having the exact Microsoft SQL Server Query File (.sql) of database to be restored, it was a futile attempt.
So next i've installed All-in-one-WP-Migration plugin and tried its Import option(which basically needs the entire .wpress file that includes entire DB+plugins+other files present).
Initially the max limit was set to 45 MB and my .wpress file that needed to be imported was of 1.2GB. 
To change it first i've updated confguration C:\Program Files\XAMPP\php:
#### upload_max_filesize 2G
#### post_max_size 2G
#### memory_limit 2G

```bash
Import From

Your host restricts uploads to 2 GB. Our Unlimited Extension bypasses this!

If you prefer a manual fix, follow our step-by-step guide on raising your upload limit.


Import failed
Your file exceeds the upload limit set by your host web server.
Our Unlimited Extension bypasses this!
If you prefer a manual fix, follow our step-by-step guide on raising your upload limit.


# BEGIN PHP Configuration
php_value upload_max_filesize 2G
php_value post_max_size 2G
php_value memory_limit 2G
# END PHP Configuration

this in .htaccess file

the file uploading .wpress format is only of 2gb, even after changing the php.ini conf files to take max file size upload to 2gb and memory im still getting the error
```

To resolve the error, I basically downloaded a downgraded 6.7 version of All-in-one-WP-Migration plugin from [Website](https://mega.nz/file/A8JFkTQK#5i5RRxJxMg4Iu2Y6KxpY30BjShPmCSZhlaTGC6qj5mk), uploaded the plugin which itself got extracted from .zip format and I activated it and selected 'Replace current with uploaded'.
Now inside Tools option I've selected Plugin File editor and selected all-in-one-wp-migration.php inside dropdown, under it selected constants.php and changed line number 284 to *define('AI1WM_MAX_FILE_SIZE', 2 << 40);* from 2 << 28.
This gave me Maximum upload file size: 2TB inide the All-in-One WP Migration Imports tab
