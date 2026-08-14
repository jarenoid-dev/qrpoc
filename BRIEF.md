# QRPOC · Claude Code Brief (v4.2)

**Kullanım:** Bu dosya `qrpoc` klasörünün kökünde `BRIEF.md` olarak durur. Claude Code'a "BRIEF.md'yi oku ve uygula" demek yeterlidir.

---

## Mevcut görev: SADECE ANALİZ

Bu session'da prototype kodu yazılmayacak, ekran build edilmeyecek. Görev: referansları derinlemesine çalışıp bir analiz dokümanı üretmek. Build fazları (Wave 1, 2, 3) aşağıda tanımlı ama **donduruldu**; analiz onaylanmadan hiçbir wave başlamaz.

Hedefin netliği: MenuTiger'a çok benzer bir app tasarlayacağız. Bu uygulamanın UI/UX'i çok iyi; biz farklı bir branding giydireceğiz, sonra kendi amaçlarımıza göre modifiye edeceğiz. Genel UI/UX kuralları ve genel his çok benzer olmalı: aynı temizlik, aynı ferahlık. **Ana hedef kitle işletmeciler; müşteri yüzeyi önemli ama ikincil.** Referansın merkezi canlı portalın kendisi, yani desktop/web app; marketing site ikincil. Bu yüzden analizin ve build'in ağırlık merkezi back office (portal) tarafıdır.

### Analiz adımları, sırayla

1. **Repo'daki referans fotoğraflarını bul ve incele.** `qrpoc` klasöründe MenuTiger ekran görüntüleri var; görsel dosyaları (png, jpg, webp) arayarak bul. Her fotoğrafı vision ile tek tek, detaylı incele. Fotoğraflar ve canlı portal (adım 2) birlikte birincil kaynaktır.
2. **Canlı portala login'li bak:** https://www.app.menutiger.com/portal
   - Browser aracını kontrol et (Claude in Chrome bağlantısı veya Playwright MCP gibi). Browser aracın yoksa kurulumu Yaren'e tek seferde, net adımlarla söyle; kurulum yapılınca devam et. Browser'ı görünür (headed) modda aç.
   - Login'i her zaman Yaren yapar. Hiçbir koşulda şifre girme, şifre isteme, şifre kaydetme. Login ekranına gelince dur, "giriş yap" de, giriş yapılınca devam et. 2FA veya doğrulama çıkarsa onu da Yaren halleder.
   - Kesinlikle read-only çalış. Portalda hiçbir şeyi değiştirme, kaydetme, silme, oluşturma; hiçbir form submit etme, save veya onay butonuna basma. Sadece gez, incele, screenshot al.
   - Portalın tüm bölümlerini sistematik gez. Her ekranın screenshot'ını `references/portal/` altına bölüm adıyla kaydet (ör. `menu-editor-01.png`).
   - Hesap, billing ve kişisel veri içeren sayfaları atla veya o alanları kadrajlama.
   - Analiz zamanının ezici çoğunluğu burada geçer.
3. **Marketing site'a hızlı bakış.** https://www.menutiger.com için sadece hızlı bir gezinti: feature adlandırmaları ve genel çerçeve notu yeterli, derinlemesine analiz yok.
4. **Figma referansı.** https://www.figma.com/design/PD58ocGJ0ogUJ0DSk3rxwn/QRPOC (Figma erişimin varsa aç. Dosya boş olabilir; doluysa görsel stil için birincil otorite kabul et, boşsa `docs/DECISIONS.md`'ye tek satır not düş.)
5. **Gerekli skill'leri kullan.** Ortamda ilgili skill'ler varsa (görsel analiz, ileride frontend-design) devreye al.
6. **Çıktıyı yaz:** `docs/REFERENCE-ANALYSIS.md`, Türkçe.

### REFERENCE-ANALYSIS.md içeriği

- **Information architecture.** Portalın tam navigasyon haritası: bölümler, alt sayfalar, hiyerarşi. Canlı portal gezisine dayanır; analizin ağırlık merkezi burası. Marketing site çok kısa bir alt başlık, birkaç satır yeterli.
- **Screen inventory.** Canlı portalda ve fotoğraflarda görülen her ekran: amacı, ana bileşenleri, layout'u; ilgili screenshot dosya adıyla eşleştir. Ekran başına kısa ve somut. Portal ekranları önce ve daha detaylı; müşteri menüsü ekranları sonra.
- **"Temiz ve ferah" hissinin anatomisi.** Bu bölüm en önemlisi; taklit edilecek şey bu his. Neyin ürettiğini somut yaz: whitespace kullanımı, card yapısı, tipografi hiyerarşisi, density seviyesi, renk kullanım disiplini, hizalama ritmi.
- **Component patternleri.** Tablolar, formlar, modallar, badge'ler, butonlar, empty state'ler, sidebar davranışı, bildirimler.
- **Multilingual pattern.** MenuTiger çok dilli desteği nasıl çözmüş: müşteri menüsünde dil switcher'ı nerede, editörde çok dilli içerik girişi nasıl. Canlı portalda birebir incele; bizim app çift dilli (TR ve EN) olacağı için bu pattern doğrudan bize temel olacak.
- **Design token çıkarımı.** Tip skalası, spacing ritmi, radius, shadow ve renk ROLLERİ (hangi rol nerede). Amaç renk değerlerini kopyalamak değil, rol sistemini anlamak; marka renkleri bizde tamamen farklı olacak.
- **QRPOC eşleme tablosu.** MenuTiger'daki hangi ekran veya pattern, Wave 1-3'teki hangi QRPOC ekranına temel oluyor. MenuTiger'da karşılığı olmayan differentiator ekranlar (memory, pre-arrival, self-service) için hangi mevcut patternlerin uyarlanacağı.
- **Açık sorular.** Onay aşamasında netleşmesi gereken noktalar, kısa liste.

Analiz bitince: commit at (`QRPOC: reference analysis`), dur, onay bekle.

---

## Genel kurallar

- **Ürün konsepti kilitli.** Konsept sahibi bu session'da değil. Feature veya scope önerme, ekleme, çıkarma, "iyileştirme" yok. Brief'in belirsiz kaldığı yerde en basit tutarlı yorumu seç ve varsayımı `docs/DECISIONS.md`'ye logla.
- **Referanstan ne alınır, ne alınmaz.** Alınır: yapı, layout mantığı, spacing ritmi, navigasyon modeli, component patternleri, etkileşim akışları, genel his. Alınmaz: logo, ikon seti, illüstrasyonlar, marka renkleri, yazılı copy. Branding tamamen farklı olacak.
- **Build fazları design prototype'tır.** Backend yok, database yok, auth yok, gerçek ödeme yok, dış API çağrısı yok. Tüm state client-side, tüm içerik typed mock fixture'lardan.
- `qrpoc` klasörü içinde çalış; dışına dokunma. Tek istisna: adım 2'deki read-only portal gezisi.
- **Dil.** Ürün çift dilli: Türkçe ve İngilizce. Kod, yorumlar ve dosya adları İngilizce. Tüm UI string'leri merkezi, typed dictionary'lerde iki dilde tutulur (`tr` ve `en`); i18n kütüphanesi ekleme, basit bir locale context ve switcher yeterli. Varsayılan dil Türkçe, İngilizce'ye geçiş switcher ile. Analiz ve karar dokümanları Türkçe.
- **Em dash (uzun tire) hiçbir yerde kullanılmaz:** UI copy'de, dokümanlarda, yorumlarda.
- Her tamamlanan ekran veya tutarlı iş biriminden sonra commit. Commit mesajları `QRPOC:` ile başlar.
- Tanımlı stack dışında dependency yok; gerekiyorsa sebep `docs/DECISIONS.md`'ye loglanır.

## Ürün bağlamı

QRPOC: müşterilerin masadaki QR kodu okutarak menüye baktığı, siparişi özelleştirip verdiği, garson çağırdığı bir platform; **app indirme yok, login yok**. Restoran tarafında back office (çalışma adı **QRapp**): menü editörü, QR ↔ masa eşleme, canlı kitchen display, analytics.

Konumlandırma: QR menü değil, POS değil. Restoranın mevcut düzeninin üstüne oturan hafif bir katman.

**Ana hedef kitle işletmeciler.** Ürünü satın alan, her gün içinde yaşayan ve değerini hisseden taraf back office'tir. Müşteri yüzeyi önemli ama ikincil; işletmecinin müşterisine sunduğu deneyim olarak back office'in kalitesini destekler.

**Ürün çift dilli (TR ve EN).** Müşteri yüzeyinde dil switcher'ı; back office'te menü içeriği iki dilde girilir. Hedef pazar önce Türkiye; turist yoğun bölgeler için İngilizce eşit derecede gerçek bir kullanım, süs değil.

İki yüzey:

- **Back office (QRapp):** desktop-first web app; sahipler ve personel için. Birincil yüzey.
- **Müşteri (QRPOC):** mobile-first web app. Giriş her zaman restoran + masa kodlayan bir QR scan. İkincil yüzey.

Tasarımın görünür kılması gereken differentiator'lar; ürünün varlık sebebi bunlar:

1. **Alerji ve diyet hafızası.** Dönen müşteri kendini yeniden anlatmaz. No-login akışın üstüne opsiyonel hesap katmanı.
2. **Derin sipariş özelleştirme.** "Turşusuz, ketçapsız, bol hardallı" seviyesinde detay, mutfağa aynen iletilir.
3. **Sürtünmesiz personel istekleri.** Garson, su, hesap; göz teması ve bekleme olmadan.
4. **Pre-arrival sipariş ve self-service pickup.**

## Tasarım yönü

- **Birincil model: MenuTiger'ın kendisi.** UI/UX kuralları ve genel his ona çok benzer: aynı temizlik, aynı ferahlık, aynı sakin density. Canlı portal, referans fotoğrafları ve analiz dokümanı bu hissin kaynağı.
- Branding farklı: renk, logo, tip kimliği bize ait olacak (yönü sonradan verilecek; o gelene kadar nötr, rol bazlı token'larla çalış).
- Figma dosyası doluysa görsel stil için birincil otorite.
- **Back office (birincil):** sakin, bilgi yoğun, yüksek taranabilirlik. Gece 23:00'te yorgun bir restoran sahibi her şeyi anında bulabilmeli. Prototype'ın kalite çıtası bu yüzeyde belirlenir.
- **Müşteri yüzeyi:** sıcak, iştah açan, hızlı hisseden. Yemek görseli ekranı taşır, chrome sessiz kalır. Birincil aksiyonlar başparmak erişiminde. Alerjen ve diyet bilgisi first-class UI, asla küçük yazı değil.
- **Kitchen display:** yüksek kontrast, 2 metreden okunur, rafta yağlı bir tablet için tasarlanmış.
- **Çift dil tasarım gerçeği.** Layout'lar iki dilin farklı metin uzunluklarında bozulmadan çalışmalı. Seçilen fontlar Türkçe karakterleri (ğ, ş, ı, İ, ö, ü, ç) tam ve düzgün render etmeli. Dil switcher'ı sessiz bir yerleşimde durur, chrome'u domine etmez.
- Erişilebilirlik: WCAG AA kontrast; müşteri yüzeyinde minimum 44 px touch target.

---

## Build fazları (DONDURULDU, analiz onayı bekliyor)

Her wave iki dilde çalışır: switcher ile TR ve EN arasında geçiş, kırılan layout yok.

### Wave 1 · Back office core (desktop-first, 1440 px birincil viewport)

1. **Menu editor.** Kategoriler, item'lar, malzemeler, alerjenler, fotoğraflar. Item adı ve açıklaması iki dilde girilir (TR ve EN alanları); editör bunu yorucu olmayan bir patternle çözer, MenuTiger'ın multilingual çözümü referans. Restoranın ana çalışma alanı; hızlı giriş ve rahat toplu düzenleme için optimize et.
2. **QR ve masa eşleme.** Masa listesi, masa başına bir QR, basit print view.
3. **Kitchen display.** Gelen siparişler canlı kart olarak, masa numarası belirgin (garson tepsiyi masa numarasına götürür), status ilerletme aksiyonları. Mock sipariş akışıyla beslenir.
4. **Analytics dashboard.** Zaman içinde siparişler, yoğun saatler, en çok satan item'lar, 3 mock lokasyon arası switcher.

### Wave 2 · Müşteri core loop (mobile-first, 390 px birincil viewport)

5. **Scan landing.** Restoran kimliği, masa bağlamı onayı, menüye giriş, dil switcher'ı (TR/EN). Ton bu ekranda kurulur: anında, güvenilir, sıfır sürtünme.
6. **Menu browse.** Kategori navigasyonu; fotoğraf, fiyat, alerjen ve diyet badge'li item kartları. Dil switcher'ı header'da da erişilebilir.
7. **Item detail.** Malzeme seviyesinde modifier'lar (çıkar ve ekle), adet, serbest not, net alerjen uyarıları.
8. **Cart ve sipariş onayı.** Özet, masa numarası; ödeme hikayesi "kasada veya garsona öde". Bu akışın hiçbir yerinde login yok.
9. **Order status.** Alındı, hazırlanıyor, hazır veya yolda. Mock timer'larla canlı his.
10. **Personel istekleri.** Garson, su, hesap; her istek görünür bir onay state'i alır.

### Wave 3 · Differentiator ekranlar

11. **Müşteri profili ve hafıza.** Alerjiler, diyet tercihleri, favori siparişler. Menünün nasıl uyum sağladığını göster: çakışan item'larda uyarı, "her zamanki" kısayolu.
12. **Pre-arrival: rezervasyon ve önden sipariş.** Restoran seç, varış saati seç, gelmeden sipariş ver.
13. **Self-service modu.** Sipariş, mock ödeme, "pickup için hazır" bildirim state'i, gişe numarası.

### Kapsam dışı. Bunların hiçbirini build etme.

Ödeme işleme, gerçek backend veya database, auth altyapısı, landing page builder (başka yerde mevcut), Google Business Profile sync, envanter, loyalty, franchise yönetimi, native mobil app'ler.

## Stack

- Next.js (App Router) + TypeScript
- Tailwind CSS + shadcn/ui
- `src/mocks/` altında typed mock fixture'lar; `src/i18n/` altında iki dilli typed UI string dictionary'leri
- Route'lar: back office `/admin`, kitchen display `/kitchen`, müşteri yüzeyi `/m/[restaurant]/[table]`
- Runtime'da başka hiçbir şey yok; gerekirse karar loglanır.

## Mock data

- 3 lokasyonlu, kurgusal, çağdaş bir Türk kafe-restoranı (admin lokasyon switcher'ı için).
- 5-6 kategoride 25-35 menü item'ı, fiyatlar TRY, otantik Türk yemekleri. Her item'ın adı ve açıklaması iki dilde (Türkçe + İngilizce karşılığı). Birkaç item zengin modifier seti ve alerjen taşımalı ki özelleştirme UI'ı gerçekten test edilsin.
- Yemek görselleri: güvenilir render oluyorsa Unsplash URL'leri, olmuyorsa özenli lokal placeholder'lar. Telifli marka görseli yok, gerçek restoran adı yok.
- Kitchen display ve analytics için mock sipariş akışı: inandırıcı hacimler, inandırıcı yoğun saatler.

## Çalışma yöntemi ve definition of done

- Her ekrandan sonra: çalıştır, screenshot al, Tasarım yönü bölümüne ve referans analizine karşı incele, geçemeyeni düzelt. Görsel self-verification beklenen davranış.
- `docs/DECISIONS.md` güncel tutulur: her varsayım ve sapma, tarihli tek satır.
- **Wave başına definition of done:** wave'deki her ekran gerçek bir click path ile erişilebilir, birincil viewport'unda doğru, iki dilde de kontrol edilmiş (switcher ile geçiş, kırılan layout yok), dead end yok, placeholder metin yok, token'lar tutarlı, `npm run build` temiz.
- **Session teslimatları:** `npm run dev` ile çalışan prototype, click path anlatımlı `README.md`, `docs/REFERENCE-ANALYSIS.md` ve `docs/DECISIONS.md`.
