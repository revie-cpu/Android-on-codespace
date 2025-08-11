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

Create a file named `android.yml` with this content:

```
version: "3.8"
services:
  android:
    image: budtmo/docker-android:emulator_7.1.1_v2.12.0
    privileged: true
    environment:
      - DEVICE=Nexus_5
      - WEB_VNC=true
      - AUTO_START=true
      - APPIUM=false
      - EMULATOR_ARGS=-gpu swiftshader_indirect
      - TZ=Asia/Dhaka
      - LOG_WEB_SHARED=false
    ports:
      - "6080:6080"
      - "5555:5555"
    shm_size: 4g
    volumes:
      - android_data:/data
    restart: unless-stopped

volumes:
  android_data:

```

---
# Start the CODE (YAY)

### Enter it ine the terminal

```
docker compose -f android.yml up
```
---
#   (OPTIONAL) 
### (Optional) Connect via ADB
```
sudo apt update
sudo apt install android-tools-adb
adb connect localhost:5555
```
---
THANKS FOR DOING THIS CREDIT ME

(NOTE : IT MIGHT TAKE TIME TO LOD ON THE GOOGLE SCREEN)

BYE BYE
