#🔥 Zilan

Zilan is Instagram scrapper which you can get accounts informations and download accounts' photos/videos.

## Documentation

- [Installation](#installation)
    - [Requirements](#requirements)
    - [Installation](#installation-1)
- [Usage](#usage)
    - [Basic Usage](#basic-usage)
    - [Required Parameters](#required-parameters)
    - [Get Account Information](#get-account-information)
    - [Get Account Posts](#get-account-posts)
    - [Download Account Media](#download-account-media)
    - [Download From List](#download-from-list)
    - [Create Settings File](#create-settings-file)
- [Usage With Docker](#usage-with-docker)
    - [Build or Install Docker Image and Run](#build-or-install-docker-image-and-run)
    - [Create Shared Folder](#create-shared-folder)
    - [Pass Arguments to Docker Container](#pass-arguments-to-docker-container)

<hr />

## INSTALLATION

### Requirements

1. [Python 3.4+](https://www.python.org/downloads/)
2. [Pip](https://pip.pypa.io/en/stable/)

### Installation

1. Clone this repo,
2. Install required libraries with pip,
3. Start `app_console.py` with python. 

```bash
$ git clone https://github.com/arviinmo/Zilan.git
$ cd zilan/
$ python -m pip install -r requirements.txt
$ python app_console.py
```

<hr />

## USAGE

### Basic Usage

```
usage: app_console.py [-h] [-u] [-p] [-a] [-s] [--info] [--posts]
                             [--media] [-l] [-o] [--save] [--download]
                             [--video]

Zilan : The Fastest Instagram Scraper

optional arguments:
  -h, --help        show this help message and exit
  -u , --username   User username
  -p , --password   User password
  -a , --account    Account username for scraping
  -s , --settings   The user settings file path
  --info            Get account general information
  --posts           Get user posts' information
  --media           Get user media information
  -l , --list       Download from account list file
  -o , --output     The file/directory path for saving result
  --save            Save the media or information
  --download        Download the media
  --video           Include videos for download. Default : False
```

### Required Parameters

To use Zilan, following parameters must be used for all commands.

| Args                  | Required  | Description                                           |
| ---                   | ---       | ---                                                   |
| `-u`, `--username`    | Required  | The username of the user who want to get information  |
| `-p`, `--password`    | Required  | The password of the user who want to get information  |
| `-a`, `--account`     | Required  | The instagram username who want to be scraped         |

This parameters must be given either as argument at runtime or as variable in [user settings file](#create-settings-file). 

### Get Account Information

Zilan can get account information such as followers, followed by etc.

| Args              | Required  | Description                                           |
| ---               | ---       | ---                                                   |
| `--info`          | Required  | Show account information                              |
| `--save`          | Optional  | Save information to file                              |
| `-o`, `--output`  | Optional  | Define file path. Used only with `--save` parameter   |

**Note:** Output should be `txt` file for better file view.

**Example Usage:**

```bash
$ python app_console.py -s settings.yml -a insta.account --info
# Show information

$ python app_console.py -s settings.yml -a insta.account --info --save
# Show information and save that to ./output.txt file

$ python app_console.py -s settings.yml -a insta.account --info --save -o ./result.txt
# Show information and save that to ./result.txt file
```

### Get Account Posts

Zilan can get account all posts information with taken time, media urls etc.

| Args              | Required  | Description                                           |
| ---               | ---       | ---                                                   |
| `--posts`         | Required  | Show account posts' information                       |
| `--save`          | Optional  | Save information to file                              |
| `-o`, `--output`  | Optional  | Define file path. Used only with `--save` parameter   |

**Note:** Output should be `json` file for better file view.

**Example Usage:**

```bash
$ python app_console.py -s settings.yml -a insta.account --posts
# Show posts' information

$ python app_console.py -s settings.yml -a insta.account --posts --save
# Show information and save that to ./output.json file

$ python app_console.py -s settings.yml -a insta.account --posts --save -o ./result.json
# Show information and save that to ./result.json file
```

### Download Account Media

Zilan can download all posts or a certain number of posts media with/without video files.

| Args              | Required  | Description                                           |
| ---               | ---       | ---                                                   |
| `--media`         | Required  | Show only account posts' information                  |
| `--save`          | Optional  | Save all media links to file                          |
| `--download`      | Optional  | Download media and save to path                       |
| `-o`, `--output`  | Optional  | Define the download directory path                    |
| `--video`         | Optional  | Include videos. Default is not included               |

**Note:** Output should be ***directory path***, if you use `--download` and should be ***json file path*** if you use `--save`.

**Example Usage:**

```bash
$ python app_console.py -s settings.yml -a insta.account --media
# Show account media information

$ python app_console.py -s settings.yml -a insta.account --media --save
# Show information and save that to ./output.json file

$ python app_console.py -s settings.yml -a insta.account --media --save -o ./result.json
# Show information and save that to ./result.json file

$ python app_console.py -s settings.yml -a insta.account --media --download
# Download account images to ./insta.account directory path

$ python app_console.py -s settings.yml -a insta.account --media --download -o ./downloads
# Download account images to ./downloads/insta.account directory path

$ python app_console.py -s settings.yml -a insta.account --media --download --video
# Download account image and videos to ./insta.account directory path
```

### Download From List

This part is still under development...🙃

### Create Settings File

If you prefer Zilan to get your information from file instead of parameters, you can create a settings file as yaml format.  
Example yaml file must be like that :

```
username : user_username
password : user_s3cr3t_p4ss
account  : the_account_name_wish_to_get_info
```

Remember that, none of the keys above is **not required**. You can define any of them and can give the others as parameter. Beside that, if you give a parameter which is already defined in settings file, **Zilan will take the parameter instead of defination in the settings file**. 

After creating settings file, you can use it like that;

```
$ python app_console.py -s ./user_settings.yml
$ python app_console.py -s ./user_settings.yml -u new_username
$ python app_console.py -s ./user_settings.yml -p new password
$ python app_console.py -s ./user_settings.yml -u new_username -p new password
$ python app_console.py -s ./user_settings.yml -a new_account
etc...
```