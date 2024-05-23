# Jellyfin2Emby

[中文文档](./README.md)

**This English document is machine-translated, and there may be errors in wording. Please bear with us.**

> Migrate Jellyfin users and their watch history to Emby

This script is based on [Marc-Vieg/Emby2Jelly](https://github.com/Marc-Vieg/Emby2Jelly) and has been modified for Jellyfin2Emby.

Known issues:

1. Inaccurate migration of the "Continue Watching" progress; After migration, the item (episode) will appear as not watched. For example: if a show in Jellyfin is watched up to 10 minutes into S01E03, after migration it will appear as unwatched in Emby.
2. Cannot migrate "Favorites" records.
3. Passwords cannot be migrated.

------

### Tested Versions

- Jellyfin: 10.8.13
- Emby: 4.8.7.0

------

### Check

**Ensure your content has been identified (it is recommended to refresh missing metadata in your library)**

Ensure that both Emby and Jellyfin search for missing metadata, even every episode/season needs to have its `providerIds` to be migrated correctly.

------

### Requirements

python3

```
json
requests
urllib.parse
configobj
time
getpass
```

------

### Configuration

Edit the settings.ini file and add your Emby and Jellyfin URLs and API keys:

```
[Emby]
EMBY_APIKEY = aaaabbbbbbbcccccccccccccdddddddd
EMBY_URLBASE = http://127.0.0.1:8097/
EMBY_PASSWORD = passwordAZ
[Jelly]
JELLY_APIKEY = eeeeeeeeeeeeeeeffffffffffffffffggggggggg
JELLY_URLBASE = http://127.0.0.1:8096/

# A trailing slash is required.

## If you have custom paths or reverse proxies, don't forget /emby/ or /jelly/
```

------

### Usage

Migrate from Jellyfin to Emby:

```
python3 jellyfin2emby.py
Parameters: (Only one file can be used at a time; run one file per execution)
        --tofile [file]     Run the script and save the view status to a file instead of sending it to the target server
        --fromfile [file]   Run the script and take the source server data from a file then send the view status to the target server
        --new-user-pw "change-your-password-9efde123"
```

(Password priority: `--new-user-pw` parameter first, then EMBY_PASSWORD in settings.ini, and finally manual input during execution)

------

### Results

The script will generate a RESULTS.txt containing a summary and a list of media not found for each user:

```
                      ### Jelly2Emby ###


fish (Jellyfin) is  fish (Emby)
user0 Created on Emby


--- fish ---
Medias Migrated : 71 / 71
--- user0 ---
Medias Migrated : 1 / 1
```

------

### Thanks

Special thanks to the original author of Emby2Jelly, Marc-Vieg (CobayeGunther).