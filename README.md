# ZenBrowser
Download Zen Browser using apt

Pulls from Official Zen Desktop GitHub -- Creates GitHub Pages APT Style

#Keyring

sudo curl -fsSL https://anmolbhat.github.io/ZenBrowserAPT/zen-archive-keyring.gpg \
  -o /etc/apt/keyrings/zen-archive-keyring.gpg

#Sources 

echo "deb [signed-by=/etc/apt/keyrings/zen-archive-keyring.gpg] https://anmolbhat.github.io/ZenBrowserAPT stable main" \
  | sudo tee /etc/apt/sources.list.d/zen.list
  
sudo apt update

apt policy zen-browser

sudo apt install zen-browser


#APT Style Publish at
  #Base URl: https://anmolbhat.github.io/ZenBrowserAPT
      #InRelease: /dists/stable/InRelease 
      #Release: /dists/stable/Release 
      #Packages: /dists/stable/main/binary-amd64/Packages
