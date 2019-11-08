# PSCP
### window to linux
```
pscp -i 190822pem.ppk -r C:\Users\multicampus\Desktop\aws-vm\ ubuntu@13.124.65.11:\var\lib\tomcat9\webapps

pscp -i 190904pem.ppk -r C:\Users\multicampus\Desktop\aws-vm\putty\AuctionConsortium ubuntu@13.209.80.76:~

pscp -i 191018pem.ppk -r C:\Users\multicampus\Desktop\dist ubuntu@13.124.143.135:
```
### linux to window
```
pscp -i 190904pem.ppk -r ubuntu@13.209.80.76:AuctionConsortium/chaincode/node/AssetManagement.js C:\Users\multicampus\Desktop\Auction
```

