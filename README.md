# canopy_docs

## How to login to the box
1. If you are running an operating system by the all mighty pinguin you should be good from the go with an ssh client. Should you for some reason not have an ssh client you can install one by opening up a terminal and run `sudo apt install openssh-client`
2. If you are like most people, you run a Windows computer. Windows does not natively support ssh as a protocol so you must install an ssh client. A simple and easy one to use is Putty. Putty can be downloaded [here](https://apps.microsoft.com/store/detail/putty/XPFNZKSKLBP7RJ) from the Microsoft Store.
3. If you already know what a private key is and you have one please skip to step [7]. If not you will need to create a private key. This can be done via another tool of putty called puttygen. (you can click on the download link for your version of windows: [64-bit x86](https://the.earth.li/~sgtatham/putty/latest/w64/puttygen.exe), [64-bit Arm](https://the.earth.li/~sgtatham/putty/latest/wa64/puttygen.exe), [32-bit x86](https://the.earth.li/~sgtatham/putty/latest/w32/puttygen.exe)).  
Once you open puttgen, please make sure `RSA` is selected and click `Generate`. Next move your mouse in a random pattern throughout the area marked in red. 
   ![puttygen](/images/puttygen1.PNG)
4. Once finished the blank area will fill with some fields.
- Key Comment: please fill out your name here, or at least the name we all know you by. this makes key management on the server a hell of a lot easier.
- Key Passphrase: this is a password of your own choosing, and remember, passwords are like underware, we don't share them with other people. 
- Confirm passphrase: please type in the same password as above. 
![puttygen](/images/puttygen2.PNG)
5. Now pay attention. You need to save two files now. first click on the button `Save private key` and save it somewhere safe. (_Caution: in the current version of puttygen the private key isn't saved with the proper ppk extention. please make sure to add `.ppk` at the end of your filename_). Once saved click on the button `Save public key` and save this file. 
6. Now share the public key (*This is the second file you saved*) with somebody who has box access and can add your public key to the box
7. Open up putty and let's save a connection to the box.  
![putty](/images/putty1.PNG)
8. At the top enter the IP adress of the box (where it says `Host Name (or IP adress)`). Please ensure the port is marked as `22` and the option `SSH` is selected
9. In the left hand menu navigate down to `Connection`->`SSH`->`Auth`->`Credentials`
10. Click the `Browse` button next to the box `Private key file for authentication` and select your private key (_The first file you saved while using puttygen.exe_)
11. Navigate back to the top of the left hand menu and select Session, you should now be back on the start screen of putty.
12. Type `Canopy is the best` in the input box of `Saved Sessions` and click `Save`. You should now see that listed in the big white box below it.
13. Now every time you want to connect to the box you just double-click `Canopy is the best`
14. Once clicked you will be greeted by a black screen (the terminal) saying `login as:`
15. Fill out the username `minecraft` and hit enter. You will be asked for you passphrase (_the password you created earlier_). Fill it out (it won't show any letters or * on the screen, that is normal) and hit enter again
16. Do a little victory dance because you have just logged into the box.
17. To exit the box simply type `exit`

## Basic explanation stuff about the box - screens - yes, read it
If you are a technical egg-head it's good to know that both survival and creative, together with the proxy are running in screens. 

If you are not a technical egg-head. To run our servers (creative and survival) we also need a thing called a proxy (Velocity) to make sure we can run it all from a single box. All that magic is somewhat hidden on the server. This section will talk about that.
The magic is called `screen` it's basically a way to keep something running in the background. To see screens we currently have you can enter the comamnd `screen -ls`  
![Screen](/images/screen.PNG)
This will show the current screens that are running on the box. Important here is the end of the row. `(Detached)`. This means that this screen can be pulled up and be interacted with. Should this say `(Attached)` it means somebody already has this screen open (_or forgot to properly close/detach it_)

To open a screen (let's take the survival server here) we can simply type `screen -r s5_canopy` and hit enter (or screen -r [resume] and then the name of the screen as shown in the list.)

Now you are in the server console itself. To leave the screen (properly detached) you can simply enter the keyboard shortkey [CTRL-A-D] and the screen will detach, leaving you back in the box

!---------------------------! WARNING !---------------------------!  
```
SHOULD YOU EVER FEEL A NEED TO COPY PASTE SOMETHING FROM THE BOX, WHATEVER YOU DO, DO NOT CTRL-C IT. AS THIS WILL SHUTDOWN THE SERVER
```
!---------------------------! WARNING !---------------------------!  
Should you feel a need to copy stuff, just select it with the mouse, it will be automatically copied to the clipboard.

Basics about folder navigation on a linux system (which is what our box is) can be found on [youtube](https://www.youtube.com/watch?v=dzHscTzpAME)

## How to start and stop a server
To stop the server just open the relevant screen as seen in the above section and press [CTRL-C]. Easy, wasn't it?

To start the server go to the respective server folder f.e. `/home/minecraft/s5_canopy` (although chances are very high you are already in the correct folder automatically) and enter the command `./startup.sh`. You should see a bunch of text scrolling over the screen indicating the server is starting

## How to update the motd (message of the day)
The motd is controlled by a custom plugin called QoL. 
- So in a first step navigate to the plugin folder `/home/minecraft/s5_canopy/plugins/QoL`
- Open the config file by entering the command `nano config.yml`
- Use the down arrow on your keyboard to scroll down untill you see the following section
```yaml
server-list:
  # Set max to 0 to disable
  max: 150
  motd: 'Where everyone chooses the beef'
  favicon: 'formaumybeloved.png'
```
- Here you can freely change the motd, just make sure the ' quotation marks are both still there
- you can choose any of the images that are listed in the QoL plugin folder
- [CTRL-X] to exit
- you will be prompted to `Save modified buffer`
- Enter Y for yes and N for no

To activate the new motd the server needs to be rebooted, this is done automatically each day

## How to add hats

**Important note**  
The resourcepack for canopy uses a custom `canopymc` namespace. This is to make sure that it does not interfere with any other resourcepack's that the player might be using that still use the custom namespace as is seen in most tutorials.

### Instructions on adding new items to the canopymc resource pack

#### **Adjust Namespaces**  
Open up the custom model .json file and search the file for any references to custom. This is a product of using a `custom` namespace as most tutorials indicate. Change all occurrences to canopymc
  

#### **Copy Files**  
- Copy the custom model (the actual json file) to `\[pack]\assets\minecraft\models\block\canopymc\`
- Copy any custom block textures to `\[pack]\assets\minecraft\textures\block\canopymc\`
  

#### **Add custom model to the base model**
- Open up the base model that the custom model was based upon (f.e. carved_pumpkin.json)
- Add an entry to the `overrides` node where:
  - The `custom_model_data` is an increment one higher of the last entry
    - `[your_custom_model]` is your model name without the .json
```json
    {
      "predicate": {
        "custom_model_data": 3
      },
      "model": "block/canopymc/[your_custom_model]"
    }
```

#### **Zip and rename**  
Due to the nature of how Mojang treats resource packs it will only prompt the player for a new download if:
- The name of the resource pack has changed
- The SHA key got updated
Since I was unable to get the resource pack working with a proper SHA key I went for the method of the pack name.
The current format for the pack is `canopy[YYYYMMDDHHMM].zip`

#### **Upload the pack**
Log into the box via sFTP and upload the pack to `/home/minecraft/resourcepacks`. 

#### **Update server.properties**
open `server.properties` and update
```
resource-pack=https\://www.canopymc.net/assets/resourcepacks/[new_pack_zip_file_name]
resource-pack-sha1=[new_sha1_key]
```

Folder structure of the resourcepack
```
canopy202403072253
+-- assets
  +-- minecraft
    +-- models
      +-- block
        +-- canopymc
          --- canopy_hat.json
          --- propeller_hat.json 
      +-- item
        --- carved_pumpkin.json
    +-- textures  
      +-- block
        +-- canopymc
          --- ...
          --- ...
      +-- misc
        --- pumpkinblur.png
--- pack.mcmeta
--- pack.png
```

## How to copy paste from console

SHOULD YOU EVER FEEL A NEED TO COPY PASTE SOMETHING FROM THE BOX, WHATEVER YOU DO, DO NOT CTRL-C IT. AS THIS WILL SHUTDOWN THE SERVER.  
Should you feel a need to copy stuff, just select it with the mouse, it will be automatically copied to the clipboard.