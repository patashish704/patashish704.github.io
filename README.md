Contents:
{:toc}
# Improve_Productivity_with_Linux
Here I provide a series of tips that will drastically improve your productivity
in Linux. To give full credit the original developers, I will give direct link 
to their work, and will provide additional information where it is warranted.

## Faster transfers between remote server and client
The scp and rsync are great for transferring small files, like your source code
because they apply sufficiently secure encryption. For large files, however, they 
choke, especially when the physical separation between client and the remote is 
huge, e.g., between transatlantic countries. A touted method is hpnssh patch, but 
that method did not work for me. 

A robust alternative is to use OneDrive or Dropbox if you have an account. The 
basic subscription of OneDrive provides 5GB of storage. The business one offers
1 TB. The idea is to have a OneDrive ( or Dropbox ) folder on both the remote 
and the client. The automatic syncing will give you far more transfer speed than
you would ever see in rsync or scp. 

### OneDrive in Linux
Make sure you have git installed. Use the one provided by your linux distribution:
```sh
sudo apt install git
```

Clone the OneDrive software written by skilion:
```sh
mkdir ~/git-repos && cd ~/git-repos
git clone https://github.com/skilion/onedrive.git
```

Follow the instructions given on the webpage https://github.com/skilion/onedrive
to install the software. 

NOTE:
1. Open your OneDrive web account and see which folders you want to sync. I have
created a folder called scp_transfers one my web OneDrive account only for the 
purpose of transferring huge data files. 
2. My ~/.config/onedrive/config file looks like this: Make full use of skip_file
feature to skip the files you don't want to sync.
	```sh
	# Directory where the files will be synced
	sync_dir = "~/OneDrive"
	# Skip files and directories that match this pattern
	skip_file = ".*|~*|Attachments|Desktop|Documents|Email attachments|IEEE_manuscript|Notebooks|Pictures"
	```
3. After installation, type `onedrive` in the terminal. You would be given a url, 
which you need to paste in the browser. The browser will ask for your office credentials.
After providing them, you will see a blank page. You need to copy the url in the 
address bar and paste it back in the terminal where it asks, `Enter the response uri`.
If you are installing OneDrive on a remote server via ssh, you can use your local browser
for uri authentication.
4. Follow the instruction on the github page of skilion, to automatically sync 
OneDrive, without you manually having to type `onedrive` in the terminal. 
5. Follow the same set of steps to install OneDrive on both the server and the 
client. After installation, put a very big datafile in ~/OneDrive/scp_transfers
on the server side, and it will be automatically downloaded in ~/OneDrive/scp_transfers
on the client machine. 
6. Use `nethogs` to monitor the download speed. 
That's it ! You should be good to go. 


