# IDC-MN-Autodeploy
Automated scripts, which are using bash and proceed's MN clean installation on new VPS.

# How that works?
## First steps
The VPS you plan to install your masternode on needs to have at least 1GB of RAM (2GB for I2P) and 10GB of free disk space. We do not recommend using servers who do not meet those criteria, and your masternode will not be stable. We also recommend you do not use elastic cloud services like AWS or Google Cloud for your masternode - to use your node with such a service would require some networking knowledge and manual configuration.

## Fund your node
To get success do the following:
* We need collateral address and collateral TX. Next step is send exactly 20 000 IDC on this address. If you wan't to setup more than one masternode, give it label which you will associate with current masternode.
* Open your IDChain wallet and go to Receive tab.
* Click into the label field and create a label, I will use MN1. *Hint: you also can go to File menu and get address with new label from Receive addresses*
* Now click on "Request payment".
* The generated address will now be labelled as MN1 If you want to setup more masternodes just repeat the steps so you end up with several addresses for the total number of nodes you wish to setup. *Example: For 10 nodes you will need 10 addresses, label them all.*
* Once all addresses are created send 20000 IDC each to them. Ensure that you send exactly 20000 IDC and do it in a single transaction. You can double check where the coins are coming from by checking it via coin control usually, that's not an issue.

As soon as all 20000 transactions are done, we will wait for 15 confirmations. You can check this in your wallet or use the explorer. It should take around 30 minutes if all transaction have 15 confirmations.

## Let's do masternode.conf
After waiting 15 confirmations for the collateral transaction to mature, go to the `Masternodes` tab in your wallet. There you will see a button on the bottom of the wallet that says "configure", click that button to bring up the masternode.conf configuration menu.
*Hint: If you have no active Masternodes tab - switch it **ON** in wallet settings and restart wallet - this tab will appear now.*
* Type in the alias you would like to name your masternode in the `Alias Name` field.
* Paste your VPS IP address in the `VPS Address` field.
* Then click on `Autofill Privkey` and `Autofill Outputs` to fill in the Privkey, Output and Output ID.
* Then click `OK` to automatically enter this information in to your masternode.conf.
* Please restart your wallet after you have completed these steps to finalize your masternode.conf.

##  Installation
SSH (Putty on Windows, Terminal.app on macOS) to your VPS, login as root (*Please note: It's normal that you don't see your password after typing or pasting it*) and run the following command:

`bash <( curl https://raw.githubusercontent.com/interactive-decisions-chain/IDC-MN-Autodeploy/master/mn_install.sh )`

When the script asks, confirm your VPS IP Address and paste your masternode key. (You can copy your key and paste into the VPS if connected with Putty by right clicking)

The installer will then present you with a few options.
**PLEASE NOTE:** Do not choose the advanced installation option unless you have experience with Linux and know what you are doing. Advanced mode will install your masternode under a non-root user called "idchain" instead of root, so you need to know what that means and how to log in as a different user under Linux. If you don't, things will not work as expected and the IDChain team CANNOT help you - you will have to restart the installation.

Follow the instructions the script presents you with.

After the basic installation is done, the wallet will sync. You will see the following message:
```Your masternode is syncing. Please wait for this process to finish.
This can take up to a few hours. Do not close this window.
```
Continue following the instructions as presented.

Once you see "Masternode setup completed." on screen, you are done.

# Non-interactive installation
You can use the installer in a non-interactive mode by using command line arguments - for example, if you want to automate the installation. This requires that you download the installer and run it locally. Here are the arguments you can pass to mn_install.sh:

```
-n --normal               : Run installer in normal mode
-a --advanced             : Run installer in advanced mode
-i --externalip <address> : Public IP address of VPS
--bindip <address>        : Internal bind IP to use
-k --privatekey <key>     : Private key to use
-f --fail2ban             : Install Fail2Ban
--no-fail2ban             : Do nott install Fail2Ban
-u --ufw                  : Install UFW
--no-ufw                  : Do not install UFW
-b --bootstrap            : Sync node using Bootstrap
--no-bootstrap            : Do not use Bootstrap
-h --help                 : Display this help text.
--no-interaction          : Do not wait for wallet activation.
--tor                     : Install TOR and configure idchaind to use it
--i2p                     : Install I2P (Requires 2GB of RAM)
```

If you want to make the installation process fully non-interactive, you need to provide IDChain with arguments for the mode to use, the external IP, private key, and wether to use fail2ban, UFW and the bootstrap, and then also add the `--no-interaction` parameter. Please not that this will not tell you to activate your masternode from your wallet after the node has finished syncing, so it will not run until you do.
