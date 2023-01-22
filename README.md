<h1 align="center"> Sarcophagus </h1>

![image](https://user-images.githubusercontent.com/101149671/213923450-405963b2-8358-4a46-ae5f-3f34eda56d52.png)

<h1 align="center"> Bu rehberde Sarcophagus'un node'unu kuracağız. Belki bir çoğunuzun alışık olmadığı bir şekilde olacak bu node, okunması gereken notlarım ile başlayalım:</h1>

* Acele etmemenizi, okuyarak ve anlayarak yapmanızı şiddetsiz bir şekilde tavsiye ediyorum.
* Bir blockchain değil, Arweave üzerinde geliştirilen bir proje.
* Sarcophagus aynı zamanda bir DAO ile yönetiliyor, ödüllü testnet için oylama başlatıldı. ve DAO tarafından kabul edildi.
* İlginizi çeker mi bilmiyorum ama, bir diğer güzel haber bu linkte: [Link 1](https://coinmarketcap.com/currencies/sarcophagus/) - [Link 2](https://www.coingecko.com/en/coins/sarcophagus#markets)
* Token alırken [discorddan](https://discord.gg/Eyd5HYzj) almalıyız (rehberin devamında tokenin kullanım alanını göstereceğim)
* Sohbet için telegram kanalı
* Aklıma geldikçe buraya daha fazla not eklerim.

![image](https://user-images.githubusercontent.com/101149671/213924896-1f09ce56-1057-4cf0-b030-6cda23835e8e.png)

## Donanım ve Gereksinimler:
```
10 GB SSD
1 GB RAM
```

* Goerli veya Sepolia'dan test ETH.
* Bir RPC URL (Nasıl alacağınızı bilmiyorsanız ben size vereceğim)
* Bir A kaydı olan domain.

### Domain Hakkında Notlar:

* Biliyorum, herkesin bir domain'i yok, bunu nasıl çözeceğinizi bilmiyorum.
* Ben kendi domainimi severime bağladım, sizde öyle yapmalısınız.

![image](https://user-images.githubusercontent.com/101149671/213924185-9e320b9d-a2ea-46b9-835b-ba70f6d5aa69.png)

* Domaini A kaydı yaptıktan sonra şu şekilde gözükecektir, örnektir: `ns1.ziesha.network`

* Domaininiz varsa size rehber olacak kaynaklar: [Godaddy](https://tr.godaddy.com/help/a-kaydi-ekleme-19238) - [Namecheap](https://www.namecheap.com/support/knowledgebase/article.aspx/319/2237/how-can-i-set-up-an-a-address-record-for-my-domain/) - [Name.com](https://www.name.com/support/articles/115004893508-adding-an-a-record)

* Şu an müsaitlik durumum yok, yoksa nasıl domain alınır nasıl bağlanılır tek tek anlatırdım, ama bana gerek yok size kaynak bıraktım ve youtube kaynak dolu.

* Biraz bakındım, ücretsiz domainlerde alabilirsiniz (işe yaramayan domainler genellikle ücretsiz oluyor, bu da işiniz görür), örneğin:

![image](https://user-images.githubusercontent.com/101149671/213924481-f7782c3f-44af-482c-83cc-2abd0fbdefc9.png)

> Test etmedim ama ücretsiz domain veren siteler: [Link 1](https://www.hostinger.web.tr/ucretsiz-domain) - [Link 2](https://tr.wix.com/domain/names) 

> HER NE KADAR DOMAİNİ ÜCRETSİZ BULSAKTA HOSTİNG ÜCRETLİ (2$-40$). Bunu sohbet grubunda tartışalım.

## Bunları okuduysanız ve çözdüyseniz node'umuzu kuralım:
```
sudo su
```
```
sudo apt update 
```
```
sudo apt upgrade
```
```
sudo apt install git
```
```
sudo apt-get update && sudo apt install jq && sudo apt install apt-transport-https ca-certificates curl software-properties-common -y && curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add - && sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu focal stable" && sudo apt-get install docker-ce docker-ce-cli containerd.io docker-compose-plugin && sudo apt-get install docker-compose-plugin
```

## Repoyu klonlayalım ve gerekli işlemlere başlayalım:
```
git clone https://github.com/sarcophagus-org/quickstart-archaeologist
```
```
cd quickstart-archaeologist
```
## Bu komutu çalıştırdıktan sonra bir 12 kelime oluşturalım:

> Altta ki komut offline seed generate isterseniz [buradan](https://iancoleman.io/bip39/) ethereum seçipte bir seed oluşturabilirsiniz.

> Konu açılmışken, yukarıda kendinize özel cüzdanlar oluşturabilirsiniz, güven ve risk konusu size kalmış :)

```
COMPOSE_PROFILES=seed docker compose run seed-gen
```

> Yukarıdaki `seed-gen` komutunu girdikten sonra 12 kelimenizi not edip saklayın.

> Daha sonra altta ki bu iki komutu girip nano ile `.env`'in içine girelim.

```
cp .env.example .env
```
```
nano .env
```

## Yukarıda `.env`'in içine girdiğinizde yapmanı gerekenler:

> `ETH_PRIVATE_KEY` için kısmı tıpkı [taiko](https://github.com/ruesandora/taiko-node#yukar%C4%B1daki-komutlar%C4%B1-girince-a%C3%A7%C4%B1lacak-ekran-g%C3%B6rselde-ki-gibi) 'da yaptığımız gibi metamask'ın private key'ini alıyoruz. (özel anahtar = private key)

* Private keyi aldıktan sonra `ETH_PRIVATE_KEY=` 'in yanına bunu giriyoruz

> `ENCRYPTION_MNEMONIC=` kısmı, yukarıda aldığımız seed/12 kelimeyi giriyoruz.

> `DOMAIN=` kısmı yukarıda anlattığım gibi `ns1.ziesha.network` gibi olacak ve ekleyeceksiniz. (bunu boşuna denemeyin, olmayacak)

> `PROVIDER_URL=` için bir RPC URL'ye ihtiyacınız var, ben aşağıya sıralıyorum (not ben ANKR RPC kullandım):

> https://rpc.ankr.com/eth_goerli -- https://rpc.ankr.com/eth_sepolia -- https://sepolia.infura.io/v3/3f110b00aeb24807b3ac5a9a4536079c --https://goerli.infura.io/v3/3f110b00aeb24807b3ac5a9a4536079c

* Bunlar dışında kendi node'unuz varsa veya Alchemy'den bağlanabilirsiniz.

> Hepsini doldurduktan sonra `CTRL + X + Y + ENTER` yapıyoruz.

