# Cosmos Projelerinde Kullanılan Genel Kodlar

- **Cosmos tabanlı projelerin node testnetlerinde node kurarken, validatör oluştururken yada diğer işlemler için kullanılan kodlar aynıdır.**
- **Kodlarda değişen yerler, proje ismi ve projenin tokenidir.**

- **Buna aşağıdaki görselden bakalım. Kodlarda sadece proje ismi değişmektedir. Nadir olarak bazı projelerde örnek olarak Dymension projesinde 
kullanılan kodlarda dymensiond yerine dymd kullanılır. 
Tokenlerde ise daha fazla değişkenlikler gösterebilir. Kyve da iki tane olmasının nedeni biri kaon ağında diğeri mainnet ağında kullanılan token adlarıdır.**

![alt text](https://i.hizliresim.com/hz9px1d.png)

# Yukarıdaki bilgilere göre genel kullanılan kodlar;
## (kodlar kujira projesi üzerinden yazılmıştır)

- **Cüzdan isminizi değiştirmek isterseniz wallet olan yerleri kendi cüzdan isminiz ile değiştirebilirsiniz.**

Yeni Cüzdan 

```
kujirad keys add wallet
```

Kullanmak istediğiniz cüzdan (cüzdan mnemoniclerinizi import etmek için)

```
kujirad keys add wallet --recover
```
Cüzdanları isimleri ve adresleri ile listeleme

```
kujirad keys list
```

Validatör Oluşturma

```
kujirad tx staking create-validator \
--amount=1000000ukuji \
--pubkey=$(kujirad tendermint show-validator) \
--moniker="Monikeradınız" \
--identity=id \
--details="detaylar" \
--chain-id=kaiyo-1 \
--commission-rate=0.10 \
--commission-max-rate=0.20 \
--commission-max-change-rate=0.01 \
--min-self-delegation=1 \
--from=wallet \
--gas-prices=0.1ukuji \
--gas-adjustment=1.5 \
--gas=auto \
-y
```
Validatör oluşturma kodunda değiştirecek olduğunuz yerler; kujirad, 1000000 (token adedi), ukuji , monikeradınız, id, detaylar, ve eğer değiştirmişseniz cüzdan isminiz (wallet)


- **--amount= delege etmek istediğiniz token miktarı**
- **moniker="Monikeradınız" = Validatör isminiz (monikeradınız yerine yazılacak)**
- **--identity=id https://keybase.io/ sitesine kayıt olup profil resmi yükledikten sonra profilinizde gözüken id numarasını id yerine boşluksuz şekilde yazarsanız explorer üzerinde validatörünüzün resmi gözükür.**

![alt text](https://i.hizliresim.com/ss2q435.png)

- **--details= Validatörünüz hakkındaki bilgiler. (detaylar yerine yazılacak)**
- **--chain-id= projenin ağ ismi**
- **--commission-rate= validatörünüze stake edilen tokenlerden alacak olduğunuz komisyon oranı (0.10=%10)**
- **--commission-max-rate= maximum yapabileceğiniz komisyon oranı**
- **--commission-max-change-rate= komisyon düzeltmede yapabileceğiniz max komisyon değiştirme oranı**
- **--min-self-delegation= kendinize delege edeceğiniz minimum token miktarı**
- **--from= cüzdan isminiz**
- **--gas-prices= gas fiyatı (projeden projeye değişebilir)**
- **--gas-adjustment= gas ayarı**


Oluşturmuş olduğunuz validatörde moniker, id, komisyon vb. değişikliği yapma

```
kujirad tx staking edit-validator \
--new-moniker="Monikeradınız" \
--identity=id \
--details="detaylar" \
--chain-id=kaiyo-1 \
--commission-rate=0.1 \
--from=wallet \
--gas-prices=0.1ukuji \
--gas-adjustment=1.5 \
--gas=auto \
-y
```

Jailed durumundan kurtulmak için

```
kujirad tx slashing unjail --from wallet --chain-id kaiyo-1 --gas-prices 0.1ukuji --gas-adjustment 1.5 --gas auto -y
```

Validatörünüz bilgilerini görme

```
kujirad q staking validator $(kujirad keys show wallet --bech val -a)
```

Validatörünüzde biriken ödülleri çekme

```
kujirad tx distribution withdraw-all-rewards --from wallet --chain-id kaiyo-1 --gas-prices 0.1ukuji --gas-adjustment 1.5 --gas auto -y
```

Validatörünüzde biriken ödül ve komisyonları çekme

```
kujirad tx distribution withdraw-rewards $(kujirad keys show wallet --bech val -a) --commission --from wallet --chain-id kaiyo-1 --gas-prices 0.1ukuji --gas-adjustment 1.5 --gas auto -y
```
Kendi Validatörünüze token delege etme

```
kujirad tx staking delegate $(kujirad keys show wallet --bech val -a) 1000000ukuji --from wallet --chain-id kaiyo-1 --gas-prices 0.1ukuji --gas-adjustment 1.5 --gas auto -y
```

Başka Validatöre token delege etme

```
kujirad tx staking delegate valoperadresi 1000000ukuji --from wallet --chain-id kaiyo-1 --gas-prices 0.1ukuji --gas-adjustment 1.5 --gas auto -y
```
valoperadresi= explorer üzerinde ilgili validatörün profilinde bulunan adres

## Burada gördüklerimizi görsel üzerinden görmek istersek;

![alt text](https://i.hizliresim.com/lidocpk.png)

Redelegate: Stake ettiğiniz tokenleri başka validaötüre delege etme

```
kujirad tx staking redelegate $(kujirad keys show wallet --bech val -a) valoperadresi 1000000ukuji --from wallet --chain-id kaiyo-1 --gas-prices 0.1ukuji --gas-adjustment 1.5 --gas auto -y
```

Unbond: Stake ettiğiniz tokenleri unstake etme (testnet ve mainnet ağlarında unstake süresi genellikle 14-21gündür.)

```
kujirad tx staking unbond $(kujirad keys show wallet --bech val -a) 1000000ukuji --from wallet --chain-id kaiyo-1 --gas-prices 0.1ukuji --gas-adjustment 1.5 --gas auto -y 
```
Send: Token gönderme

```
kujirad tx bank send wallet cüzdanadresi 1000000ukuji --from wallet --chain-id kaiyo-1 --gas-prices 0.1ukuji --gas-adjustment 1.5 --gas auto -y 
```

cüzdanadresi=gönderecek olduğunuz cüzdan adresi


Aktif olan proposal/oylamaları görme

```
kujirad query gov proposals
```

EVET oyu

```
kujirad tx gov vote 1 yes --from wallet --chain-id kaiyo-1 --gas-prices 0.1ukuji --gas-adjustment 1.5 --gas auto -y
```

HAYIR oyu

```
kujirad tx gov vote 1 no --from wallet --chain-id kaiyo-1 --gas-prices 0.1ukuji --gas-adjustment 1.5 --gas auto -y
```

ÇEKİMSER oyu

```
kujirad tx gov vote 1 abstain --from wallet --chain-id kaiyo-1 --gas-prices 0.1ukuji --gas-adjustment 1.5 --gas auto -y
```

## Indexer Güncelleme
Buradaki kodda kv=dizinleri tutar
null=dizinleri tutmaz. (sunucuda fazla yer kaplamaz)

```
sed -i 's|^indexer *=.*|indexer = "kv"|' $HOME/.kujira/config/config.toml
```

Koddaki kv yerini null yapabilirsiniz. .kujira klasörü başka projede örnek olarak Kyve'da .kyve'dır.


