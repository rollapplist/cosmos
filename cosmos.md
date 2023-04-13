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

