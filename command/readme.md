```
cd $HOME
```

```
wget https://raw.githubusercontent.com/vinjan23/sc/main/autocompound.sh
chmod +x autocompound.sh
```

```
./autocompound.sh
```

```
sudo tee /etc/systemd/system/autocompound.service > /dev/null <<EOF
[Unit]
Description=autocompound
After=network-online.target

[Service]
User=$USER
ExecStart=$(which autocompound) start
Restart=always
RestartSec=3
LimitNOFILE=65535

[Install]
WantedBy=multi-user.target
EOF
```
```
sudo systemctl daemon-reload
sudo systemctl enable autocompound
sudo systemctl start autocompound
journalctl -fu autocompound -o cat
```
