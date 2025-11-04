# ⚙️ Gensyn Node Setup Guide

![OS Ubuntu](https://img.shields.io/badge/OS-Ubuntu%2020.04+-blue?logo=ubuntu)
![Language Python](https://img.shields.io/badge/Language-Python%203.10+-yellow?logo=python)
![Language NodeJS](https://img.shields.io/badge/Language-Node.js%2022.x-green?logo=node.js)
![Status Stable](https://img.shields.io/badge/Status-Stable-success?logo=github)
![License MIT](https://img.shields.io/badge/License-MIT-lightgrey)

> 🧠 This guide is made for both **beginners** and **advanced users** who want to run a **Gensyn RL-Swarm node** and contribute computing power to the Gensyn network.



![Gensyn Node Dashboard](https://github.com/rajvir00/gensyn-swam/blob/main/2.PNG)

---

## 🧩 Step 1 — System Update

```bash
sudo apt-get update && sudo apt-get upgrade -

```

## 🧰 Step 2 — Install Dependencies

```
sudo apt install screen curl iptables build-essential git wget lz4 jq make gcc nano automake autoconf tmux htop nvme-cli libgbm1 pkg-config libssl-dev libleveldb-dev tar clang bsdmainutils ncdu unzip -y
```

## 🐍 Step 3 — Install Python

```
sudo apt-get install python3 python3-pip python3-venv python3-dev -y
```

## 🧠 Step 4 — Install Node.js and Yarn

```
sudo apt-get update
curl -fsSL https://deb.nodesource.com/setup_22.x | sudo -E bash -
sudo apt-get install -y nodejs
sudo npm install -g yarn
```

**Install Yarn via Script**

 ```
curl -o- -L https://yarnpkg.com/install.sh | bash
```

**Add Yarn to PATH:**

```
export PATH="$HOME/.yarn/bin:$HOME/.config/yarn/global/node_modules/.bin:$PATH"
source ~/.bashrc
```

## ✅ Step 5 — Verify Installations

```
node -v
yarn -v
npm -v
python3 --version
```

## 🧬 Step 6 — Clone Gensyn Repository

```
git clone https://github.com/gensyn-ai/rl-swarm/
```

**Start a new screen session:**

```
screen -S gensyn
```

**Enter the project folder:**

```
cd rl-swarm
```

## 🧱 Step 7 — Create Python Virtual Environment

```
python3 -m venv .venv
source .venv/bin/activate
```

**Update repository:**

```
git switch main
git reset --hard
git clean -fd
git pull origin main
```

## 📦 Step 8 — Install Python Packages

```
pip install --force-reinstall transformers==4.51.3 trl==0.19.1
pip freeze
```

## 🚀 Step 9 — Run the Node

**💡 Tip: If you already have a previous swarm setup, copy your swarm.pen file into the rl-swarm directory before running the command below.**
```
./run_rl_swarm.sh
```
## 🌐 Step 10 — Setup Tunnel Access (New VPS Tab)

Open a new VPS tab and run:

```
sudo npm install -g localtunnel
lt --port 3000
```

This will generate a public tunnel URL for your node dashboard.

![Gensyn Node Dashboard](https://github.com/rajvir00/gensyn-swam/blob/main/756.PNG)

## 🔎 Step 11 — Check Node Status

Reattach to your running session:

```
screen -d -r gensyn
```

## ⚠️ Step 12 — If Node Stops (Red Line Issue)

To restart a stopped node:

```
deactivate
rm -rf .venv

python3 -m venv .venv
source .venv/bin/activate
```
```
git switch main
git reset --hard
git clean -fd
git pull origin main
```

```
./run_rl_swarm.sh
```

# 🐝 Gensyn GSwarm Role Setup Guide

> 🎯 **Goal:** Set up a **GSwarm monitoring bot** that tracks your Gensyn node via Telegram and earns you **“The Swarm” Discord role**.


## 1️⃣ Install GSwarm

### 🧰 Install Go

```
sudo rm -rf /usr/local/go
curl -L https://go.dev/dl/go1.22.4.linux-amd64.tar.gz | sudo tar -xzf - -C /usr/local
echo 'export PATH=$PATH:/usr/local/go/bin:$HOME/go/bin' >> $HOME/.bash_profile
echo 'export PATH=$PATH:$(go env GOPATH)/bin' >> $HOME/.bash_profile
source .bash_profile
```

**Check version:**

```
go version
```

### 🐝 Install GSwarm

```
go install github.com/Deep-Commit/gswarm/cmd/gswarm@latest
```

**Verify installation:**

```
gswarm --version
```

✅ If you see the version output — GSwarm is successfully installed.

## 2️⃣ Setup Telegram Bot

**Step 1 — Create a Telegram Bot**

Open @BotFather on Telegram.

Send /newbot and follow the prompts:

hoose a bot name and username.

After setup, you’ll receive a Bot Token — save it safely.

**Step 2 — Get Your Telegram Chat ID**

Send any message to your new bot.

Visit https://api.telegram.org/bot<YOUR_BOT_TOKEN>/getUpdates

⚠️ Replace <YOUR_BOT_TOKEN> with your actual token (keep the word bot before the token).

Look for your chat ID in the JSON response:


Example:

```
"chat": {
  "id": 123456789,
  "first_name": "GSwarm",
  "username": "gswarm_user",
  "type": "private"
}
```

✅ Your chat ID is 123456789.

💡 Tip: If you get {"ok":true,"result":[]}, send another message to your bot and refresh the URL.

## 3️⃣ Run GSwarm Bot
Run the bot in your terminal:

```
gswarm
```

Then follow the on-screen prompts:
Enter your Bot Token

Enter your Chat ID

Enter your EOA Address ([from the Gensyn Dashboard](https://dashboard.gensyn.ai/))

🧠 The bot will monitor your node’s activity and send you notifications directly in Telegram.

## 4️⃣ Linking Discord and Telegram
To connect your Discord and Telegram accounts:

**Step 1 — Get Verification Code from Discord**
Go to the Gensyn Discord.

In the #｜swarm-link channel, type:

/link-telegram
You’ll receive a verification code.

**Step 2 — Verify in Telegram**
Open your Telegram bot.

**Send:**

```
/verify <code>
```

Replace <code> with the verification code from Discord.

✅ Verification & Earning “The Swarm” Role

![Gensyn Node Dashboard](https://github.com/rajvir00/gensyn-swam/blob/main/Capture.PNG)
