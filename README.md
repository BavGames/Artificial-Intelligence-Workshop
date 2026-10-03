# BavGames Atölye

**Türkçe kodlama asistanı | Sürüm 1.1.0 | Windows x64**

Atölye, **BavGames tarafından geliştirilen** bir masaüstü kodlama asistanıdır. Proje klasörünü açabilir, dosyaların nasıl çalıştığını sorabilir, hata incelemesi yaptırabilir ve yeni özellikler için değişiklik önerileri alabilirsin. Dosya değişiklikleri, sen inceleyip onayladıktan sonra uygulanır.

Uygulama, seçtiğin OpenAI uyumlu API sağlayıcısına bağlanır. Noxery bu kılavuzda örnek olarak kullanılır; başka uyumlu sağlayıcıların veya yerel servislerin adresini de girebilirsin. Yapay zeka yanıtını seçilen model üretir.

```text
<---- 01: UYGULAMANIN ANA EKRAN RESMİ EKLENECEK ---->
```

**Görselde:** Sol üstte BavGames yazısı, sohbet alanı, Klasör aç ve Bağlantı ve ayarlar düğmeleri görünsün. Dosya adı: `gorseller/01-ana-ekran.png`.

## 1. Ne işe yarar?

- Projenin dosya yapısını ve kodların görevini açıklamak.
- Kodda olası sorunları bulmak ve düzeltme önermek.
- Yeni özellikler için dosya düzenlemeleri hazırlamak.
- Önerilen değişiklikleri satır satır inceleyip onaylamak veya reddetmek.
- Uygulanmış bir değişikliği uygun olduğunda geri almak.
- Resim, metin, kod dosyası ve ZIP ekleyerek bunlar hakkında konuşmak.
- Sohbetleri yerel olarak saklamak, silmek ve mesaj metinlerini dışa aktarmak.

Bu sürüm terminal komutu çalıştırmaz; projeyi kendiliğinden derlemez veya test etmez. Düzenlemelerden sonra projenin kendi geliştirme ortamında kontrol yapmalısın. Modelin bir dosyayı düzenleyebilmesi için araç çağrısı desteği, resimleri anlayabilmesi için görsel desteği gerekir.

## 2. Kurulum ve ilk açılış

Gerekenler: Windows x64 bilgisayar, paketin tamamını açabileceğin bir klasör ve uyumlu bir API bağlantısı. Bulut sağlayıcılarında internet ve sağlayıcının istediği hesap/API anahtarı gerekir. Yerel servis kullanacaksan o servisin ayrıca çalışıyor olması gerekir.

1. `BavGames-Atolye-1.1.0-Windows-x64.zip` dosyasını indir.
2. ZIP dosyasına sağ tıkla ve **Tümünü ayıkla** seçeneğini kullan.
3. Açılan `BavGames-Atolye-1.1.0` klasörüne gir.
4. **Atolye.exe** dosyasını çalıştır.

Atolye.exe dosyasını yanındaki `resources`, `locales` ve diğer dosyalardan ayırma. Masaüstüne erişim için exe dosyasını taşımak yerine kısayol oluşturabilirsin. Paketli uygulama için Node.js veya VS Code kurulumu gerekmez.

```text
<---- 02: ZIP'TEN ÇIKARILMIŞ UYGULAMA KLASÖRÜ RESMİ EKLENECEK ---->
```

**Görselde:** Windows Dosya Gezgini içinde Atolye.exe, resources ve locales birlikte görünsün. Dosya adı: `gorseller/02-kurulum-klasoru.png`.

## 3. API bağlantısı nasıl kurulur?

Sol alttaki **Bağlantı ve ayarlar** düğmesine bas. Açılan **Çalışma arkadaşını seç.** penceresindeki alanları doldur:

| Alan veya düğme | Ne işe yarar? |
| --- | --- |
| API adresi | Sağlayıcının temel API adresidir. Örnek biçim: `https://sunucu.com/v1`. Adresin sonuna `/chat/completions` veya `/models` ekleme. |
| API anahtarı | Sağlayıcının hesabın için oluşturduğu erişim anahtarıdır. Anahtar istemeyen yerel servislerde boş bırakılabilir. |
| Model kimliği | Kullanılacak modelin tam kimliğidir. Sağlayıcının verdiği yazımı kullan. |
| Kaydet ve modelleri getir | Bağlantı bilgilerini kaydeder ve sağlayıcının model listesini getirir. |
| Yanıt uzunluğu sınırı | Yanıt için istenecek en fazla token sayısıdır. Token, modelin metni işlediği küçük birimdir; kelime sayısıyla aynı değildir. Varsayılan 8192'dir. Sağlayıcının daha düşük sınırı olabilir. |
| Ayarları kaydet | Adres, model ve yanıt sınırını saklar. Tek başına başarılı bağlantı testi anlamına gelmez. |
| Anahtarı kaldır | Seçili API adresi için kayıtlı anahtarı kaldırır. |

API anahtarı kayıtlıysa alan maskeli görünür. Aynı adreste yeni anahtar yazmadan kaydettiğinde mevcut anahtar korunur. Ayarları yeniden açtığında adres, model ve yanıt sınırı görünmeye devam eder.

Her temel API adresinin anahtarı ayrı saklanır. Adresi değiştirdiğinde önceki adresin anahtarı yeni adrese otomatik gönderilmez. Yeni bağlantı için gerekiyorsa anahtarı tekrar gir.

Model listesi alınamayan ancak sohbet bağlantısı çalışan bir sağlayıcıda model kimliğini elle yazabilirsin. API'nin `/chat/completions` biçimiyle uyumlu olması gerekir; sadece herhangi bir internet adresi yazmak yeterli değildir.

## 4. Noxery ile örnek bağlantı

Noxery örnek bir API sağlayıcısıdır. Atölye paketi Noxery hesabı, abonelik, API anahtarı veya kullanım kredisi içermez. Erişim ve ücretlendirme sağlayıcının koşullarına bağlıdır.

### A. Hesaba gir ve API anahtarı oluştur

1. [Noxery sitesini](https://noxery.net/tr) aç ve kendi hesabına giriş yap.
2. Hesap panelindeki **API Keys / API anahtarları** bölümünü aç.
3. Yeni bir anahtar oluştur ve Atölye'deki API anahtarı alanına yapıştır. Anahtarın oluşturulurken gösterildiği ekranda kopyalanması gerekir. Sağlayıcının [kimlik doğrulama belgesini](https://noxery.net/tr/docs/api/authentication) kontrol edebilirsin.

```text
<---- 03: NOXERY API ANAHTARLARI SAYFASI RESMİ EKLENECEK ---->
```

**Görselde:** API anahtarlarının bulunduğu bölüm ve yeni anahtar oluşturma düğmesi görünsün. Gerçek anahtarın tamamını ve hesap bilgilerini kapat. Dosya adı: `gorseller/03-noxery-api-anahtari.png`.

### B. Model kimliğini bul

[Noxery model sayfasından](https://noxery.net/tr/models) hesabında kullanmak istediğin modeli incele. Atölye'de **Kaydet ve modelleri getir** düğmesiyle alınan listedeki kimliği kullan. Örneğin `gpt-6-astra`, hesabının listesinde varsa seçilebilir; listede yoksa erişebildiğin başka bir modeli seç.

Modelin resim desteği ve kullanılabilirliği modele göre değişir. Sağlayıcının [model listesi belgesi](https://noxery.net/tr/docs/api/models) bu konuda referanstır.

```text
<---- 04: NOXERY MODEL SAYFASI RESMİ EKLENECEK ---->
```

**Görselde:** Modelin adı ve tam model kimliği okunabilsin. Görsellerle kullanımı anlatıyorsan görsel desteği olan bir modeli göster. Dosya adı: `gorseller/04-noxery-model.png`.

### C. Atölye ayarlarını doldur

| Alan | Örnek değer |
| --- | --- |
| API adresi | `https://noxery.net/v1` |
| API anahtarı | Kendi hesabında oluşturduğun anahtar |
| Model kimliği | `gpt-6-astra`, yalnızca hesabının listesinde varsa |
| Yanıt uzunluğu sınırı | `8192`, seçilen modelin sınırına uygun olarak |

**Adres notu:** Noxery'nin resmi belgesinde temel adres `https://api.noxery.net/v1` olarak belirtilir. Bu sürüm hazırlanırken, 3 Ekim 2026 tarihinde model listesi bağlantısı `https://noxery.net/v1` üzerinden doğrulandı. Yukarıdaki örnek bu adresi kullanır. Sağlayıcının adresleri değişirse güncel belgesini kontrol et. Model listesinin gelmesi, her modelin sohbet veya görsel desteğinin ayrıca test edildiği anlamına gelmez.

**Kaydet ve modelleri getir** düğmesine bas, istediğin modeli seç ve **Ayarları kaydet** ile tamamla. İlk deneme için “Merhaba, Türkçe yanıt ver.” mesajını gönder.

```text
<---- 05: UYGULAMADAN BAĞLANTI VE AYARLAR RESMİ EKLENECEK ---->
```

**Görselde:** Çalışma arkadaşını seç. başlığı, API adresi, maskelenmiş anahtar, model kimliği, yanıt sınırı ve başarılı model listesi durumu görünsün. Dosya adı: `gorseller/05-atolye-ayarlar.png`.

## 5. Proje açma ve ilk görev

1. Sağ üstte **Klasör aç** düğmesine bas.
2. İncelemek istediğin projenin ana klasörünü seç.
3. Sağdaki Proje bölümünde dosyaları gör. **Dosya ara...** alanıyla listeyi filtreleyebilirsin.
4. Bir dosyaya tıklayarak önizlemesini açabilir, **Bu dosya hakkında sor** düğmesini kullanabilirsin.
5. Mesaj alanına görevini yaz ve **Gönder** düğmesine bas.

İlk inceleme için örnek:

```text
Bu projenin dosya yapısını incele. Nasıl çalıştığını ve önemli dosyaların
görevlerini açıkla. Henüz dosya değiştirme.
```

Hata incelemesi için örnek:

```text
Ayarları kaydettikten sonra pencereyi tekrar açınca model seçimi boş görünüyor.
İlgili dosyaları incele, sorunun nedenini açıkla ve bir düzeltme önerisi hazırla.
```

```text
<---- 06: PROJE KLASÖRÜ AÇILMIŞ SOHBET EKRANI RESMİ EKLENECEK ---->
```

**Görselde:** Örnek proje adı, sağdaki dosya listesi ve örnek bir inceleme mesajı görünsün. Paylaşılabilir bir örnek proje kullan. Dosya adı: `gorseller/06-proje-inceleme.png`.

## 6. Değişiklikleri onaylama ve geri alma

Model bir dosya değişikliği önerdiğinde **Değişiklikler** bölümünden öneriyi aç. Kırmızı satırlar kaldırılan, yeşil satırlar eklenen içeriktir. Öneride birden fazla dosya varsa her birini incele.

- **Onayla ve uygula:** Öneriyi proje dosyalarına yazar.
- **Reddet:** Öneriyi uygulamaz.
- **Değişikliği geri al:** Uygulanan öneriyi yerel yedeği kullanarak geri alır.

Öneri beklerken dosyayı başka bir editörde değiştirdiysen Atölye eski öneriyi dosyanın üzerine yazmaz. Dosyanın yeniden okunmasını ve önerinin yenilenmesini iste. Geri alma sonrasında da başka düzenlemelerin kaybolmaması için dosyanın güncel durumu kontrol edilir.

```text
<---- 07: DEĞİŞİKLİK İNCELEME VE ONAY EKRANI RESMİ EKLENECEK ---->
```

**Görselde:** Dosya adı, kırmızı/yeşil satırlar, Reddet ve Onayla ve uygula düğmeleri görünsün. Dosya adı: `gorseller/07-degisiklik-onayi.png`.

## 7. Resim, dosya ve ZIP ekleme

Mesaj alanındaki **Dosya ekle** düğmesini kullanabilir, dosyaları pencereye sürükleyip bırakabilir veya bir resmi mesaj alanına **Ctrl+V** ile yapıştırabilirsin.

Göndermeden önce ekin kartına tıklayarak önizlemeyi aç. Yanlış dosya eklediysen **Kaldır** düğmesiyle çıkar. Ardından ne yapılmasını istediğini yaz ve gönder.

```text
Bu ekran görüntüsündeki hatayı incele. Eklediğim kaynak dosyada buna neden
olabilecek bölümü bul ve düzeltme önerini açıkla.
```

```text
<---- 08: MESAJ ALANINA RESİM VE DOSYA EKLENMİŞ HALİNİN RESMİ EKLENECEK ---->
```

**Görselde:** Dosya ekle düğmesi, bir resim kartı, bir kod dosyası ve bir ZIP kartı görünsün. Dosya adı: `gorseller/08-dosya-ekleme.png`.

| İçerik | Destek ve sınırlar |
| --- | --- |
| Resim | PNG, JPG/JPEG, WebP, GIF ve BMP. GIF'in ilk karesi kullanılır. En fazla 10 MB ve 40 megapiksel. Gönderim için uzun kenar en fazla 1600 piksele indirilir. |
| Metin/kod | UTF-8 veya UTF-16 metin dosyaları; örneğin TXT, MD, JSON, CSV, CPP, H ve CS. Tek dosya en fazla 2 MB. |
| ZIP | İçindeki metin/kod dosyaları okunur. Arşiv en fazla 25 MB; bildirilen toplam açılmış boyut en fazla 100 MB. En fazla 2000 kayıt içinden 200 metin dosyası okunur. |
| Desteklenmeyen belgeler | PDF ve Office belgeleri bu sürümde çözümlenmez. Uygulama dosyaları ve diğer ikili dosyalar kod metni olarak okunmaz. |

Bir mesajda en fazla **8 ek** bulunabilir. Bir metin veya ZIP içeriği yaklaşık **120.000 karakter** ile sınırlıdır. Kısaltılan veya atlanan içerik önizlemede belirtilir.

ZIP dosyası proje klasörüne açılmaz. İçeriği konuşma için referans olarak okunur; eklediğin kaynak dosyalar kendiliğinden projenin parçası olmaz. Şifreli ZIP girdileri, ikili dosyalar, bazı gizli dosyalar ve üretilmiş klasörler atlanır. Proje düzenlemek için ayrıca **Klasör aç** kullan.

```text
<---- 09: ZIP DOSYASI İÇERİK ÖNİZLEMESİ RESMİ EKLENECEK ---->
```

**Görselde:** ZIP adı, okunabilen dosyalar ve varsa atlanan/kısaltılan içerik açıklaması görünsün. Dosya adı: `gorseller/09-zip-onizleme.png`.

## 8. Sohbetler ve kısayollar

Sol paneldeki **Yeni sohbet** ile yeni konuşma başlat. Önceki bir konuşmaya dönmek için adına tıkla. **Sohbeti dışa aktar** mesaj metinlerini dosyaya kaydeder; eklerin orijinal dosyalarını dışa aktarmaz.

Sohbetin yanındaki **Sil** düğmesi bir onay penceresi açar. **Sohbeti sil** mesajları, gönderilen ekleri ve sohbetin değişiklik geçmişini siler. Projeye uygulanmış düzenlemeler ve yerel dosya yedekleri korunur. İşlem devam ediyorsa önce **Durdur** düğmesine bas.

```text
<---- 10: SOHBET SİLME ONAY PENCERESİ RESMİ EKLENECEK ---->
```

**Görselde:** Sohbet silinsin mi? başlığı, açıklama, Vazgeç ve Sohbeti sil düğmeleri görünsün. Dosya adı: `gorseller/10-sohbet-silme.png`.

| Kısayol | İşlem |
| --- | --- |
| Enter | Mesajı gönderir. |
| Shift+Enter | Mesajda yeni satır açar. |
| Ctrl+N | İşlem sürmüyorsa ve bir ayar/onay penceresi açık değilse yeni sohbet açar. |
| Ctrl+V | Mesaj alanında panodaki resmi ekler; metinse metni yapıştırır. |
| Escape | Açık iletişim penceresini kapatır; sohbet silme onayından vazgeçer. |

## 9. Veriler nerede tutulur?

Uygulamanın yerel verileri **`%APPDATA%\Atolye`** klasöründe saklanır. Windows'ta Win+R tuşlarına basıp bu yolu yazarak klasörü açabilirsin. Sohbetler, gönderilmiş eklerin işlenmiş içerikleri, ayarlar ve yerel değişiklik yedekleri burada tutulur. API anahtarları Windows hesabıyla şifrelenerek saklanır.

Ekler ve modelin okuduğu proje metinleri yanıt oluşturulması için seçtiğin API sağlayıcısına gönderilir. Hangi sağlayıcıya bağlandığını ve hangi içeriği gönderdiğini kontrol et. ZIP paketi kendi API anahtarını veya sohbetlerini içermez; her kullanıcı kendi bağlantısını ayarlar.

Yeni sürüme geçerken yeni uygulama paketini ayrı bir klasöre açabilirsin. Aynı Windows hesabındaki yerel veriler uygulama klasörünün dışında olduğundan korunur. Sohbet silmek, proje dosyalarındaki değişiklikleri geri almaz.

## 10. Sık karşılaşılan sorunlar

| Durum | Yapılacak kontrol |
| --- | --- |
| Bağlantı doğrulanamadı / fetch failed | API adresini ve internet bağlantısını kontrol et. Yanlış alan adı, sunucu kesintisi veya ağ erişimi sorunu olabilir; bu mesaj tek başına anahtarın bozuk olduğunu göstermez. |
| API 20 saniye içinde yanıt vermedi | Model listesi isteği zaman aşımına uğradı. Sağlayıcının güncel adresini ve hizmet durumunu kontrol et. |
| 401 | API anahtarının eksik, yanlış veya iptal edilmiş olup olmadığını kontrol et. |
| 402 | Sağlayıcındaki kullanım hakkını veya hesap planını kontrol et. |
| 403 | Hesabının seçilen modele erişimi olup olmadığını kontrol et. |
| 404 | Temel API adresini ve model kimliğini kontrol et. Adrese ayrıca `/models` veya `/chat/completions` ekleme. |
| 429 | Sağlayıcının istek veya kullanım sınırına ulaşılmış olabilir. Bir süre bekle ve hesabındaki sınırları kontrol et. |
| Resim içeren mesaj reddediliyor | Seçilen modelin ve sağlayıcının görsel giriş desteğini kontrol et. |
| Model cevap veriyor ama dosya düzenleyemiyor | Proje klasörünün açık olduğunu ve modelin araç çağrılarını desteklediğini kontrol et. |
| Dosya listede görünmüyor | Bazı gizli, üretilmiş veya ikili dosyalar atlanır. Proje okuma/düzenleme sınırı dosya başına 256 KB'tır. |
| ZIP veya ek çok büyük | Gereksiz dosyaları çıkar, yalnız gerekli kaynakları ekle veya içeriği daha küçük parçalara ayır. |
| Bağlam sınırına ulaşıldı | Yeni sohbet aç ve yalnız gerekli dosyalarla görevin kısa özetini ekle. |
| Uygulama açılmıyor veya dosya eksik diyor | ZIP'in tamamını yeniden ayıkla. Atolye.exe'nin yanındaki dosyaların korunduğundan emin ol. |

Bir değişiklik önerisi en fazla **12 dosya**, bir görev turu en fazla **20 model çağrısı** içerir. Bu sınırları aşan işleri küçük adımlara böl.

## 11. Bu README'ye görseller nasıl eklenecek?

Bu bölüm, kılavuzu dağıtım için hazırlayan kişiye yöneliktir. Yukarıdaki ok işaretli alanlar **yer tutucudur**; ekran görüntüleri henüz eklenmemiştir.

1. Ekran görüntüsünü ilgili bölümde anlatıldığı şekilde al.
2. Görseli bu README ile aynı klasördeki **gorseller** klasörüne, belirtilen dosya adıyla kaydet.
3. İlgili `<---- ... ---->` satırını ve onu çevreleyen üç ters tırnaklı bloğu kaldır.
4. Yerine aşağıdaki listeden uygun Markdown görsel satırını ekle.
5. Görselin altındaki hazırlama talimatını istersen sil. Diğer kullanım açıklamaları kalabilir.
6. README.md ile gorseller klasörünü birlikte tut ve uygulama klasörünün tamamını yeniden ZIP yap.

```markdown
![BavGames Atölye ana ekranı](gorseller/01-ana-ekran.png)
![ZIP'ten çıkarılmış uygulama klasörü](gorseller/02-kurulum-klasoru.png)
![Noxery API anahtarları](gorseller/03-noxery-api-anahtari.png)
![Noxery model bilgisi](gorseller/04-noxery-model.png)
![Atölye bağlantı ayarları](gorseller/05-atolye-ayarlar.png)
![Proje inceleme](gorseller/06-proje-inceleme.png)
![Değişiklik onayı](gorseller/07-degisiklik-onayi.png)
![Sohbete dosya ekleme](gorseller/08-dosya-ekleme.png)
![ZIP önizlemesi](gorseller/09-zip-onizleme.png)
![Sohbet silme](gorseller/10-sohbet-silme.png)
```

Gerçek API anahtarını, kişisel hesap bilgilerini veya özel proje içeriğini görsellere koyma. Örnek proje ve maskelenmiş anahtar kullan. Görsellerde metinler okunacak büyüklükte olsun; ilgili pencereyi göstermek yeterlidir.

## 14. Paket içeriği ve paylaşma

```text
BavGames-Atolye-1.1.0/
  Atolye.exe
  README.md
  gorseller/
  resources/
  locales/
  LICENSE
  LICENSES.chromium.html
  ... uygulamanın diğer çalışma dosyaları
```

Dağıtırken klasörün tamamını paylaş. `LICENSE` ve `LICENSES.chromium.html` gibi birlikte gelen üçüncü taraf lisans dosyalarını koru. `%APPDATA%\Atolye` klasörünü, kendi API anahtarlarını veya kişisel sohbetlerini pakete ekleme.

**Geliştirici: BavGames**
