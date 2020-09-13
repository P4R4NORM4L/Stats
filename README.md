
# Rust PHP Stats page

Shows stats of players like KDR and played time.<br>
SQL Stats is used to show the amount of animals that have been killed altogether.<br>

01.09.2020: This is rewritten to support oxide plugin: PlayerRanks and SQL Stats

git clone https://github.com/P4R4NORM4L/Stats.git

## Short Example:
Edit /api/api-server#.php and enter your API details
- Battlemetrics support
- Support for multiple servers
- Support for rust-servers.net and rust-servers.info
- Support for PlayerRanks
- Support for SQL Stats

See the how to section for setup.

# Required:
- Oxide
- Oxide plugin: PlayerRanks and/or SQL Stats
- battlemetrics.com - no need to register your server
- rust-servers.net - you need to register your server to get an api key
- rust-servers.info - you need to register your server to get an api key
- MySql/MariaDB
- Webserver
- php 5.6 or higher

# Oxide plugin:
[PlayerRanks](https://codefling.com/files/file/14-playerranks/)<br>
See how to install on https://codefling.com/files/file/14-playerranks/?tab=details

[SQL Stats](https://www.chaoscode.io/resources/sqlstats.114/)<br>
See how to install on https://www.chaoscode.io/resources/sqlstats.114/

# How to:
I'm gonna assume you already know how to install PlayerRanks and/or SQL Stats plugins.

## Download the content
1. Create a folder on your computer and download the files as a zip and extract the content to the folder of your choice.

## Web files
1. Copy the all the extracted files/folders from your download folder exept for folders: nginx, rustadmin unless you need them<br>
2. Edit the mconfig.php file to match your playerranks database settings in your oxide/config directory of your rust server<br>
3. If you have the SQL Stats plugin as well, make sure to uncomment that section clearly identified in mconfig.php<br> 
4. Configure your api-server1.php to match your server settings<br>
5. Changing the background image: Change link on line 23 in mycustom.css file<br>

## Web Directory
1. I recommmend using WinSCP to connect via SSH to your webserver.
2. Once connected, create a new folder named Stats
3. Copy all files from the extracted folder on your desktop to your newly created folder, in this case, Stats on your webserver.
4. Make sure your newly created folder has the right permissions / owner:group

### You can use chown -R owner:group /path/of/your/website/Stats

## Rust plugin PlayerRanks.cs
1. Get latest update from https://codefling.com/files/file/14-playerranks/ and add it into your rust plugin folder.<br>
2. you should now edit the file oxide\config\PlayerRanks.json and fill inn the database information like below<br>
```
"MySQL": {
    "useMySQL": true,
    "autoWipe": false,
    "sql_port": 3306,
    "sql_host": "localhost",
    "sql_db": "Database",
    "sql_user": "DBUser",
    "sql_pass": "UserPassword",
    "tablename": "playerranksdb",
    "LBtableName": "playerranksLeaderdb"
  }
```
3. Go into rust console and type o.reload PlayerRanks - this plugin will auto create the sql tables.
4. Wait 15 min and it should save the data to the SQL database server, or run this console command in Rcon: playerranks.save

## Subdomain
I have no idea what hosting company you use, but you should now just create a "A Record" stats.yourdomain.com and point it to your external IP<br>
just remember to open port 80/443 TCP from same as you open the rust port.<br>

You should also consider to move your domain to Cloudflare for faster cdn and website<br>
You also get free ssl and auto renewal.


# Credits
Kennethrisa for his awesome work!
Steenamaroo for his great plugin!
