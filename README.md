# msn-chat-history-viewer

View your MSN Messenger chat history XML files in a web browser with early 2000's style formatting.

[Try it out now](https://tysonmatanich.github.io/msn-chat-history-viewer/index.html)

## Features

- Once built, simply open the index.html file and drag on a Messenger XML file over to view it formatted how it looked back in the early 2000's in MSN Messenger 6.2
- File can run directly off the file system and doesn't require a web server
- All data stays private in browser with no uploading to a server
- Supports viewing on mobile devices

### Options

- Toggle on/off
  - Emoticons
  - Animations (GIFs or PNG)
  - Logon Name \<email@address.com\>
  - Message Date
  - Message Time
- Display customized names for each party making it easier to tell who the message is from
- Render as a more modern threaded text messaging bubble interface

## Commands

```bash
# Use Webpack to serve locally with hot reloading
npm run serve

# Use Webpack to bundle CSS and JavaScript into separate files and inline the XSLT in JS for use with a web server
filesys
npm run build

# Use Webpack to inline CSS, JavaScript, XSLT so it can run off the file system without a web server
npm run build-filesys
```

## Known Issues

- Some chat history XML files are missing `@LogonName` which custom names relies on to determine who sent the message
- Only supports `.xml` files no support for other files such as `.txt`, `.rtf`
- Only tested on Chrome for Windows and Chrome for iOS, bugs may exist with other browsers.

## MSN Messenger Assets

The image assets were extracted from the MSN Messenger 6.2 exe ([download at your own risk](http://www.oldversion.com/windows/msn-messenger-6-2)) using [7-Zip](https://www.7-zip.org/).

```
msnm62.exe > MsnMsgs.msi > MsgrCore.cab > msnmsgrexe.ADEB440D_7847_4F65_80BD_899870ED2EC9 > .rsrc > PNG
```

The PNGs in this folder are missing file extensions. These can be added via a PowerShell script:

```ps
# Define the path to the folder
$folderPath = "C:\Users\user\Downloads\msnm62\MsnMsgs\MsgrCore\msnmsgrexe\.rsrc\PNG"

# Get all files in the folder without an extension and .png
Get-ChildItem -Path $folderPath -File | Where-Object { -not $_.Extension } | ForEach-Object {
    $newName = "$($_.FullName).png"
    Rename-Item -Path $_.FullName -NewName $newName
}
```

I had to convert the PNG sprites to animated GIFs. I matched the timing of the GIFs to the ones I found on an [archive of old MSN Messenger site](http://web.archive.org/web/20140204231459/http://messenger.msn.com/Resource/Emoticons.aspx).
