# Cosmos Projelerinde Kullanılan Genel Kodlar

- **Cosmos tabanlı projelerin node testnetlerinde node kurarken, validatör oluştururken yada diğer işlemler için kullanılan kodlar aynıdır.**
- **Kodlarda değişen yerler, proje ismi ve projenin tokenidir.**

- **Buna aşağıdaki görselden bakalım. Kodlarda sadece proje ismi değişmektedir. Nadir olarak bazı projelerde örnek olarak Dymension projesinde 
kullanılan kodlarda dymensiond yerine dymd kullanılır. 
Tokenlerde ise daha fazla değişkenlikler gösterebilir. Kyve da iki tane olmasının nedeni biri kaon ağında diğeri mainnet ağında kullanılan token adlarıdır.**

![alt text](https://i.hizliresim.com/s5gmzio.png)

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
kujira# f2f2f2d keys list
```
