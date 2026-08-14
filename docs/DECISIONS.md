# QRPOC Kararlar ve Varsayımlar

- 2026-08-14: Brief v4.2 BRIEF.md olarak kaydedildi ve commit'lendi; onceki surum repoda hic var olmadi (repo bu gun git init ile kuruldu).
- 2026-08-14: "Menu Tiger Screens" klasorunde png/jpg/webp yok; 8 dosyanin tumu .h2d uzantili (html.to.design Figma eklentisinin sifreli yakalama formati, dogrudan goruntulenemiyor). Vision incelemesi yerine canli portal gezisi birincil gorsel kaynak olarak kullanildi. Dosya adlari yakalanan ekranlari belgeliyor: /portal, /portal/menus x3, iki ayri menunun menu-editor'u x3, ayrica bir Behance UI referansi (Cortex AI Chatbot SaaS).
- 2026-08-14: Figma QRPOC dosyasi (PD58ocGJ0ogUJ0DSk3rxwn) bos: tek sayfa "Startup Pitch", icerik yok. Gorsel stil otoritesi olarak kullanilamadi.
- 2026-08-14: Marketing site analizi v2 brief doneminde derin yapilmisti; v4.2 geregi dokumanda yalnizca kisa bir alt baslik olarak yer aliyor.
- 2026-08-14: "Menu Tiger Screens" klasoru commit'lere dahil edilmedi (buyuk binary referans dosyalari, brief commit'leri dar kapsamli). Yaren isterse ayri karar ile eklenir.
- 2026-08-14: Portal gezisi Playwright (headed Chromium) ile yapildi; login Yaren tarafindan girildi. Salt okuma korundu: hicbir Save/submit basilmadi, deneme (trial) baslatilmadi, siparis verilmedi, toggle degistirilmedi.
- 2026-08-14: Musteri yuzeyi ekran goruntuleri icin `references/customer/` klasoru acildi; brief'in tanimladigi `references/portal/` portala ayrildi.
- 2026-08-14: Hesap Freemium oldugu icin Table Management (Premium) ve Kitchen Display (Advanced) canli incelenemedi; kilit arkasinda gorunen kadar + upsell kaliplari belgelendi. Musteri cart/checkout/status ekranlari siparis vermeden gorulemedigi icin kapsam disi kaldi.
- 2026-08-14: `settings-03-languages-currency.png` kisisel veri (e-posta) kadrajlamamak icin dil/para birimi satirlarina kirpildi. Stores > Users tablosu bos oldugu icin kisisel veri icermiyor.
- 2026-08-14: Musteri app'inde dil Turkce'ye yalnizca analiz tarayicisinin oturumunda cevrildi (fallback davranisini gozlemlemek icin); hesap verisi degismedi.
- 2026-08-14 (Yaren kararlari, acik sorular turu): (1) Menu editorunde iki dilli giris TR ve EN alanlari ayni formda yan yana; Localize sekmesi kalibi alinmayacak. (3) KDS tasarimi marketing gorselleri + brief kurallarindan turetilecek, deneme baslatilmayacak. (5) Dashboard stat karti stili marka yonune ertelendi.
- 2026-08-14 (varsayim, soru 2 "bilmiyorum" kaldigi icin en basit tutarli yorum): prototype'ta plan/kilit/upsell kaliplari tamamen kapsam disi.
- 2026-08-14: Yaren onayi ile musteri tarafinda test siparis akisi denendi: Beef Steak + ozel not sepete eklendi, cart belgelendi; checkout "Enable guest checkout" kapali oldugu icin musteri login duvarina takildi. Hesap acilmadi, sifre girilmedi, siparis tamamlanmadi. Devami icin toggle'in Yaren tarafindan acilmasi bekleniyor.
- 2026-08-14: .h2d import talimatlari `references/h2d-figma-import.md` olarak yazildi; import html.to.design eklentisini Figma'da elle calistirmayi gerektirdigi icin Claude tarafindan yapilamadi (eklenti MCP ile calistirilamiyor). Adimlar resmi dokumanla dogrulanamadi (site JS-render), eklenti bilgisine dayali.
