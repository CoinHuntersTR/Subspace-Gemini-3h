# Subspace-Gemini-3h

# <h1 align="center">Subspace Network Node Kurulumu (Gemini 3h)

  
 ![image](https://user-images.githubusercontent.com/107190154/191179355-ac1b6ff1-095b-4937-8f2c-8578c0774345.gif)

### Sistem Gereksinimleri 

|CPU | RAM  | Disk  | 
|----|------|----------|
|   4| 8GB  | 160GB     |

  
  # NODE KURULUMU
  
  ## Sistem Güncelleme
  
   ### Sistem güncellemesi yapıyoruz
  ```
  sudo apt update && sudo apt upgrade -y
  ```
  
  ## Kütüphanelerin Kurulumu
   ```
sudo apt install ocl-icd-opencl-dev ocl-icd-libopencl1 libopencl-clang-dev libgomp1 -y && sudo apt install wget -y && cd $HOME
  ```
  ## Subspace Node ve Farmer Dosyalarını indiriyoruz.
  ```
  wget https://github.com/subspace/subspace/releases/download/gemini-3h-2024-feb-05/subspace-farmer-ubuntu-x86_64-skylake-gemini-3h-2024-feb-05
  ```
  ```
  wget https://github.com/subspace/subspace/releases/download/gemini-3h-2024-feb-05/subspace-node-ubuntu-x86_64-skylake-gemini-3h-2024-feb-05
  ```
   ## Binary dosyalarına yetki veriyoruz
  ```
   sudo mv subspace-node-ubuntu-x86_64-skylake-gemini-3h-2024-feb-05 /usr/local/bin/subspace-node
   sudo mv subspace-farmer-ubuntu-x86_64-skylake-gemini-3h-2024-feb-05 /usr/local/bin/subspace-farmer
  ```
  ```
 mkdir subspacenode
 sudo chmod 700 ~/subspacenode
 mkdir subspacefarmer
 sudo chmod 700 ~/subspacefarmer
  ```
##  Node için subspaced isimli bir servis dosyası oluşturalım; (NODEISMINIYAZ kısmına istediğiniz node isminizi yazmayı unutmayın!)
```
sudo tee <<EOF >/dev/null /etc/systemd/system/subspace-node.service
[Unit]
Description=Supsapce Node
After=network.target

[Service]
User=$USER
ExecStart=subspace-node run  --chain gemini-3h --base-path /root/subspacenode --farmer --name 'NODEISMI'
Restart=always
RestartSec=10
LimitNOFILE=10000

[Install]
WantedBy=multi-user.target
EOF
  ``` 
  
 ## Node servislerini başlatalım
  ```
  sudo systemctl daemon-reload
  ```
  ```
  sudo systemctl enable subspace-node.service
  ```
  ```
  sudo systemctl restart subspace-node.service
  ```
# [BURADAN](https://chrome.google.com/webstore/detail/polkadot%7Bjs%7D-extension/mopnmbcafieddcagagdcbnhejhlodfdd) Polkadotjs cüzdan indiriyoruz.

### [Buradan](https://coinhunterstr.com/polkadot-cuzdan-nasil-olusturulur-2/) Detaylı Kurulum Rehberine ulaşabilirsiniz.

### Testnete katılmak için gerekli cüzdan adresini; cüzdanımıza bu ayarları yaptıktan sonra, gelen adresi kopyalıyoruz.


  ## Farmer için subspace-farmer isimli bir servis oluşturalım;
  
  ### CUZDANADRESI kısmına ödül almak istediğiniz cüzdan adresini giriyoruz.

  ```
  sudo tee <<EOF >/dev/null /etc/systemd/system/subspace-farmer.service
[Unit]
Description=Subspace Farmer
After=network.target

[Service]
User=$USER
ExecStart=subspace-farmer farm --reward-address CUZDANADRESI path=/root/subspacefarmer,size=SIZE
Restart=always
RestartSec=10
LimitNOFILE=10000

[Install]
WantedBy=multi-user.target
EOF
  ```
 ## Farmer servislerini başlatalım
  ```
  sudo systemctl daemon-reload
  ```
  ```
  sudo systemctl enable subspace-farmer.service
  ```
  ```
  sudo systemctl restart subspace-farmer.service
  ```  
## Node loglarımıza bakıyoruz.
  ```
 journalctl -u subspace-node.service -f
  ```  

## Farmer loglarımıza bakıyoruz.
  ```
 journalctl -u subspace-farmer.service -f
  ```  
![supspace2](https://user-images.githubusercontent.com/111747226/191376523-09d78401-83d8-46d1-9344-924344208f73.png)
  
## Sync kontrol etmek için 
  ### isSynincg:false çıktısı almanız lazım
  ```
 curl -H "Content-Type: application/json" -d '{"id":1, "jsonrpc":"2.0", "method": "system_health", "params":[]}' http://localhost:9933
  ```   
![subspace 3](https://user-images.githubusercontent.com/111747226/191377150-74d43064-261d-4bf4-bb70-8bd8b6cf298b.png)
  
 ## Subspace Network Linkler;
  
### [Discord](https://discord.gg/subspace-network)
### [Twitter](https://twitter.com/NetworkSubspace)
### [Web](https://subspace.network/)
### [Subspace Explorer](https://telemetry.subspace.network/#list/0x0c121c75f4ef450f40619e1fca9d1e8e7fbabc42c895bc4790801e85d5a91c34)
 
 
