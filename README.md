# ZenBrowser
Download Zen Browser using apt

sudo curl -fsSL https://anmolbhat.github.io/ZenBrowserAPT/zen-archive-keyring.gpg \
  -o /etc/apt/keyrings/zen-archive-keyring.gpg

echo "deb [signed-by=/etc/apt/keyrings/zen-archive-keyring.gpg] https://anmolbhat.github.io/ZenBrowserAPT stable main" \
  | sudo tee /etc/apt/sources.list.d/zen.list
  
sudo apt update
apt policy zen-browser
sudo apt install zen-browser
