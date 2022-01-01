sudo apt install snapd

sudo apt-get update && sudo apt-get install -yqq daemonize dbus-user-session fontconfig
sudo daemonize /usr/bin/unshare --fork --pid --mount-proc /lib/systemd/systemd --system-unit=basic.target
exec sudo nsenter -t $(pidof systemd) -a su - $LOGNAME

sudo snap install hugo




git add .
git commit -m "first commit"
git branch -M master
git remote add origin https://github.com/DannyJRa/andromeda.git
git push -u origin master


sudo snap install hugo
sudo snap remove hugo
hugo server --themesDir ../..
hugo server -D

echo 'export PATH=$PATH:/snap/bin' >> ~/.bashrc
source ~/.bashrc











#Extended version
wget https://github.com/gohugoio/hugo/releases/download/v0.85.0/hugo_extended_0.85.0_Linux-64bit.deb

sudo dpkg -i hugo_extended_0.85.0_Linux-64bit.deb

hugo version

# following https://gohugo.io/getting-started/quick-start/
# this command just builds the diretory structure
# config.toml  - site config
# archetypes/default.md - default markdown
hugo new site quickstart 
cd quickstart 

git init

# adds themes/ananke
# submodule allows you to keep a git repo as a subdirectory of another git repo
git submodule add https://github.com/budparr/gohugo-theme-ananke.git themes/ananke

# updating all the submodules
# git submodule update --remote --merge

echo 'theme = "ananke"' >> config.toml

# adds into content\posts\my-first-post.md
hugo new posts/my-first-post.md



cd exampleSite/

# Start local dev server
hugo server -D --themesDir ../..