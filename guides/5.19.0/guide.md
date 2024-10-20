# Version 5.19.0

| Version | Download                         | Guide Compatibility              | End of Compatibility | Notes                                       |
| ------- | -------------------------------- | -------------------------------- | -------------------- | ------------------------------------------- |
| 5.19.0  | [Download](https://downloads.getfiddler.com/win/Fiddler%20Everywhere%205.19.0.exe) | 5.17.0 +                         | -                    | Compatible with "no libfiddler.dll versions |


## Pre-requirements
  - Fiddler everywhere 5.19.0 (or another compatible version)
  - Local Server (which response to `identity.getfiddler.com` & `api.getfiddler.com`): [Download](./server/)
  - `fiddler.dll` & `hostpolicy.dll` from [Yui-Patch](https://github.com/project-Yui/Yui-patch). Download it from the [releases](https://github.com/project-Yui/Yui-patch/releases/).
    > Note that only `Yui-Patch` release `1.1.0 + ` are supported by Fiddler Everywhere 5.19.0. You can download it from release [1.1.0](https://github.com/project-Yui/Yui-patch/releases/tag/1.1.3)

    > Update: Important, that the current (as of 18/10/2024) the `latest release` - `1.1.3` is *supported by Fiddler Everyehere `5.19.0`+*

## Guide
  
  > Note that there're no real order to patch. Just need to follow all steps in ordered manner or not.

  0. Install Fiddler Everywhere (Or just extract the exe with WinRar).
  1. Open Installation Folder
  2. Delete `fiddler.dll` in the root directory
  3. Copy the downloaded `fiddler.dll`. (Downloaded from Yui-Patch in pre-reuirements)
     > Of course you can do 2. and 3. in one step buy just replacing original `fiddler.dll` with Yui-Patch's `fiddler.dll`
  
  4. Open `resources/app/out/WebServer`
     ![Screenshot](https://github.com/user-attachments/assets/f85a8806-b47a-4180-9f96-3a8b7422f14d)

  5. Locate `hostpolicy.dll` and Rename it to `hostpolicy.original.dll`
  6. Copy the downloaded `hostpolicy.dll` to the `root/resources/app/out/WebServer` folder which contains newly renamed `hostpolicy.original.dll`
     > So the WebServer has both `hostpolicy.dll` and `hostpolicy.original.dll`
     
     ![Screenshot](https://github.com/user-attachments/assets/399401b3-2977-483c-85b9-29a544ce026c)

  7. Now, you're in `root/resources/app/out/WebServer/`. Open `ClientApp/dist/` folder. Now you're in `root/resources/app/out/WebServer/ClientApp/dist`. Search a file named like `main-PCHGHPS6.js`.
     > For `5.19.0` the file name is `main-PCHGHPS6.js` but for other versions the text following `main-` is different.

  8. Copy the `main-PCHGHPS6.js` likely named js to the same directory but rename it to `main-PCHGHPS6.original.js`. So you need to append `.original` to end of the file name. So you have to files like this.
     ![Screenshot](https://github.com/user-attachments/assets/cbd5ce84-ae02-4cca-aa7e-48d54325f690)

  9. Open `main-PCHGHPS6.js` like js (Not the one that have `.original` suffix. 
      - And `Search` and `Replace All`, `https://api.getfiddler.com` with `http://127.0.0.1:5678/api.getfiddler.com`
      - And `Search` and `Replace All`, `https://identity.getfiddler.com` with `http://127.0.0.1:5678/identity.getfiddler.com`
      
  10. Go back *3 steps* (3 folders back) and now you're in `root/resources/out/`. And find for `main.js`. Unlike the previous one. This's not follwed by letters. And copy it to same directory and rename to `main.original.js` like you did for previous js, So you've two main files like this.
      ![Screenshot](https://github.com/user-attachments/assets/2835398f-73c8-41fa-b0a0-f790008036b8)

  11. Open a new File Explorer, and open downloaded `server` folder from pre-requirements. And you have a folder named `file` and a file named `index.js` in it. Copy the `file` folder and copy it to `root/resources/app/out/` folder. Now your `out` folder of Fiddler Everywhere looks like this.
      ![Screenshot](https://github.com/user-attachments/assets/844081f2-92bc-47c0-bb14-acb24aba2793)

  11. Back in the `server` folder (which we'd downloaded in pre-requirements), there's a file named `index.js`. 
      - Open it (`index.js`) in a text editor. 
      - Copy entire js code in it.
      - Now back to Fiddler Everywhere, open `resources/app/out/main.js` in a text editor. (Not the one with we copied and renamed `.original` suffix)
      - Append the copied code (from `index.js`) to the very begining of `main.js` (which we've opened in text editor of course).
        > No need to (Actually don't) leave any spaces.
  
  12. Now, back into `root/resources/app/out/WebServer/` folder and create a `json` file named. `patch.json`
        - Open it with a text editor and put following content.
        ``` json
        {
            "ClientApp\\dist\\main-TPC5GS2R.js": {
                "target": "ClientApp\\dist\\main-TPC5GS2R.original.js",
                "content": "",
                "cur": 0,
                "start": 0,
                "end": 1
            },
            "..\\main.js": {
                "target": "..\\main.original.js",
                "content": "",
                "cur": 0,
                "start": 0,
                "end": 1
            }
        }
        ```
        > Note that the file names `main-TPC5GS2R.js` & `main-TPC5GS2R.original.js` is for version 5.19.0 as we discussed above. You need to replace it with tha names of the js files we've edited, and copied-renamed in `root/resources/app/out/WebServer/ClientApp/dist/`
   
   
**All Done! Now, you should be able to open and use it, well with an unlimited trial period that doesn't limit any functionality.**

