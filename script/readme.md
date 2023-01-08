`Make New Wallet or Main Wallet Mnemonic`

### Install Nodejs
```
curl -sL https://deb.nodesource.com/setup_17.x -o /tmp/nodesource_setup.sh
# read the script file and when you're sure it's safe run it
chmod +x /tmp/nodesource_setup.sh
/tmp/nodesource_setup.sh
apt install nodejs -y
node --version
> v17.9.0
npm --version
> 8.5.5
```

### Clone 
```
git clone https://github.com/eco-stake/restake
cd restake
npm install
cp .env.sample .env
nano .env
```
### Update NPM
```
git pull
npm install
```

### Script

```
nano $HOME/restake/restake.sh
```

```
#!/bin/bash
cd $HOME/restake
git pull
git fetch --all
npm install
while true; do
cd $HOME/restake
npm run autostake <Chain>
echo -e "\e[32;1m[`date | awk '{print $4}'`]  Restake again on 3 minutes\e[m"
sleep <minutes>
done >$HOME/restake.log 2>&1 &
```

### Create Network.local.json `Restake/src`
```
{
  "planq": {
    "prettyName": "planq",
    "restUrl": [
      "https://rest.planq.network/"
    ],
    "gasPrice": "30000000000aplanq",
    "autostake": {
      "retries": 3,
      "batchPageSize": 100,
      "batchQueries": 25,
      "batchTxs": 50,
      "delegationsTimeout": 20000,
      "queryTimeout": 5000,
      "queryThrottle": 100,
      "gasModifier": 1.1
      }
  },
  "planq": {
    "prettyName": "planq",
    "autostake": {
      "correctSlip44": true
    }
  }
}
```

  
  ### Submit Your Operator Validator
### Make PullRequest >>> [PR](https://github.com/eco-stake/validator-registry)

Create `profile.json`
```
{
  "$schema": "../profile.schema.json",
  "name": "Name",
  "identity": "ID                          "
 }
 
 ```
 Create `chains.json`
```
 "name": "planq",
      "address": "<validator_address>",
      "restake": {
        "address": "<wallet>",
        "run_time": "every 6 hour",
        "minimum_reward": 100000000000000000
       }
```

### Grant
```
planqd tx authz grant plq1csj5g5j4r682apvjckdk3qldkup4y0742nl8ac generic --msg-type /cosmos.staking.v1beta1.MsgDelegate --from wallet
```

### Edit Permissions
```
cd $HOME/restake
chmod +x restake.sh
```

### RUN
```
./restake.sh
```

### Check Log
```
tail -f -n 1000 $HOME/restake.log
```


`Tribute to Jambulmerah`

