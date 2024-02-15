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
```
```
sudo mv subspace-farmer-ubuntu-x86_64-skylake-gemini-3h-2024-feb-05 /usr/local/bin/subspace-farmer
```
```
sudo chmod +x /usr/local/bin/subspace*
```
```
mkdir subspacenode
```
```
sudo chmod 700 ~/subspacenode
```
```
mkdir subspacefarmer
```
```
sudo chmod 700 ~/subspacefarmer
```

##  Node için subspaced isimli bir servis dosyası oluşturalım;

```
$NODE_NAME=NodeAdınızıYazın
```
```
sudo tee <<EOF >/dev/null /etc/systemd/system/subspaced.service
[Unit]
Description=Subspace Node

[Service]
User=$USER
ExecStart=subspace-node run  --chain gemini-3h --base-path /root/subspacenode --farmer --name '$NODE_NAME'
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

> Aşağıdaki resminde olduğu gibi st ile başlayan adresini ekleyip onu bir yere not edelim.

![Ekran görüntüsü 2024-02-15 140044](https://github.com/CoinHuntersTR/Subspace-Gemini-3h/assets/111747226/e1451b1a-07b6-46c1-8dc9-9a1819fb6e96)

> Bu adrese ulaşabilmek için [BURADAN](https://polkadot.js.org/apps/) polkadot js gidiyoruz.

![Ekran görüntüsü 2024-02-15 140249](https://github.com/CoinHuntersTR/Subspace-Gemini-3h/assets/111747226/17bf69f8-cad4-4635-8e0e-b30ff09e55c9)

> Simgesine bastığınızda birçok ağ göreceksini orada testnet network ağını seçip, Subspace gemini 3g yada 3h seçebilirsiniz. Seçimi yaptıktan sonra en üstten swich diyerek ağı değiştirelim.

![Ekran görüntüsü 2024-02-15 140422](https://github.com/CoinHuntersTR/Subspace-Gemini-3h/assets/111747226/c99a09f6-5276-4d83-a735-ba755dd2cb6b)

> Setting Metadata bölümüne geldiğinizde sizde update çıkacak ona bastığınızda st ile başlayan cüzdan adresine erişmiş olursunuz.

## Farmer için subspace-farmer isimli bir servis oluşturalım;
  
### CUZDANADRESI kısmına ödül almak istediğiniz cüzdan adresini giriyoruz. 
### SIZE bölümüne ise sunucu içinde ayrılacak boyutu giriyoruz. 
```
$ADDRESS=Cüzdanadresiniekleyin
```
```
$PLOTSIZE=SIZE Yazın(Örnek 100G,200G)
```
> Örneğin 400G SDD aldınız 110G'sini bırakıyoruz. 290G subspace veriyoruz. Oraya gireceğiniz örnek olarak: 290G,300G gibi 

 ```
sudo tee <<EOF >/dev/null /etc/systemd/system/farmerd.service
[Unit]
Description=Subspace Farmer

[Service]
User=$USER
ExecStart=subspace-farmer farm --reward-address $ADDRESS path=/root/subspacefarmer,size=$PLOTSIZE
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
journalctl -u subspaced -f -o cat
```  

## Farmer loglarımıza bakıyoruz.
```
journalctl -u farmerd -f -o cat
```  
> Bu adımları yaptıktan sonra alta explorer linki var oradan kendinizi bulabilirsiniz.

![Ekran görüntüsü 2024-02-15 135945](https://github.com/CoinHuntersTR/Subspace-Gemini-3h/assets/111747226/abd5edaa-bacf-4484-8fb7-92d99b1615f7)

 ## Subspace Network Linkler;
  
### [Discord](https://discord.gg/subspace-network)
### [Twitter](https://twitter.com/NetworkSubspace)
### [Web](https://subspace.network/)
### [Subspace Explorer](https://telemetry.subspace.network/#list/0x0c121c75f4ef450f40619e1fca9d1e8e7fbabc42c895bc4790801e85d5a91c34)
 
 
