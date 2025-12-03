##  STEP BY STEP GUIDE ON HOW TO SET UP CODEASSIST
<img width="889" height="793" alt="Screenshot 2025-11-06 031324" src="https://github.com/user-attachments/assets/a2a72668-def0-4e9c-b4c7-075e2816bf8e" />
 
 **CodeAssist is a completely private and local AI coding assistant, developed by Gensyn. It helps you practice programming problems and train a novel assistant to help you code.**
#### Unlike typical code assistants, CodeAssist writes directly in your editor as you work. Every keystroke - whether you type, fix, delete, or leave its output untouched - becomes a learning signal. Over time, it adapts to your habits and style, acting more like an apprentice learning from your craft than a tool following commands.

### REQUIREMENTS
#### Local pc Cpu with at least 8gb RAM (Linux, ubuntu or macOS) 
#### Huggingface token get it here, if you don't have one yet https://huggingface.co/
#### Always confirm if your softwares accept `sudo` cmd before running 

## 1 Update system packages
```
sudo apt update && sudo apt upgrade -y
```
## 2 Install docker
#### For Ubuntu/linux
```console 
# install required dependencies
sudo apt install ca-certificates curl gnupg lsb-release -y

# Add Docker’s official GPG key
sudo mkdir -p /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg

# Set up Docker repository
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] \
  https://download.docker.com/linux/ubuntu \
  $(lsb_release -cs) stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

# Install Docker Engine
sudo apt update
sudo apt install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin -y

# Start and enable Docker
sudo systemctl start docker
sudo systemctl enable docker

# Verify installation
docker --version

# You should see something like:
# Docker version 27.0.3, build xxxxxxx

```
#### for mac users, download the docker desktop (https://www.docker.com/products/docker-desktop/ incase you haven't downloaded it yet) and verify docker on your terminal using
#### Verify docker version
```
docker --version
```
### 3 Install python 
```
sudo apt install python3 python3-pip python3-venv python3-dev -y
```
#### verify python version
```
python3 --version
```
### 4 Install UV 
#### Required to to manage the dependencies of the main script.
##### for linux/ubuntu
```
curl -LsSf https://astral.sh/uv/install.sh | sh
```
##### for macOS
```
brew install uv
```
### 5 Download the Codeassist
#### Clone the repository
```
git clone https://github.com/gensyn-ai/codeassist.git
cd codeassist
```
### 6 Run the Code
```
uv run run.py
```
##### You'll see something like what's on the screen below 
<img width="1555" height="868" alt="image" src="https://github.com/user-attachments/assets/1b38fcf5-0529-44a4-b5d6-15eb20b40679" />

#### Wait for it to load finish and also get your hugging face token ready. generate it with `write` access, that's if you don't have one 
#### After script running ends, it will automatically take you to a website to login with your email or if it dosen't, use this http://localhost:3000/ to open CodeAssist.
#### After logging in your credentials will be stored in `persistent-data/auth/userKeyMap.json` 
<img width="1903" height="762" alt="image" src="https://github.com/user-attachments/assets/252ee342-9bb6-48e2-b63a-1101554d7715" />

#### Once logged in, you can select Easy, Medium, or Hard problems from the sidebar. CodeAssist will begin recording an episode. Every click, keystroke, edit, or deletion is logged as training feedback.
#### When you stop typing, CodeAssist takes initiative. It writes directly into your file without any pop-ups or confirmations. Whether you accept, modify, or remove its edits, each interaction contributes to the model’s understanding of your preferences.
### Tips and Tricks
#### > Use `Shift+Space` or click the Pause Assistant button to temporarily stop the assistant. The first keystroke after pausing will unpause it.
#### > Keep your cursor near the section you're working on, as CodeAssist inserts code relative to your cursor position.
#### > When the assistant produces a "No-Op" (does nothing), it's waiting for you. This is intentional and signals it's your turn to act.

### Training
#### CodeAssist continuously records your interactions while the web UI is running. To complete an episode and train your model, press `Ctrl+C` in the terminal where CodeAssist is running.
#### You do not need to successfully solve a LeetCode problem to train the model. You can stop recording the episode by leaving the CodeAssist web UI, returning to the terminal CodeAssist is running in, and using the ctrl+c command to start training.
#### During training, CodeAssist will:
#### > Compare your edits to the assistant's actions
#### > Calculate rewards and penalties based on your interactions
#### > Update your local model checkpoint
#### > Store new model weights under `persistent-data/trainer/models` 
#### > Upload your trained model to Hugging Face (if a valid token is provided)
##### After training completes (which takes a few minutes depending on your system), you can restart CodeAssist to use your updated model trained on your most recent episode.
### Best Practices
#### > Be patient: The assistant watches your typing and timing. Working too quickly or aggressively correcting can neutralize training efficacy.
#### > Treat it as a collaborator: Let it naturally interject code and keep useful code around briefly before editing or removing.
#### > Don't delete everything instantly: If you delete everything it writes right away, you're teaching it to stop acting altogether.
#### > Record multiple varied problems: Diversify its learning signals by working on different problems.
#### > Expect gradual improvement: Early episodes may feel inconsistent. Improvement becomes clearer after 4-5 episodes of training.

### GOOD LUCK GUYS!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!
