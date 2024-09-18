# Version 5.15.1

| Version | Download                         | Guide                      | Guide Compatibility              | End of Compatibility | Notes                        |
| ------- | -------------------------------- |--------------------------- | -------------------------------- | -------------------- | ---------------------------- |
| 5.15.1  | [Download](https://rb.gy/abawou) | [Guide](/guides/5.15.1.md) | 5.9.0 to somewhere around 5.16.X | Doesn't know clearly | Isn't compatible with 5.17.0 |


## Pre-requirements
  - Fiddler everywhere 5.15.1 (or another compatible version)
  - Local Server (which response to `identity.getfiddler.com` & `api.getfiddler.com`): [Download](./server/)
  - `libfiddler.dll` & `hostpolicy.dll` from [Yukihana-Patch](https://github.com/project-yukihana/Yukihana-patch). Download it from the [releases](https://github.com/project-yukihana/Yukihana-patch/releases/tag/v1.0.9).
    > Note that new versions of [Yukihana-Patch](https://github.com/project-yukihana/Yukihana-patch) *might not support* Fiddler Everywhere 5.15.1. The last checked version is [1.0.9](https://github.com/project-yukihana/Yukihana-patch/tree/v1.0.9). You can download it from [original repository releases](https://github.com/project-yukihana/Yukihana-patch/releases/tag/v1.0.9) or from [backup](https://rb.gy/8f75nl)

## Guide
  > Note: You can also just downloaded patched repack: [Just Download Repack](https://www.dropbox.com/scl/fi/d9nuu9pk4a24lmz0q1htq/Fiddler-Everywhere-5.15.1-Cracked.zip?rlkey=kcj8ky0dmh98suuwm6sbll2q9&st=1tsthdl3&dl=1)
  
  > Note that there're no real order to patch. Just need to follow all steps in ordered manner or not.

  0. Install Fiddler Everywhere (Or just extract the exe with WinRar).
  1. Open Installation Folder (Looks like following)
     ![Screenshot](https://github.com/user-attachments/assets/5d09eaf8-b412-483e-a715-c0bbdf3106f2)
  
  2. Delete `libfiddler.dll` in the root directory
     ![Screenshot](https://github.com/user-attachments/assets/2f599f7c-5ca2-4eab-ae33-e396de856a82)
  
  3. Copy the downloaded `libfiddler.dll`. (Downloaded from Yukihana-Patch in pre-reuirements)
     > Of course you can do 2. and 3. in one step buy just replacing original `libfiddler.dll` with Yukihana-Patch's `libfiddler.dll`
  
  4. Open `resources/app/out/WebServer`
     ![Screenshot](https://github.com/user-attachments/assets/f85a8806-b47a-4180-9f96-3a8b7422f14d)

  5. Locate `hostpolicy.dll` and Rename it to `hostpolicy.original.dll`
  6. Copy the downloaded `hostpolicy.dll` to the `root/resources/app/out/WebServer` folder which contains newly renamed `hostpolicy.original.dll`
     > So the WebServer has both `hostpolicy.dll` and `hostpolicy.original.dll`
     
     ![Screenshot](https://github.com/user-attachments/assets/399401b3-2977-483c-85b9-29a544ce026c)

  7. Now, you're in `root/resources/app/out/WebServer/`. Open `ClientApp/dist/` folder. Now you're in `root/resources/app/out/WebServer/ClientApp/dist`. Search a file named like `main-OX7W2LTJ.js`.
     > For `5.15.1` the file name is `main-OX7W2LTJ.js` but for other versions the text following `main-` is different.

  8. Copy the `main-OX7W2LTJ.js` likely named js to the same directory but rename it to `main-OX7W2LTJ.original.js`. So you need to append `.original` to end of the file name. So you have to files like this.
     ![Screenshot](https://github.com/user-attachments/assets/cbd5ce84-ae02-4cca-aa7e-48d54325f690)

  9. Open `main-OX7W2LTJ.js` like js (Not the one that have `.original` suffix. 
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
            "ClientApp\\dist\\main-OX7W2LTJ.js": {
                "target": "ClientApp\\dist\\main-OX7W2LTJ.original.js",
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
        > Note that the file names `main-OX7W2LTJ.js` & `main-OX7W2LTJ.original.js` is for version 5.15.1 as we discussed above. You need to replace it with tha names of the js files we've edited, and copied-renamed in `root/resources/app/out/WebServer/ClientApp/dist/`
   
   
**All Done! Now, you should be able to open and use it, well with an unlimited trial period that doesn't limit any functionality.**
