FuckAdBlock (v3.2.1)
===========

Kötü reklam engelleyicileri tespit edebilirsiniz.
Çevrimiçi örnek: http://sitexw.fr/fuckadblock/

(Ayrıca daha uygun bir ada sahip [BlockAdBlock](https://github.com/sitexw/BlockAdBlock) adlı bir proje var)

*Gelin ve FuckAdBlock'un geleceğini görün: [V4 Beta](https://github.com/sitexw/FuckAdBlock/tree/v4.x)*


Geçerli
---------------------
- Google Chrome
- Mozilla Firefox
- Internet Explorer (8+)
- Safari
- Opera

Şununla yükleyin:
---------------------
NPM:
```
npm fuckadblock'u yükle
```
çardak:
```
bower fuckadblock yükleyin
```
CDN :
```
https://cdnjs.cloudflare.com/ajax/libs/fuckadblock/3.2.1/fuckadblock.min.js
https://cdn.jsdelivr.net/npm/fuckadblock@3.2.1/fuckadblock.min.js
```
Bütünlük:
```
sha256-4/8cdZfUJoNm8DLRzuKwvhusQbdUqVov+6bVj9ewL7U= (fuckadblock.js)
sha256-xjwKUY/NgkPjZZBOtOxRYtK20GaqTwUCf7WYCJ1z69w= (fuckadblock.min.js)
```
Code example
---------------------
Ideally positioned at the end of `<body>`.
```javascript
// Function called if AdBlock is not detected
function adBlockNotDetected() {
	alert('AdBlock is not enabled');
}
// Function called if AdBlock is detected
function adBlockDetected() {
	alert('AdBlock is enabled');
}
// We look at whether FuckAdBlock already exists.
if(typeof fuckAdBlock !== 'undefined' || typeof FuckAdBlock !== 'undefined') {
	// If this is the case, it means that something tries to usurp are identity
	// So, considering that it is a detection
	adBlockDetected();
} else {
	// Otherwise, you import the script FuckAdBlock
	var importFAB = document.createElement('script');
	importFAB.onload = function() {
		// If all goes well, we configure FuckAdBlock
		fuckAdBlock.onDetected(adBlockDetected)
		fuckAdBlock.onNotDetected(adBlockNotDetected);
	};
	importFAB.onerror = function() {
		// If the script does not load (blocked, integrity error, ...)
		// Then a detection is triggered
		adBlockDetected(); 
	};
	importFAB.integrity = 'sha256-xjwKUY/NgkPjZZBOtOxRYtK20GaqTwUCf7WYCJ1z69w=';
	importFAB.crossOrigin = 'anonymous';
	importFAB.src = 'https://cdnjs.cloudflare.com/ajax/libs/fuckadblock/3.2.1/fuckadblock.min.js';
	document.head.appendChild(importFAB);
}
```
Varsayılan seçenekler
---------------------
```javascript
// Başlatma sırasında AdBlock'un etkin olup olmadığını kontrol edin
// fuckAdBlock.check() yöntemini kullanır
checkOnLoad: doğru
// Kontrolün sonunda, eklenen tüm olayları kaldırıyor mu?
resetOnEnd: doğru
// Her kontrol arasındaki milisaniye sayısı
döngüKontrol Süresi: 50
// AdBlock'un etkin olmadığı kabul edilen negatif kontrollerin sayısı
// Zaman (ms) = 50*(5-1) = 200ms (varsayılan olarak)
loopMaxSayı: 5
// AdBlock tarafından yakalanan yem tarafından kullanılan CSS sınıfı
baitClass: 'pub_300x250 pub_300x250m pub_728x90 metin-reklam metniAd text_ad text_ads metin-reklamlar metin-reklam-bağlantıları'
// Kullanıcıların yemlerini gizlemek için kullanılan CSS stili
baitStyle: 'genişlik: 1 piksel !important; yükseklik: 1 piksel !önemli; konum: mutlak !önemli; sol: -10000 piksel !önemli; üst: -1000 piksel !önemli;'
// Hata ayıklamayı konsolda görüntüler (yalnızca 3.2 ve daha fazla sürümden itibaren kullanılabilir)
hata ayıklama: yanlış
```

Mevcut yöntem
---------------------
```javascript
// Seçeneklerin ayarlanmasına izin verir
// #seçenekler: dize|nesne
// #değer: dize
fuckAdBlock.setOption(seçenekler, değer);
// AdBlock'un etkin olup olmadığını manuel olarak kontrol edin.
// Kontrol tamamlandıktan sonra 'true' değerini döndürür.
// Kontrol yapılamazsa (örneğin devam eden başka bir kontrol nedeniyle) 'false' döndürür.
// 'loop' parametresi, 'loopMaxNumber' değerine göre birkaç kez döngü olmadan kontrole izin verir
// Örnek: loop=true => time~=200ms (süre konfigürasyona göre değişir)
// döngü=yanlış => süre~=1ms
// #loop: boolean (varsayılan: true)
fuckAdBlock.check(döngü);
// AdBlock'un varlığının manuel olarak simüle edilmesine izin verir veya vermez
// #detected: boolean (AdBlock algılandı mı?)
fuckAdBlock.emitEvent(algılandı);
// 'on', 'onDetected' ve 'onNotDetected' yöntemleriyle eklenen tüm olayları temizlemeye izin verir
fuckAdBlock.clearEvent();
// AdBlock algılanırsa olay eklenmesine izin verir
// #detected: boolean (doğru: algılandı, yanlış: algılanmadı)
// #fn: işlev
fuckAdBlock.on(tespit edildi, fn);
// fuckAdBlock.on'a benzer(true|false, fn)
fuckAdBlock.onDetected(fn);
fuckAdBlock.onNotDetected(fn);
```

Misal
---------------------
*(Yalnızca 3.1 ve üzeri sürümlerde mevcuttur)*
Varsayılan olarak, FuckAdBlock otomatik olarak başlatılır.
Bu otomatik başlatmayı engellemek için, betiği içe aktarmadan önce bir değerle (boş, yanlış, ...) bir "fuckAdBlock" değişkeni oluşturmanız yeterlidir.
```html
<script>var fuckAdBlock = false;</script>
<script src="./fuckadblock.js"></script>
```
Bundan sonra, kendi örneklerinizi oluşturmakta özgürsünüz:
```javascript
fuckAdBlock = yeni FuckAdBlock;
// ve|veya
myFuckAdBlock = yeni FuckAdBlock({
checkOnLoad: doğru,
resetOnEnd: doğru
});
```
