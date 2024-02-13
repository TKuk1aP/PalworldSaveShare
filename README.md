# Palworld Save Share

### A complete step-by-step guide on how to transfer a co-op save to another user while retaining all progress.
The process will require some collaboration between both parties.

<br />

The entire process takes about 15 minutes.

> [!NOTE]
> So far I've only tested it with 2 players
>
> Game version tested with ```v0.1.3.0```

<br />

## Prerequisites

<br />

- Download and install [Notepad++](https://notepad-plus-plus.org/) (Highly recommended)
> [!NOTE]
> This can be any other editor that can handle large documents and provides the ability to ***Search & Replace*** all occurrences in a file

<br />
<br />

- Download and install the latest version of [Python](https://www.python.org/)
> [!IMPORTANT]
> During installation, make sure to select the **```Add python X.X to PATH```** checkbox

<br />
<br />

- Download and extract [palworld-save-tools](https://github.com/cheahjs/palworld-save-tools) by [cheahjs](https://github.com/cheahjs)
> [!CAUTION]
>  Any version older than ```v0.4``` will create corrupt ```Level.sav``` files when converting from ***JSON*** to ***SAV***

<br />

## Step 1 - Locating the save
The save directory can be located at the following path
```C:\Users\%username%\AppData\Local\Pal\Saved\SaveGames\<YourSteamID>```

This directory will contain all of your Palworld saves including the ones from the worlds you've visited.

If you see more than one save, the simplest way to identify the correct one is by loading it in the game, saving it and then sorting the directories by *```'Date modified'```*, the latest should be the one.

> [!IMPORTANT]
> Manually backup your entire save to avoid losing it to data corruption

<br />

## Step 2 - Creating an organized workspace
> [!TIP]
> To simplify the process as much as possible, avoid collisions and having to repeat the process from the start, I highly recommend sticking to my naming conventions

<br />

1. Create a new folder anywhere where it is convenient for you and name it ```Work```
2. Inside the ```Work``` folder create a new folder and name it ```JSON_backup```
3. Inside the ```Work``` folder create a new text document and name it ```Guid```

<br />

## Step 3 - Cooperation
### In this step both parties have to cooperate in order to retrieve some values which will be crucial in the following steps
> [!NOTE]
> ***Host*** - refers to the current host
>
> ***Client*** - refers to the current client
>
> The same naming convention will be maintained throughout the entire procedure

<br />

### Client's instructions
1. Create a new world with multiplayer enabled and wait for the **Host** to join
2. After the ***Host*** joins, save and exit the game
3. Follow [Step 1](#Step-1---Locating-the-save) to locate the new world's save
4. Open the new world's ```Players``` folder,
   there should now be two ```.sav``` files one of which is named ```000...001.sav```, that's ***your*** file
5. Share with the ***Host*** the name of ***their*** player file

<br />

### Host's instructions
1. Join the ***Client*** in their newly created world
2. Wait for the ***Client*** to provide you with the name of ***your*** player file
3. Paste the file name in the ```Guid``` text document
4. On the next line write down the first 8 characters of the file name in **lower case**
   followed by ```-0000-0000-0000-000000000000```
5. On the next line Create a new value from the previous value stripped of the ```-``` characters
6. Open the ```Players``` folder, there you should see at least 2 files, ```000...001.sav``` is ***your*** file
   - If there are more than 2 files inside, follow the **Client's instructions** to figure out how to acquire ***their*** file name
7. Repeat **instructions 3 through 5** for the ***Client***'s file name
8. Name the values you've just created ```Host_name```, ```Host_guid```, ```Host_group```, ```Client_name```, ```Client_guid``` and ```Client_group``` respectively

If both parties did everything correctly you should end up with a text document that contains 6 values with their associated names similar to this:
```
B8222BF0000000000000000000000000         Host_name
b8222bf0-0000-0000-0000-000000000000     Host_guid
b8222bf0000000000000000000000000         Host_group

F632C4E9000000000000000000000000         Client_name
f632c4e9-0000-0000-0000-000000000000     Client_guid
f632c4e9000000000000000000000000         Client_group

The values above are meant to serve as an EXAMPLE only, using them will corrupt your save
```

<br />

9. Paste the following instructions in your ```Guid``` text document and format them swapping the variables with their associated values
```
1. SEARCH -> ("value": "00000000-0000-0000-0000-000000000001")                                             1.  REPLACE -> ("value": "Host_guid")
2. SEARCH -> ("value": "Client_guid")                                                                      2.  REPLACE -> ("value": "00000000-0000-0000-0000-000000000001")
3. SEARCH -> (_uid": "00000000-0000-0000-0000-000000000001")                                               3.  REPLACE -> (_uid": "Host_guid")
4. SEARCH -> (_uid": "Client_guid")                                                                        4.  REPLACE -> (_uid": "00000000-0000-0000-0000-000000000001")
5. SEARCH -> ("group_name": "00000000000000000000000000000001")                                            5.  REPLACE -> ("group_name": "Host_group")
6. SEARCH -> ("group_name": "Client_group")                                                                6.  REPLACE -> ("group_name": "00000000000000000000000000000001")
7. SEARCH -> ([\r\n                                            "00000000-0000-0000-0000-000000000001")     7.  REPLACE -> ([\r\n                                            "Host_guid")
8. SEARCH -> (,\r\n                                            "00000000-0000-0000-0000-000000000001")     8.  REPLACE -> (,\r\n                                            "Host_guid")
```
> [!CAUTION]
> Additional formatting may be required if your editor does not recognize ```\r\n``` as a line break

<br />

Your ```Guid``` text document is now in its complete state and should look similar to this:
```
B8222BF0000000000000000000000000         Host_name
b8222bf0-0000-0000-0000-000000000000     Host_guid
b8222bf0000000000000000000000000         Host_group

F632C4E9000000000000000000000000         Client_name
f632c4e9-0000-0000-0000-000000000000     Client_guid
f632c4e9000000000000000000000000         Client_group

1. SEARCH -> ("value": "00000000-0000-0000-0000-000000000001")                                             1.  REPLACE -> ("value": "b8222bf0-0000-0000-0000-000000000000")
2. SEARCH -> ("value": "f632c4e9-0000-0000-0000-000000000000")                                             2.  REPLACE -> ("value": "00000000-0000-0000-0000-000000000001")
3. SEARCH -> (_uid": "00000000-0000-0000-0000-000000000001")                                               3.  REPLACE -> (_uid": "b8222bf0-0000-0000-0000-000000000000")
4. SEARCH -> (_uid": "f632c4e9-0000-0000-0000-000000000000")                                               4.  REPLACE -> (_uid": "00000000-0000-0000-0000-000000000001")
5. SEARCH -> ("group_name": "00000000000000000000000000000001")                                            5.  REPLACE -> ("group_name": "b8222bf0000000000000000000000000")
6. SEARCH -> ("group_name": "f632c4e9000000000000000000000000")                                            6.  REPLACE -> ("group_name": "00000000000000000000000000000001")
7. SEARCH -> ([\r\n                                            "00000000-0000-0000-0000-000000000001")     7.  REPLACE -> ([\r\n                                            "b8222bf0-0000-0000-0000-000000000000")
8. SEARCH -> (,\r\n                                            "00000000-0000-0000-0000-000000000001")     8.  REPLACE -> (,\r\n                                            "b8222bf0-0000-0000-0000-000000000000")

The values above are meant to serve as an EXAMPLE only, using them will corrupt your save
```
<br />

After verifying and confirming that you've replaced the variables with their correct values, you may save and close the ```Guid``` file, we'll return to it shortly

<br />

## Step 4 - Preparing the files

1. Copy the following files into the ```Work``` folder
```
Level.sav
Players\000...001.sav
Players\Client_Guid.sav
```

2. Drag and drop the copied files one by one onto the ```convert-single-sav-to-json.bat``` file in the ```palworld-save-tools``` directory
> [!WARNING]
> Converting ```Level.sav``` to ***JSON*** may take some time and will produce a large file of **~2GB**

3. Copy the newly generated ***JSON*** files from the ```Work``` folder into the ```JSON_backup``` folder
>[!TIP]
> This backup will serve as a fallback point for you to avoid repeating the conversion process should anything go wrong

## Step 5 - Editing player files

Using the text editor of your choice, open the newly generated ```player.sav.json``` files from the ```Work``` folder
   
### In ```000...001.sav.json```
- Replace all occurrences of ```00000000-0000-0000-0000-000000000001``` with ```Host_guid```
- Save and close the file

<br />
     
### In ```Client_name.sav.json```
- Replace all occurrences of ```Client_guid``` with ```00000000-0000-0000-0000-000000000001```
- Save and close the file

<br />

## Step 6 - Editing Level file

Using the text editor of your choice, open the newly generated ```Level.sav.json``` file from the ```Work``` folder
> [!CAUTION]
> **The following actions must be performed in the exact order they're listed in to avoid collisions**

<br />

- 1..8. Open the ```Guid``` text document and follow your own personalized instructions searching for all occurrences and replacing them with their corresponding values between ```(``` and ```)```
<br />

9. Find and replace **ONLY THE FIRST** occurrence of ```00000000-0000-0000-0000-000000000001``` with ```Host_guid```
> [!CAUTION]
> Only applicable if the host has not been changed previously! <sup>see notes</sup>[^5.7]

[^5.7]: If the host has been changed previously, you can no longer rely on their struct's position in the save file, you'll have to manually locate the user's struct using their NickName or InstanceID which can be found in their player file, the GUID will be located at the top of the struct

<br />

10. Replace **ALL** occurrences of ```Client_guid``` with ```00000000-0000-0000-0000-000000000001```
11. Save and close the file

<br />

## Step 7 - The Grand Finale

Now with the tedious part out of the way, there are just a few simple steps left

<br />

1. Convert the edited ***JSON*** files back to ***SAV*** by dragging them one by one onto the ```convert-single-json-to-sav.bat``` file in the ```palworld-save-tools``` directory
2. Rename the newly generated ```000...001.sav``` file to ```Host_name.sav```
3. Rename the newly generated ```Client_name.sav``` file to ```00000000000000000000000000000001.sav```
4. Replace the old files in your save folder with their edited versions

### Lastly, the contents of the save folder should be transferred to the new Host and dropped into the save folder
> [!NOTE]
> To retain the map data, both parties should keep their ```LocalData.sav``` files

> [!NOTE]
> Both the host and the client might have to disable steam cloud to load the save for the first time

<br />

## Testing

If the original ***Host*** attempts to load the save
- The ***Host*** will take over the ***Client***'s character and progress
- The ***Client*** will be prompted with the character creation screen

If the ***Client*** attempts to load the save
- Both the ***Client*** and the ***Host*** will retain their own characters and progress

<br />
  
## Conclusion

If you managed to follow me to this point then ***Congratulations!***

You have successfully swapped roles, characters and progress with the second party.

<br />
  
### The ***Host*** is now the ***Client***
### The ***Client*** is now the ***Host***

<br />
  

<br />

## Credits

### Huge thanks to [cheahjs](https://github.com/cheahjs) for making this possible!

<br />
<br />

### Notes


