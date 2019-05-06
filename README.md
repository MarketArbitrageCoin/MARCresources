# Market Arbitrage Coin

This script is used to setup MARC masternode. This script supports 9 OS systems. Which are : Ubuntu 14/16/17/18, CentOS 7, Debian 8/9 & Fedora 27/28/29.
This script also provides other benefits :  
1. User can setup more than 1 MARC MN on the same VPS.
2. Support for IPv4 & IPv6
3. On-screen instructions for Local wallet

To setup more than 1 MN on same VPS, please note some of the followings :    
 * Insure you have additional public ip address for each additional masternode
 * Run script in **CUSTOM** settings mode (using full questionnaire)
 * Select option to create new user for additional MN (masternodes isolated by using different accounts).


***

## VPS installation

For users who have setup MN using previous script version, users can update their script using the following link:

```
wget -O marcmnupdate.sh https://unclear.space/repo/marc/update/marcmnupdate.sh; chmod +x marcmnupdate.sh
```
Run Script :
```
./marcmnupdate.sh
```

For fresh VPS installations, you can use the following link:
```
wget -O marcmnautosetup.sh https://unclear.space/repo/marc/marcmnautosetup.sh; chmod +x marcmnautosetup.sh
```
Run Script :
```
./marcmnautosetup.sh
```

Users can follow installation steps like in the following video :
https://discord.gg/Kc8VNqK

***
## Desktop wallet setup


After the Masternode is up and running, you need to configure the desktop wallet accordingly. Here are the steps:

1. Open the **MARCoin** Desktop Wallet.

2. Go to **RECEIVE** and create a **New Address** name it **MN1** *(name can be adjusted to user's choice)*

3. Generate private key for MN1. Go to **Help -> Debug Window > Console** and type :  
``dumpprivkey <wallet_address_MN1>. ``   

**Important Note :**
*Private key must be stored in a safe place. Private key is very necessary when user want to do wallet restoration. Access to your wallet private key gives full control over the balance and wallet address.*


4. Generate masternode private key. Go to **Help -> Debug Window > Console** and type : 
``masternode genkey``.

5. Send **5000** MARC to MN1. **User need to send exact 5000 coins in one single transaction. Wait for 18 confirmations.** 

6. Get transaction info for masternode activation. Go to **Help -> Debug Window > Console** and type the following command: ``masternode outputs``

7. After typing masternode outputs, user will have these results :
```
"txhash" : "<txhash>",
"outputidx" : <txindex>
```

8. Masternode configuration preparation. Go to **Tools -> Open Masternode Configuration File**. Add the following entry:

```Alias Address Privkey TxHash TxIndex```   

Alias: MN1  
Address: VPS_IP:PORT  
Privkey: Masternode Private Key  from Step 4
TxHash: First value from Step 6  
TxIndex: Second value from Step 6  

Result will be like this :  
```MN1  VPS_IP:44004 masternodeprivkey TxHash TxID```

9. Save and close the file.

10. Click Update status to see user MN. If it is not shown, close the wallet and start it again. Make sure wallet is unlocked.

11. Select MN1 and click Start Alias to start it. Another alternative, Go to Help > Debug Window > Console and type startmasternode alias false MN1.   
If successful, you will get the following output : Masternode successfully started.

12. Check masternode status in user VPS. Login to VPS and check masternode status by typing this commands :  
```~/marc-sym/marcoin-cli masternode status```  
Output result will be like this :
```
“txhash” : “<txhash>”
“outputidx” : “<txid>”
“netaddress” : “vps_ip:44004”
“status” : 4
“message” : “masternode successfully started”
```
***

## Commands:

**VPS Commands :**
```
~/marc-sym/marcoin-cli mnsync status => to check if user's MN is fully synced.
~/marc-sym/marcoin-cli masternode status => to check user's Masternode.
~/marc-sym/marcoin-cli stop => to stop marcoin services.
~/marc-sym/marcoin-cli -daemon => to start marcoin services.
~/marc-sym/marcoin-cli -daemon -resync => to start marcoin services with resync.
```

**Desktop/Local Wallet Command**
```
mnsync status => to check if user's wallet is fully synced.
masternode list-conf => to check user's Masternode.
getbalance => to check user balance
getstakingstatus => to check wallet status
listaddressgroupings => to check address in user local wallet.
```

***
