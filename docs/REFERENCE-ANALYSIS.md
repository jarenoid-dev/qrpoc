# QRPOC Referans Analizi: MenuTiger

Tarih: 2026-08-14. Kaynaklar: canli portala login'li gezi (app.menutiger.com, "Ramiz'in Yeri" test hesabi, salt okuma), ekran goruntuleri `references/portal/` ve `references/customer/`, marketing sitesine hizli bakis, musteri menu app'i (menutigr.com). Figma dosyasi bos cikti; klasordeki .h2d dosyalari sifreli oldugu icin acilamadi (detay `DECISIONS.md`).

Onemli sinir: hesap Freemium oldugu icin Table Management ve Kitchen Display canli olarak kilitliydi; bu iki ekran icin ancak kilit arkasinda gorunen kadar + upsell modallari belgelenebildi.

Guncelleme (ayni gun, Yaren onayi ile): masa QR akisi ucundan ucuna canli test edildi. Gecici bir kat + masa olusturuldu ("Test" / "Masa 1"), masanin QR'i cozuldu (kisa URL kalibi: menutigr.com/<uid>), dine-in siparis login'siz verildi (Cash), portalda durum ilerletildi ve musteri stepper'inin canli guncellendigi goruldu; hot action istegi de ayni masadan gonderilip portal logunda izlendi. Test kati ve masa sonra silindi. Boylece cart, payment, order status ve hot actions ekranlarinin tamami birincil kaynaktan belgelendi.

---

## 1. Information Architecture

### 1.1 Portal navigasyon haritasi (canli geziden)

Kabuk: 260 px beyaz sol sidebar + 65 px beyaz topbar + gri kanvas icerik alani. Sidebar uc grupta, ince ayiracilarla:

```
Grup 1 (gunluk operasyon)
  Dashboard                /portal
  Menus                    /portal/menus
  Orders                   /portal/orders
  Table Management         /portal/table-management   [Premium kilidi]
  Kitchen Display          /portal/kitchen-display    [Advanced kilidi]
Grup 2 (kurulum ve buyume)
  Stores  (acilir grup)
    Store                  /portal/stores
    Taxations              /portal/taxations
  Marketing  (acilir grup)
    Website                /portal/website
    Promotions             /portal/promotions
    Surveys                /portal/surveys
    Customers              /portal/customers
  Hot Actions              /portal/hot-actions
  Reports                  /portal/reports
  Accounting  [New rozeti] /portal/accounting
  FAQ                      /portal/faq
Grup 3 (sistem)
  Integrations             /portal/integrations
  Settings                 /portal/settings
Sidebar alti: Onboarding Video karti, Download e-Book karti
```

Bolum ici hiyerarsi hep ayni iki katmanla cozuluyor: sayfa ustunde ikonlu sekme seridi, gerektiginde sekme icinde inline editor. Ucuncu seviye hicbir zaman yeni sayfa hissi vermiyor; breadcrumb + sag ustte Save butonuyla ayni kabukta acilan bir duzenleme modu.

Bolum bazinda sekmeler:

- **Menus:** Menus / Modifiers / Archive. Menu kartina tiklaninca menu editoru: solda Categories paneli, sagda item listesi. Item'a tiklaninca item editoru sekmeleri: Item Information / Price Options / Modifier Options / **Localize**. Modifier group formu da ayni kalip: form + **Localize**.
- **Orders:** Orders / Deleted Orders. Filtre satiri: Invoice ID + 4 dropdown + Apply/Reset Filter.
- **Table Management:** kilit modali kapatilinca Orders'a geri atiyor. Arkada gorunen: store karti (Store 1, Ramiz'in Yeri) + "View table orders" ve "Configure tables" aksiyonlari.
- **Kitchen Display:** kilit arkasinda "Select Your Station" ekrani: her fiziksel ekran bir istasyona atanir (Kitchen / Bar), ayar cihaza kaydedilir. Ayrica "Welcome to Kitchen Display" video onboarding diyalogu.
- **Stores > Store:** master-detail. Solda store listesi, sagda sekmeler: Tables / Users / Opening Hours / Social Accounts / WiFi [kilitli] / Location Details / Settings.
- **Marketing > Website:** Homepage / Colors [New] / Themes [New]. Solda bolum listesi (Hero, About, Featured Food, Why Choose Us, Newsletter); her bolumun sag panelinde ac/kapa toggle + Configuration ve **Localize** alt sekmeleri.
- **Hot Actions:** Create Hot Actions / Hot Action Requests.
- **Reports:** Scheduler / Newsletter signups / Feedback.
- **Accounting:** tek Orders sekmesi: store + tarih filtresi, 5 istatistik cipi, tablo, Download.
- **Integrations:** Payment Integrations / White Label [kilitli] / Printers [kilitli] / Point Of Sale.
- **Settings:** Profile / Restaurant / Notifications / Order Settings / Developer / Billing / Restaurant QR Code.

Topbar (soldan saga): sidebar daraltma, sari "Upgrade your plan", koyu tema toggle'i, **Translate** (portal arayuz dili menusu), bildirim zili, onboarding ilerleme rozeti (%0), cihaz onizleme, tam ekran, changelog rozeti, store sayaci, avatar + ayar disli.

Her sayfanin ustunde ayni baslik bandi: solda h2 baslik + tek satir aciklama, sagda QR ikonu + menu linki kopyalama + teal "OPEN APP" butonu. Bu bant portalin her ekraninda ayni yerde duruyor ve musteri menusune gecisi surekli bir tik uzakta tutuyor.

### 1.2 Musteri app'i (ikincil yuzey)

Giris URL'i restoran slug'i (menutigr.com/ramizin-yeri-...). Once website-builder ciktisi olan vitrin sayfasi (hero: "Welcome to Ramiz'in Yeri" + Our Menu butonu), oradan `/menu` rotasina geciliyor. Menu ekrani: ust bar (hamburger, logo, arama, rozetli sepet), kapak fotografi, kategori chip carousel'i, kategori basligi + 2 sutun item kartlari, altta sabit nav. Hamburger cekmecesi: Orders, Cart, Feedback, **Localizations**, Login. Item detayi ayri ekran: tam genislik foto, aciklama, meta satirlari (hazirlik suresi, boyut, siparis turu), fiyat varyantlari listesi, **Ozel Talimatlar** serbest metin alani, yapiskan alt bar (Toplam + SEPETE EKLE + adet). Tema restoranin kendi markasi (bu hesapta siyah/sari); portal temasindan tamamen bagimsiz.

Kritik baglam ayrimi: iki giris modu ayni app'in iki farkli halini aciyor.
- **Restoran linki** (menutigr.com/<slug>): online menu modu. Alt nav Home / Orders / Cart. Checkout musteri hesabi ister (guest checkout kapaliysa login duvari).
- **Masa QR'i** (menutigr.com/<uid>, ornekte /xaKQ): dine-in modu. Alt nav **Orders / Hot actions / Cart** olur; Hot actions yalniz masa baglaminda gorunur. Checkout login istemez: dogrudan Payment ekranina gider. QRPOC'un no-login vaadi bu modun karsiligi.

### 1.3 Marketing site (kisa not)

menutiger.com: Features (11 alt sayfa: QR Code Menu, Online Food Order System, Table-side Ordering, Website Builder, Website & Menu Templates, Analytics & Data Insight, Integrations, Branding & White Label, Feedback Management, Kitchen Display System, Marketing Tools), E-books, Blog, POS (coming soon), Pricing, FAQ. Pricing 4 katman: Freemium $0 (10 masa, 1 store), Regular $17, Advanced $46 (KDS burada acilir), Premium $119 (Table Management + white-label). Feature adlandirmalari QRPOC ekran adlari icin dogrudan kullanilabilir sozluk niteliginde. Yardim merkezi yok; FAQ sayfasi bu rolu goruyor.

---

## 2. Screen inventory

Portal ekranlari once, her biri ilgili screenshot dosyasiyla.

### 2.1 Portal

**Dashboard** (`portal/dashboard-01.png`)
Amac: gunun nabzi. Bilesenler: Today/Week/Month segmenti + tarih araligi + store filtresi; 4 istatistik karti (Total Orders lacivert, Revenue teal gradient, Customers lacivert, Feedback beyaz); Total Orders cizgi grafigi (Orders/Sales secimli, SVG/PNG/CSV indirme menulu); QR Scan Count ve Most Sold Foods kartlari. Layout: genis sol sutun (grafik) + dar sag sutun (kucuk kartlar). Bos veri durumunda her kart kendi illustrasyonlu empty state'ini gosteriyor.

**Menus listesi** (`portal/menus-01-list.png`)
Amac: menu koleksiyonu. Bilesenler: Menus/Modifiers/Archive sekmeleri, teal Add New, bilgi pill'i, menu kartlari grid'i (kapak, kebab menu, "Connected" yesil outline rozeti), kesikli cizgili + kartli "yeni ekle", rows-per-page + sayfalama. Kart grid'i tablo degil; menu sayisi az oldugu icin kart secilmis.

**Menu editoru** (`portal/menu-editor-01-categories.png`)
Portalin kalbi. Layout: ust bant (geri oku + menu adi), solda Categories paneli (baslik + yesil kare "+"; her satir: surukleme tutamaci, ad, kebab; secili satir acik teal), sagda breadcrumb (Categories / Salads) + Add New + arama, item satirlari: checkbox, tutamac, kucuk foto, ad, dine-in/takeaway mini rozetleri, sag hizali fiyat (10.00 TRY), kebab. Satirlar ayri beyaz kartlar, ~72 px yukseklik. Toplu secim + surukleyerek siralama ayni listede.

**Item editoru: Item Information** (`portal/menu-editor-02-item-info.png`)
Inline tam sayfa form (modal degil): breadcrumb + sag ustte Save. Alanlar: Name*, Description* (zengin metin: Normal/H1-H3, bold, italik, liste, link), Labels (coklu secim), Display on* (Dine in / Takeaway chip'leri), Size + Unit, Preparation time, **Ingredient Warnings** (alerjen coklu secimi), Tax Categories, Mark as sold out / Availability / Featured toggle'lari, Recommended, Images dropzone ("Preferred size is 400px * 300px").

**Item editoru: Price Options** (`portal/menu-editor-03-price-options.png`)
Bilgi pill'i ("Items can have price options according to their sizes, servings etc."), Price* satirlari (deger + cop kutusu) + kesikli "ADD NEW". Ad bos birakilirsa tek fiyat. Musteri tarafinda Small/Medium/Large olarak goruluyor.

**Item editoru: Modifier Options** (`portal/menu-editor-04-modifier-options.png`)
Tek satirlik aciklama + Modifier Groups coklu secim dropdown'u. Gruplar global olarak Menus > Modifiers'ta tanimlanip item'a buradan baglaniyor.

**Item editoru: Localize** (`portal/menu-editor-05-localize.png`, `menu-editor-06-localize-expanded.png`)
"Text localization" basligi + dil basina akordeon (bu hesapta "Turk"). Akordeon acilinca o dile ait Name ve Description (zengin metin) alanlari. Ceviri ana formdan tamamen ayri tutulmus.

**Modifier group formu** (`portal/menus-03-modifier-group-form.png`)
Name*, Type (Optional/Required radio), "Allow adding same choice multiple times" checkbox'i, Modifiers tablosu (Name / Price / Unit kolonlari, satir silme, satir ekleme). Ikinci sekme yine Localize. QRPOC'un derin ozellestirme modelinin birebir karsiligi.

**Orders** (`portal/orders-01.png`, dolu hali `orders-02-with-order.png`, durum menusu `orders-03-status-dropdown.png`, `orders-04-inprogress.png`)
"Food orders / Order Monitoring and History". Orders / Deleted Orders sekmeleri. Filtre satiri: Invoice ID araması + store/odeme/teslimat/menu dropdown'lari + teal Apply Filter + outline Reset Filter. Tablo kolonlari: Invoice ID, Payment method, Total, Date, Time, Delivery method, Paid status, Order status. Dolu satirda: Payment "Cash" chip'i; Delivery method hucresi iki chip (DINE-IN + masa adi "Masa 1"); Paid status kirmizi "Not Paid" dropdown'u; Order status sari "Pending" dropdown'u (secenekler: Pending / In-Progress / Completed); satir sonunda bilgi, fis ve sil ikonlari. Durum ve odeme, tabloyu terk etmeden satir ici dropdown'larla yonetiliyor; bu, QRPOC siparis yonetiminin cekirdek etkilesim kalibi.

**Table Management** (`portal/table-management-01.png`, `table-management-02-locked.png`)
Premium kilidi: tam ekran upsell modali (video + turuncu "Claim 14-Day Free Trial" + Upgrade / Compare plans); kapatinca bolumden cikariyor. Arkada: store karti + View table orders / Configure tables. Masa listesi bu hesapta gorulemedi; Stores > Tables sekmesi kismi ikame (asagida).

**Kitchen Display** (`portal/kitchen-display-01.png`)
Advanced kilidi, ayni upsell kalibi (30 gun deneme). Kilit arkasinda: "Select Your Station" + Kitchen / Bar istasyon butonlari; "Each screen should be assigned to a station. This setting is saved to this device only." Cihaz basina istasyon atama konsepti QRPOC KDS'i icin dogrudan alinabilir.

**Stores > Tables** (`portal/stores-01-list.png`; dolu ornekler `stores-06-table-created.png`, `stores-07-table-qr-popover.png`, `stores-08-delete-confirm.png`)
Master-detail. Solda Stores paneli (arama + kilit ikonu + store satirlari). Tables sekmesi: mavi bilgi banner'i ("Changing the QR style will apply to all tables across all floors..."), "+ Add Floor" outline butonu, sag ustte "Customize QR Code", kat filtresi, masa listesi. Kat > masa > QR hiyerarsisi. Canli testte olculenler: kat olusturma kucuk modal (Floor Name + Cancel/Create); masa ekleme inline form (breadcrumb + Name satirlari + Save, coklu ekleme destekli); masa karti uzerinde QR onizleme popover'i, indirme ve kebab (Edit / Move to Floor); satir checkbox'i secilince ust seritte toplu aksiyonlar beliriyor ("Download QR Codes" + kirmizi "Delete"); silme onayi kisa modal ("You can't undo this action" + Cancel/Confirm). Her masanin QR'i kisa URL'e gider: menutigr.com/<uid>.

**Stores > Users** (`portal/stores-04-users.png`)
Add New + tablo: First name / Last name / Email / Role. Store seviyesinde rol bazli personel modeli.

**Stores > Opening Hours** (`portal/stores-05-opening-hours.png`)
Gun basina satir karti: gun adi + toggle | baslangic saati | bitis saati | yesil "+" (ikinci zaman araligi ekleme). Tekrarli satir kalibinin en temiz ornegi.

**Stores > Settings** (`portal/stores-02-settings.png`, `stores-03-settings-scrolled.png`)
Order Settings karti iki kolon: QR Menu (Enable dine in / Enable takeaway toggle'lari) ve Online Menu (Enable pickup / Enable delivery / Enable guest checkout). Delivery Checkout Fields: alan basina Required/Optional/... dropdown'u (Recipient phone, Apartment/Floor, State, ZIP, Country, Delivery notes) + Delivery Charge (TRY). Food Menu Settings: **Allow special instructions** toggle'i (musteri serbest notunun anahtari), Display full food name, Select Menu (store'a menu baglama: "Sample Menu"). Order notification settings: e-posta toggle'i + e-posta listesi (Add email).

**Settings > Restaurant** (`portal/settings-01-restaurant.png`, `settings-03-languages-currency.png`)
Logo dropzone, kapak fotografi, restoran kimlik alanlari ve kritik uclu: **Languages** (coklu secim chip: English + Turk), **Default language** (English), **Currency** (Turkish Lira). Icerik dillerinin tek tanim yeri burasi. (Not: `settings-03` kisisel veri kadrajlamamak icin kirpildi.)

**Settings > Order Settings** (`portal/settings-04-order-settings.png`)
Customers karti: Enable Customer Tip / Enable Cancel Order toggle'lari. Invoice karti: Invoice ID Prefix.

**Settings > Restaurant QR Code** (`portal/settings-05-restaurant-qr.png`)
QR ozellestirici: solda akordeon paneller (Logo, Pattern, Eyes, Colors, Frame), sagda canli QR onizleme + indirme + kopyalama + hedef URL. Konfigurasyonu solda, sonucu sagda canli gosteren iki kolon kalibi.

**Hot Actions** (`portal/hot-actions-01.png`, istek logu `hot-actions-02-requests.png`)
QRPOC personel isteklerinin birebir karsiligi. Create Hot Actions sekmesi: tablo Header / Image / Message + satir basina toggle, edit, delete. Hazir tanimlar: "Call someone", "Call for notes change", "Call to verify bill", "Call to clean table". Add New kilitli (ozel aksiyon ust planda). Hot Action Requests sekmesi gelen isteklerin logu: Today/Week/Month segmenti + filtreler; tablo Icon / Header / **Table** / Status (sari "Active" dropdown) / Requested On / Approved On. Musterinin masadan gonderdigi istek buraya masa adiyla dusuyor; canli dogrulandi.

**Marketing > Website** (`portal/marketing-01-website.png`)
Website builder: solda bolum listesi, sagda bolum toggle'i + Configuration / Localize alt sekmeleri; alan etiketi solda-icerde kalibi (Button Link, Redirect to, Heading, Description).

**Marketing > Promotions / Surveys / Customers** (`portal/marketing-02..04`)
Ucu de ayni liste kalibi: Add New + bilgi pill'i + tablo + empty state. Promotions kolonlari: Name / Description / Schedule Status.

**Reports** (`portal/reports-01.png`)
Scheduler: zamanlanmis rapor e-postalari (Name / Frequency / Report) + Download. Newsletter signups ve Feedback ayri sekmeler.

**Accounting** (`portal/accounting-01.png`)
Store + tarih filtresi, 5 acik-teal istatistik cipi (Total sales, Total discounts, Total orders, Total tax, Total tip; etiket kartin ust kenarina oturuyor), genis tablo, Download. Not: alt baslikta ham i18n anahtari ("accounting-description") ve kucuk harf kolon adlari (subtotal, tax) gorunuyor; kopyalanmamasi gereken ozensizlik ornekleri.

**Integrations** (`portal/integrations-01.png`)
Kart grid'i: Stripe / PayPal / Adyen ("Connect" outline butonlu), **Cash** (toggle, bu hesapta acik) ve Custom Payment (toggle + ayar disli). "Kasada ode" akisinin kaynagi Cash entegrasyonunun acik olmasi. White Label ve Printers sekmeleri kilitli.

**FAQ** (`portal/faq-01.png`)
Portal ici yardim: kategori bazli akordeon SSS.

**Taxations** (`portal/taxations-01.png`)
Standart liste kalibi (vergi kategorileri; item editorundeki Tax Categories buradan besleniyor).

**Topbar Translate menusu** (`portal/topbar-01-language-menu.png`)
Portal arayuz dili dropdown'u: English, Espanol, Francais, Deutsch, Italiano, Nederlands, Portugues, Arapca... Native ad + parantezde Ingilizce ad. Icerik dillerinden tamamen ayri bir sistem.

### 2.2 Musteri app'i

**Vitrin** (`customer/customer-01-landing.png`): kapak ustune buyuk baslik + tagline + kisa paragraf + Our Menu. Website builder'daki Hero bolumunun render'i.

**Menu** (`customer/customer-02-menu.png`): kategori chip carousel'i (koyu pill'ler + ok), kategori basligi, 2 sutun item kartlari (foto, ad, 2 satirla kirpilan aciklama, fiyat "₺ 10" veya araligi "₺ 10 - ₺ 20", sari "+"), altta sabit Home/Orders/Cart. Footer: Contact + Opening hours.

**Cekmece** (`customer/customer-03-drawer.png`): Orders, Cart, Feedback, Localizations, Login.

**Localizations** (`customer/customer-04-localizations.png`): tam ekran dil listesi: "English (English)" secili, "Turkce (Turkish)".

**Turkce secili menu** (`customer/customer-05-turkish.png`): chrome Turkcelesti (Ana Sayfa / Siparisler / Sepet) ama item adlari ve aciklamalari Ingilizce kaldi; ceviri girilmemis icerik varsayilan dile dusuyor, otomatik ceviri yok.

**Item detayi** (`customer/customer-06-item-detail.png`, `customer-07-item-notes.png`, `customer-08-item-note-filled.png`): tam genislik foto, aciklama kutusu, meta satirlari (Hazirlik Suresi: 10 dakika, Boyut: 150 grams, Siparis Turu), Fiyat Varyantlari listesi (Small/Medium/Large + fiyat + checkbox), **Ozel Talimatlar** serbest metin alani, yapiskan alt bar: Toplam, SEPETE EKLE, adet steperi. Not alaninin placeholder'i alerji odakli: "Please let us know if you are allergic to anything or if we need to avoid some ingredients". Detay ekrani ayni kategorideki item'lar arasinda yatay kaydirilabilen bir carousel; her slaytin kendi varyant + not alani var.

**Cart** (`customer/customer-09-cart.png`): "My cart" basligi + geri oku; item satiri (kucuk foto, ad, fiyat, sag ustte cop ikonu, adet steperi), "Add more items" butonu, **Add tip** bolumu (%5 / %10 / %15 / %20 preset butonlari + "or an amount?" serbest alan), Subtotal satiri, yapiskan alt bar: Total + siyah CHECKOUT.

**Checkout, online modda** (`customer/customer-10-checkout.png`): restoran linkinden gelindiginde CHECKOUT musteri Login ekranina cikiyor (Email + Password + Sign up; Google secenegi yok). Sebep: "Enable guest checkout" kapali. Not: bu toggle'i portaldan acma denemesi de sessizce basarisiz oldu (Save tiklaninca API'ye istek gitmiyor; olasi client-side dogrulama hatasi veya plan kisiti).

**Masa baglamı: dine-in akisi** (masa QR'i uzerinden, login'siz):
- **Masa menusu** (`customer/customer-12-table-menu.png`): ayni menu ama alt nav Orders / **Hot actions** / Cart.
- **Hot actions istek ekrani** (`customer/customer-13-hot-actions.png`, `customer-14-hot-action-selected.png`): "Requests" basligi, 4 istek karti (CALL SOMEONE, CALL FOR NOTES CHANGE, CALL TO VERIFY BILL, CALL TO CLEAN TABLE; illustrasyon + baslik + aciklama), secim yapilana kadar pasif REQUEST butonu. Istek portal loguna masa adiyla dusuyor.
- **Payment** (`customer/customer-16-payment.png`, `customer-17-pay-with-cash.png`): login YOK; Payment options (Cash) + Order summary (Delivery method: DINEIN, Subtotal, Discounts, VAT, Total). Cash secilince "Complete your purchase and pay with cash on delivery." metni + "Pay with cash" butonu.
- **Siparis sonrasi** (`customer/customer-18-order-placed.png`): sepet sifirlanir, alt navda Orders rozeti yanar.
- **Active orders** (`customer/customer-19-order-status.png`): "You have 1 active order" + restoran basligi + siparis karti (invoice no, PENDING rozeti, tarih-saat, tutar).
- **Siparis detayi ve durum stepper'i** (`customer/customer-20-order-detail.png`, `customer-21-order-inprogress.png`): uc adimli yatay stepper **PENDING - INPROGRESS - COMPLETED** (aktif adim dolu daire), Order items listesi, Order summary (DINEIN chip'i). Portalda durum degistirilince stepper aninda ilerliyor; canli dogrulandi.

---

## 3. "Temiz ve ferah" hissin anatomisi

Taklit edilecek sey bu bolum. His su somut kararlardan cikiyor:

1. **Uc katmanli zemin, cizgisiz ayrim.** Acik gri kanvas (#DCE0E4) ustunde beyaz yuzeyler; sidebar ve topbar da beyaz. Kartlarda golge yok denecek kadar az; ayrimi renk farki yapiyor (gri/beyaz), border veya golge degil. Sonuc: cok bolme var ama gorsel gurultu yok.
2. **Tek vurgu rengi, katı gorev dagilimi.** Teal yalnizca aksiyon ve aktif durum (birincil buton, secili sekme, secili nav item'i, toggle-acik). Bir ekranda ayni anda en fazla 1-2 dolu teal buton var. Sari yalnizca plan/upsell (Upgrade, New rozeti). Kirmizi yalnizca yikici aksiyon ve uyari rozetleri. Geri kalan her sey notr gri tonlari. Renk her gorundugunde bir anlam tasidigi icin ekran sakin kaliyor.
3. **Comert bosluk olcusu.** Kanvas padding'i 20 px, kart ici ~24 px, form alanlari arasi ~16 px, liste satirlari ~72 px, topbar 65 px. Hicbir liste sıkıştırılmamis; Modifier Options gibi tek alanli sekmeler kocaman bos alanla yayinlaniyor ve bu bir hata gibi degil, nefes gibi duruyor.
4. **Dusuk yogunluk varsayilani.** Ekran basina tek ana is karti. Tablolar 4-9 kolonla sinirli. Ust uste iki farkli is akisi ayni ekrana konmuyor; ikinci is her zaman sekmeye veya inline editore taşınıyor.
5. **Tipografik sakinlik.** Tek font (Roboto). Sayfa basligi 24 px / 500; govde ve nav 14 px / 400; buton ve tablo basligi 14 px / 500. Bold neredeyse hic yok; hiyerarsi agirlikla degil renkle kuruluyor: basliklar #121926, govde #364152, yardimci metin gri.
6. **Hizalama ritmi.** Icerik tek sol cizgiye oturuyor; sag kenar aksiyonlara ayrilmis (Save, Add New, fiyat, kebab). Baslik bandi + sekme seridi + icerik karti her ekranda ayni dikey sirada; kullanici hicbir ekranda yeni bir duzen ogrenmiyor.
7. **Tutarli yumusak koseler.** Kart 8 px, buton ve input 4-8 px, yardim pill'leri ve Need Help tam yuvarlak. Koseler asla dekoratif buyukluge cikmiyor.
8. **Nazik empty state'ler.** Her bos liste ayni clos illustrasyonu + "No records availble" + tek satir yonlendirme ("Click 'Add New' to create a new record"). Bos ekran hata gibi degil, davet gibi.
9. **Yardim her yerde ama sessiz.** Soru isareti ikonlu outline hint pill'leri baslik hizasinda duruyor, icerigi isgal etmiyor. Videolu onboarding yalniz kilit/ilk kullanim anlarinda modal oluyor.
10. **Ferahligin istisnasi bilincli:** Dashboard'daki lacivert ve teal-gradient stat kartlari sayfadaki tek "agir" renk blogu; sayilara agirlik vermek icin kullanilmis. Bu kontrast, geri kalan her seyin ne kadar acik oldugunu vurguluyor.

QRPOC icin ozet kural: az renk + cok bosluk + tek font + cizgisiz katman ayrimi + her ekranda ayni iskelet.

---

## 4. Component patternleri

- **Sayfa baslik bandi:** beyaz serit; solda h2 + tek satir aciklama, sagda QR + link kopyala + OPEN APP. Sabit bağlam cıpası.
- **Sekme seridi:** acik gri bant ustunde ikon + etiket; aktif sekme teal metin + alt cizgi; tasan sekmelerde yatay kaydirma oklari. Kilitli sekme gri ve tiklanamaz (WiFi, White Label, Printers).
- **Liste sayfasi kalibi:** [teal Add New] + [hint pill] + [sagda arama] ustte; tablo veya kart grid'i ortada; rows-per-page + "1-1 of 1" + ok sayfalama altta. Promotions, Surveys, Customers, Users, Taxations, Modifiers hep ayni kalip.
- **Tablolar:** 14 px, baslik 500, satir ayirici #EEE, zebra yok. Satir aksiyonlari sag uçta: durum toggle'i + mavi kalem + kirmizi cop (Hot Actions ornek).
- **Inline editor (modal degil):** olusturma ve duzenleme, listeyle ayni kabukta acilan tam sayfa forma gidiyor; ust bantta breadcrumb (ust seviye / alt seviye) + sag ustte tek Save. Iptal yerine geri oku. Modal yalnizca upsell ve onboarding videosu icin.
- **Form alanlari:** MUI outlined tarz; iki varyant: etiket alanin icinde solda sabit hucre gibi ("Restaurant name * | deger", "Heading * | deger") veya floating label. Zorunluluk kirmizi yildizla. Bilgi gereken alanda soru ikonu.
- **Required/Optional dropdown kalibi:** checkout alan konfigurasyonunda her alan bir dropdown'la zorunlu/opsiyonel/kapali yapiliyor; alan listesi sabit, davranisi secilebilir.
- **Toggle satir kutulari:** ince border'li beyaz satir: solda etiket (+ soru ikonu), sagda switch. Ayar ekranlarinin tamami bu satirlarla kurulu.
- **Master-detail:** Stores'ta sol dar liste paneli (arama + satirlar) + sag sekmeli detay. Cok store'lu hesapta olceklenen kalip.
- **Tekrarli satir + ekle:** Opening Hours (gun satiri + "+"), Price Options (fiyat satiri + ADD NEW), Modifiers tablosu (satir + ekle). Ayni zihinsel model her yerde.
- **Iki kolon konfigurasyon + canli onizleme:** QR ozellestirici (solda akordeon ayarlar, sagda canli QR).
- **Badge'ler:** "New" sari dolu; "Connected" yesil outline; sayi rozetleri kirmizi daire; dine-in/takeaway mini ikon rozetleri item satirinda.
- **Empty state:** gri clos illustrasyonu + kalin kisa mesaj + acik gri yonlendirme satiri.
- **Feature gating:** uc mekanizma: (a) kilit ikonlu devre disi buton (Add New kilitli), (b) gri kilitli sekme, (c) tam ekran upsell modali (video + turuncu gradient CTA + "No credit card" guven satiri + Upgrade/Compare ikincil aksiyonlari); modal kapatilinca bolumden cikarma.
- **Bildirim ve yardim:** topbar zil; sag kenara yapisik kirmizi dikey "Feedback" sekmesi; sag altta teal "Need Help?" pill'i (canli destek). Uc kanal da iceriğin disinda, kenarlarda.
- **Drag-and-drop:** kategori ve item satirlarinda alti nokta tutamac; siralama listede yapiliyor, ayri "siralama modu" yok. Toplu secim icin satir basi checkbox.

---

## 5. Multilingual pattern

MenuTiger dili uc bagimsiz katmanda cozmus; QRPOC'un TR/EN modeli icin dogrudan sablon:

1. **Portal arayuz dili (kullanici tercihi).** Topbar'daki Translate ikonu sabit urun dilleri listesini aciyor (English, Espanol, Francais, Deutsch, Italiano, Nederlands, Portugues, Arapca...). Restoranin icerik dillerinden tamamen bagimsiz; sadece back office chrome'unu cevirir.
2. **Icerik dilleri (restoran konfigurasyonu).** Settings > Restaurant icinde: Languages coklu secim (chip'ler: English + Turk), Default language, Currency. Burada secilen liste her yerde ceviri yuvalarini turetir.
3. **Icerik cevirisi girisi (varlik basina Localize sekmesi).** Ana form her zaman tek dilde (varsayilan dil). Ceviri, item / modifier group / website bolumu gibi her varlikta ayri bir "Localize" sekmesi: dil basina akordeon, icinde o dilin Name + Description alanlari. Ceviri girilmezse musteri tarafi varsayilan dile duser; otomatik ceviri yok.
4. **Musteri dil secimi.** Hamburger cekmecesinde "Localizations" tam ekran listesi: native ad + parantezde Ingilizce ad, secili olan vurgulu. Secim chrome dizelerini aninda cevirir (Ana Sayfa / Siparisler / Sepet); icerik ceviri varsa cevrilir, yoksa varsayilan kalir.

QRPOC'a uyarlama notlari:
- Iki dilli (TR/EN) sabit bir urunde 1. ve 2. katman birlesebilir; ama "icerik dili" ile "arayuz dili" ayriminin kendisi korunmali (musteri Ingilizce chrome + Turkce icerik gorebilmeli ve tersi).
- **Karar (2026-08-14, Yaren):** menu editorunde TR ve EN alanlari ayni formda yan yana girilir; MenuTiger'in ayri Localize sekmesi kalibi alinmaz. Fallback kurali yine gecerli: bos birakilan dil, dolu dile duser.
- Fallback kurali aynen alinmali: cevirisi olmayan icerik varsayilan dilde gosterilir, bos gosterilmez.
- Musteri switcher'i MenuTiger'da cekmecede gomulu; QRPOC brief'i "sessiz ama erisilir" diyor ve scan landing + header'da istiyor. Cekmece-only yerlesimi kopyalanmayacak.

---

## 6. Design token cikarimi (roller)

Olculen degerler (getComputedStyle, 1440 px viewport) ve rol sistemi. Amac deger kopyalamak degil; QRPOC kendi degerlerini bu rollere koyacak.

**Tipografi**
- Tek aile: Roboto (QRPOC kendi fontunu secer; Turkce karakter kapsami sart).
- Roller: `page-title` 24/500, `body` ve `nav-item` 14/400, `button` ve `table-header` 14/500, `helper` ~12/400. Buton metinlerinde textTransform none (OPEN APP istisna, uppercase).
- Hiyerarsi agirlikla degil renk tonuyla: `text-strong` #121926, `text-body` #364152, `text-muted` gri.

**Renk rolleri**
- `action-primary`: teal #2CA58D (butonlar, aktif sekme, secili nav, toggle-on). Ikincil varyant #14B8A6 (OPEN APP).
- `canvas`: #DCE0E4; `surface`: #FFFFFF; `surface-tint`: acik teal (secili nav pill'i, secili kategori).
- `border-subtle`: #EEEEEE (tablo ayiraclari, satir kutulari).
- `upsell`: sari #FFE57F (Upgrade, New) ve turuncu gradient (deneme CTA'lari). QRPOC'ta plan/upsell yok; bu rol muhtemelen dusuyor.
- `destructive`: kirmizi (cop ikonlari, rozetler, Feedback sekmesi).
- `success`: yesil outline ("Connected").
- `info`: teal outline + soru ikonu (hint pill'leri, bilgi banner'lari).
- `stat-emphasis`: lacivert (#0D1B3E civari) ve teal gradient; yalniz dashboard stat kartlari.
- Musteri tarafinda tema restoran markasina ait (ornekte siyah + sari aksan); portal paletinden bagimsiz. QRPOC'ta da musteri yuzeyi ayri paletle kurulacak.

**Bicim**
- Radius: `card` 8 px, `control` 4-8 px, `pill` tam yuvarlak.
- Golge: yuzeylerde yok (katman ayrimi renkle); butonlarda hafif MUI elevation; yalniz modallarda belirgin golge.
- Spacing ritmi 4/8 grid: kanvas 20, kart ici 24, alan arasi 16, liste satiri ~72, topbar 65, sidebar 260.

**Altyapi notu:** portal MUI (Material UI) tabanli hazir bir admin iskeleti uzerine kurulmus (Berry tarzi). QRPOC shadcn/ui + Tailwind ile ayni ROLLERI kuracak; MUI'nin floating label veya elevation detaylarini birebir taklit etmeye calismayacak.

---

## 7. QRPOC esleme tablosu

| QRPOC ekrani (Wave) | MenuTiger temeli | Ekran goruntusu | Not |
|---|---|---|---|
| W1-1 Menu editor | Menu editoru: iki panel + inline item editoru + modifier groups | `menu-editor-01..04`, `menus-03` | Kalip aynen; iki dilli giris karari acik (Localize sekmesi vs yan yana alanlar) |
| W1-2 QR ve masa eslemesi | Stores > Tables (Add Floor, kat filtresi, Customize QR Code) + QR ozellestirici | `stores-01`, `settings-05` | Kat kavrami QRPOC kapsaminda yok; masa listesi + masa basina QR + print view yeter |
| W1-3 Kitchen display | KDS istasyon secimi (cihaz basina) + upsell arkasi yapi; canli panosu kilitliydi | `kitchen-display-01` | Kanban kolonlu pano marketing gorsellerinden + brief kurallarindan turetilecek (yuksek kontrast, 2 m okunurluk) |
| W1-4 Analytics dashboard | Dashboard (segment + tarih + store filtresi + stat kartlari + grafikler) + Accounting cipleri | `dashboard-01`, `accounting-01` | 3 mock lokasyon switcher'i = store filtresi dropdown kalibi |
| W2-5 Scan landing | Masa QR'i kisa URL'e gider (menutigr.com/<uid>), dogrudan masa baglamli menu acilir; vitrin sayfasi ayri | `customer-01`, `customer-12` | QRPOC masa bagalami onayini ekler; dil switcher'i burada gorunur olacak |
| W2-6 Menu browse | Musteri menu: chip carousel + bolumlu 2 sutun grid + alt nav (dine-in modda Orders / Hot actions / Cart) | `customer-02`, `customer-12` | Alerjen/diyet rozetleri QRPOC'ta karta cikar (MenuTiger kartta gostermiyor) |
| W2-7 Item detail | Item detayi: foto + meta + fiyat varyantlari + Ozel Talimatlar + yapiskan toplam bari | `customer-06..08` | Malzeme cikar/ekle seviyesi icin modifier group + serbest not birlesimi |
| W2-8 Cart ve onay | My cart + Payment ekrani: Cash + DINEIN ozetli siparis onayi, login'siz | `customer-09`, `customer-16..18` | "Kasada veya garsona ode" = Cash odeme secenegi; dine-in modda login duvari yok, birebir dogrulandi |
| W2-9 Order status | Active orders listesi + uc adimli stepper (PENDING / INPROGRESS / COMPLETED); portal dropdown'u ile canli senkron | `customer-19..21`, `orders-02..04` | QRPOC durum dili: Alindi / Hazirlaniyor / Hazir; stepper kalibi aynen |
| W2-10 Personel istekleri | Musteri Requests ekrani (4 kart + REQUEST) + portal Hot Action Requests logu (masa adiyla) | `customer-13..15`, `hot-actions-01..02` | Birebir temel; QRPOC musteri tarafinda gorunur onay state'i ekler |
| W3-11 Musteri profili / hafiza | Dogrudan karsilik yok | | Uyarlama: toggle satir kutulari (ayarlar), chip coklu secim (alerjiler; Languages chip kalibi), item rozetleri (uyari) |
| W3-12 Pre-arrival | Dogrudan karsilik yok | | Uyarlama: store secimi (master-detail listesi), Opening Hours satir kalibi (saat secimi), menu browse akisi |
| W3-13 Self-service | Dogrudan karsilik yok | | Uyarlama: order status + gise numarasi icin stat-kart tipografisi (dashboard buyuk sayi stili) + KDS kontrast kurallari |

Genel kural: MenuTiger'dan alinan sey iskelet ve kaliplar (baslik bandi, sekme seridi, liste kalibi, inline editor, toggle satirlari, empty state, master-detail). Alinmayan: logo, ikon seti, illustrasyonlar, marka renkleri, yazili copy, upsell/gating mekanizmalari.

---

## 8. Acik sorular ve cozumleri (2026-08-14 guncellemesi)

1. **Iki dilli menu girisi:** KARAR: TR ve EN alanlari ayni formda yan yana. Localize sekmesi kalibi alinmayacak.
2. **Gating kaliplari:** Yaren kararsiz kaldi; en basit tutarli yorum uygulanacak: prototype'ta plan/kilit/upsell kaliplari tamamen kapsam disi. Ileride istenirse ayri karar olur.
3. **KDS gorsel kaynagi:** ONAYLANDI: pano tasarimi marketing gorselleri + brief kurallarindan turetilecek; deneme baslatilmayacak.
4. **Cart/checkout/status:** COZULDU: masa QR'i uzerinden dine-in akisi login'siz calisti; payment, siparis onayi, order status stepper'i, portal siparis yonetimi ve hot action dongusu ucundan ucuna belgelendi (`customer-12..21`, `orders-02..04`, `hot-actions-02`). Online moddaki login duvari ve calismayan guest checkout toggle'i ayrica not edildi.
5. **Dashboard stat kartlari:** ERTELENDI: marka yonu belirlenince karar verilecek.
6. **h2d dosyalari:** Import adimlari yazildi: `references/h2d-figma-import.md`. Import, html.to.design eklentisinin Figma icinde elle calistirilmasini gerektiriyor; MCP uzerinden otomatiklestirilemiyor.
