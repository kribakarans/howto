# Decrypting the WhatsApp Database

This guide explains how to extract and decrypt WhatsApp chat data from an Android device for analysis or backup purposes.

## Prerequisites

- USB Debugging is enabled on the Android device (Settings → Developer Options → USB Debugging)
- Root access is available on the Android device
- Logged into the WhatsApp account whose data you want to decrypt
- ADB installed on your PC (Install via apt install adb or from Android Platform Tools)

## Extracting WhatsApp Data

### 1. Pull WhatsApp Media Folder

WhatsApp media is stored under the scoped storage directory:

```
adb pull /sdcard/Android/media/com.whatsapp/WhatsApp ./workspace/WhatsApp-Media
```

### 2. Pull WhatsApp Key and Database Files (Root Access Required)

The key and database are stored in the internal protected storage. You must have root access:

```
adb root
adb pull /data/data/com.whatsapp/files/key                     ./workspace/key
adb pull /data/data/com.whatsapp/databases/wa.db               ./workspace/wa.db
adb pull /data/data/com.whatsapp/databases/msgstore.db.crypt12 ./workspace/msgstore.db.crypt12
```

Tip: If `adb root` doesn't work, try using `adb shell` and run the pull commands from a root shell.

# Methods to Decrypt Database

## 1. Decrypt with [WhatsApp-Chat-Exporter](https://github.com/klab-oss/WhatsApp-Chat-Exporter)

### Features

- Decrypt .crypt12, .crypt14, .crypt15, and the latest databases
- Outputs chat history in readable HTML or structured JSON.

### Usage:

```
pip install whatsapp-chat-exporter

mkdir working_wts
cd working_wts

wtsexporter -a
```

### Decrypt Crypt12 or Crypt14 Database:
```
wtsexporter -a -k key -b msgstore.db.crypt14
```

### Export Datbase to HTML
```
wtsexporter -a
```

### Results

![Output](https://raw.githubusercontent.com/klab-oss/WhatsApp-Chat-Exporter/refs/heads/main/imgs/pm.png)

This will export the chats in HTML format to the result directory.

## 2. Decrypt with [whatsapp-msgstore-viewer](https://github.com/klab-oss/whatsapp-msgstore-viewer)

### Features

- Standalone Python Chat Viewer
- View contact and group chats and call logs
- Easy access to media files (images, audios and videos)
- Decrypt and view the database if you have the decryption key (Should support crypt12, crypt14 and crypt15)
- Cross-platform (Should work on Linux, Windows and Mac)

### Usage

```
git clone https://github.com/absadiki/whatsapp-msgstore-viewer

pip install -r requirements.txt

python main.py
```

![Output](https://raw.githubusercontent.com/klab-oss/whatsapp-msgstore-viewer/refs/heads/main/assets/demo/demo_gif_2.gif)

## 3. Decrypt with [wa-crypt-tools](https://github.com/klab-oss/wa-crypt-tools)

- Decrypt and encrypt WhatsApp and WA Business' .crypt12, .crypt14 and .crypt15 files with ease
- For decryption, you NEED the key file or the 64-characters long key
- The key file is named "key" if the backup is crypt14 or "encrypted_backup.key" if the backup is crypt15 (encrypted E2E backups)
- Those who are looking for a more complete suite for WhatsApp forensics, check out [whapa](https://github.com/B16f00t/whapa).

### Usage
```
python -m pip install wa-crypt-tools

wadecrypt key msgstore.db.crypt14 msgstore.db
```

## 4. Decrypt with [whapa](https://github.com/klab-oss/whapa)

- Dcryption Working
- Export is not working (raw_string_jid column not found error)

### Usage

```
git clone https://github.com/B16f00t/whapa.git && cd whapa

pip3 install --upgrade -r ./doc/requirements.txt

python3 whapa-gui.py
```

![Output](https://raw.githubusercontent.com/B16f00t/whapa/master/doc/software.png)

# Methods to View Decrypted Database

### 1. [WhatsApp-Chat-Exporter](https://github.com/klab-oss/WhatsApp-Chat-Exporter)

- This tool can decrypt and export chats to HTML format

### 2. [whatsapp-msgstore-viewer](https://github.com/klab-oss/whatsapp-msgstore-viewer)

- Standalone application to decrypt and view chats in the PC

### 3. [WhatsApp-Viewer](https://github.com/klab-oss/WhatsApp-Viewer)

- Export the WhatsApp chats to HTML file from the decrypted database
- It doesn't have an option to decrypt the database
- Configure the file msgstore.db, key location as follows:
```
$ cat config.cfg
[input]
# Path to the file msgstore.db
msgstore_path=msgstore.db
# Use external contacts database wa.db?
use_wa_db = True
# Path to the file wa.db
wa_path=wa.db

[output]
# Create an HTML export?
export_html=True
# Path to the HTML file to export
html_output_path=index.html
# Create an export to txt files?
export_txt=False
# Path to the directory for exporting txt files
txt_output_directory_path=output
```

## Other Repos
https://github.com/EliteAndroidApps/WhatsApp-Crypt12-Decrypter

https://github.com/KisanThapa/WhatsApp-Database-Decrypter (Worked for crypt12 | Older Repo)

https://github.com/andreas-mausch/whatsapp-viewer (Windows App | Need to Test)
