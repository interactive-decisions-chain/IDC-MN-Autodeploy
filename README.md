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
`https://raw.githubusercontent.com/interactive-decisions-chain/IDC-MN-Autodeploy/master/mn_install.sh`
