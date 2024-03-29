# PYGDCLI
Python CLI client to selectively sync Google Drive directories from Ubuntu terminal.

# Installation
- Clone this git repository.
```bash
git clone https://github.com/akhlak-mahmood/pygdcli.git ~/pygdcli
```
- Install the dependencies.
```bash
pip install --upgrade pytz python-dateutil google-api-python-client google-auth-httplib2 google-auth-oauthlib peewee
```
- Navigate to your local Google Drive sync directory.
```bash
mkdir ~/GDrive
cd ~/GDrive
```  
- Run the client with a path for the settings file.
```bash
~/pygdcli/gdcli settings.json
```
This will create a **settings.json** file.

- Next, edit the **settings.json** file specifying your desired Google Drive sync directory. Please make sure the json format is correct. (There should not be any comma after the last item.)
For example,
```json
{
"local_root_path": "Photos",
"remote_root_path": "/Photos",
"token_pickle": "token.pk",
"db_file": "db-photos.sqlite"
}
```
- Run the client again.
```bash
~/pygdcli/gdcli settings.json
```
 A new browser window will open up to authenticate the app and grant permissions to access your Drive files. Review the permissions.

 *Please note that, the app has not been verified by Google yet, so you will have to choose to continue with the "unsafe" option during authentication.*

- You will be asked to review and confirm the detected changes before they are executed. Files outside your sync directory will still be reported by Google Drive API as changes, they will be ignored accordingly.

# Features
- You can sync multiple folders by using different **settings.json** with different `root_paths` and `db_file`.
- You can use multiple google accounts by specifying different `token_pickle` paths.
- You can specify a list of glob patterns as `ignore_paths` to ignore certain files during sync. Example:
```json
    "ignore_paths": [
        "*.pk",
        ".~*",
        "*.ipynb_*"
    ]
```

# Limitations
- The client does not watch file changes, so you have to run it each time you need to sync.
- Files are downloaded to memory first, so files with size greater than your available memory will fail to download.
- No differential sync supported, whole file will be uploaded/downloaded during sync.

# Dependencies
Python libraries:
- pytz
- python-dateutil
- google-api-python-client
- google-auth-httplib2
- google-auth-oauthlib
- peewee

# License
GNU General Public License v3.0 (c) 2019 Akhlak Mahmood
