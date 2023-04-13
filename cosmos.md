# Cosmos Projelerinde Kullanılan Genel Kodlar

- **Cosmos tabanlı projelerin node testnetlerinde node kurarken, validatör oluştururken yada diğer işlemler için kullanılan kodlar aynıdır.**
- **Kodlarda değişen yerler, proje ismi ve projenin tokenidir.**

- **Buna aşağıdaki görselden bakalım. Kodlarda sadece proje ismi değişmektedir. Nadir olarak bazı projelerde örnek olarak Dymension projesinde 
kullanılan kodlarda dymensiond yerine dymd kullanılır. 
Tokenlerde ise daha fazla değişkenlikler gösterebilir. Kyve da iki tane olmasının nedeni biri kaon ağında diğeri mainnet ağında kullanılan token adlarıdır.**

![alt text](https://i.hizliresim.com/a0w50bo.png)

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

Monikeradınız= Validatör isminiz
id= https://keybase.io/ sitesine kayıt olup profil resmi yükledikten sonra profilinizde gözüken id numarası. Bunu --identity=id'deki id yerine boşluksuz şekilde yazarsanız explorer üzerinde validatörünüzün resmi gözükür.

![alt text](https://i.hizliresim.com/g02u7hh.png)

