# BASIC TERMINAL KNOWLEGE NEEDED
---

## Setup

### Download the packages

```
# 1. Install dependencies
sudo apt update
sudo apt install -y apt-transport-https ca-certificates curl gnupg lsb-release

# 2. Add Docker's official GPG key
sudo mkdir -m 0755 -p /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg

# 3. Add Docker's official repo
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu \
  $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

# 4. Install docker-compose-plugin
sudo apt update
sudo apt install -y docker-compose-plugin
```
Just put it in the Terminal

### Create `android.yml` and run it

Create a file named `android.yml` with this content (made faster in update):

```
version: '3.8'

services:
  android:
    image: budtmo/docker-android:emulator_11.0
    privileged: true
    devices:
      - /dev/kvm:/dev/kvm
    environment:
      - DEVICE=Nexus_5x
      - WEB_VNC=true
      - AUTO_START=true
      - EMULATOR_ARGS=-gpu host -no-window -skin 1080x1920
      - SNAPSHOT=true
      - TZ=Asia/Dhaka
    ports:
      - "6080:6080"
      - "5555:5555"
    shm_size: 20g
    restart: unless-stopped


```

---
# Start the CODE (YAY)

### Enter it ine the terminal

```
docker compose -f android.yml up
```
---
#   (OPTIONALS STUFF) 
### (Optional) Connect via ADB
Make a new terminal and do this
```
docker exec -it codespaces-blank-android-1 bash
cat /proc/cpuinfo | grep vmx
```
### ( def not Optional) How to Download apps dont do this on the adb please make a antoher new terminal plase(since  no GOOGLE PLAY STORE DEFINETIELY NOT GETTING FIXED)

```
 wget --referer="https://apkfiledownloadweb.com" --user-agent="Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/115.0.0.0 Safari/537.36" "https://apkfiledownload.com/full-link" -O APKNAME.apk
```
like this
```
  wget --referer="https://www.apkmirror.com/" --user-agent="Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/115.0.0.0 Safari/537.36" "https://www.apkmirror.com/wp-content/themes/APKMirror/download.php?id=8805694&key=283d012af4e3ac709b5affed1fdcc142a1d82915&forcebaseapk=true" -O googledrive.apk
```
then copy to a anthor place to install
```
docker cp APKNAME.apk codespaces-blank-android-1:/tmp/APKNAME.apk
```
now go to adb terminal and paste this (to install)
```
adb install /tmp/APKNAME.apk
```
your all set! now
### save a snapshot (to load where you left off)
```
adb emu avd snapshot save default
```
and load it 
```
adb emu avd snapshot load default
```

### Find packages (apps) to uninstall and list
```
adb shell pm list packages
```
then it will show you the list of apps or packages whatever you call it
IF you want to find the specific app using a key word
```
adb shell pm list packages | grep KEYWORD
```
like 
```
adb shell pm list packages | grep google
```
to unintall
```
adb shell pm uninstall --user 0 package.name.here
```
# MORE COMING SOON 
---
THANKS FOR DOING THIS CREDIT ME

(NOTE : IT MIGHT TAKE TIME TO LOD ON THE GOOGLE SCREEN)

BYE BYE
