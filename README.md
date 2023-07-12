Гайд по установке узла

Высота блока моментального снимка 05.10.22 (2,4 ГБ) --> 361346

# 1. install the node as standard, but do not launch.
# 2. delete the .data directory. 
# 3. create an empty directory
sudo systemctl stop haqqd
rm -rf $HOME/.haqqd/data/
mkdir $HOME/.haqqd/data/

# 4. download archive
cd $HOME
wget http://88.198.34.226:7150/haqqddata.tar.gz

# 5. unpack the archive
tar -C $HOME/ -zxvf haqqddata.tar.gz --strip-components 1

# 6. run the node after unpacking. Don't forget to delete the archive to save space
cd $HOME
rm haqqddata.tar.gz
systemctl restart haqqd && journalctl -u haqqd -f -o cat

sed -i -e "s/^pruning *=.*/pruning = \"nothing\"/" $HOME/.haqqd/config/app.toml 
systemctl restart haqqd && journalctl -u haqqd -f -o cat

# 7. ждем полной синхронизации
