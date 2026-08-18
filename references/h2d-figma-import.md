# .h2d dosyalarini Figma'ya alma (html.to.design)

`references/menu-tiger-screens/` klasorundeki 7 MenuTiger .h2d dosyasi, html.to.design eklentisinin sifreli yakalama formati (alakasiz Behance UI referansi ayrildi: `references/ui-references/behance-cortex-ai-chatbot-saas.h2d`). Yalnizca eklentinin kendisi acabilir; bu yuzden import elle yapilir (MCP/otomasyonla yapilamiyor).

Adimlar (eklenti bilgisine dayali; resmi dokuman sitesi JS-render oldugu icin metinden dogrulanamadi, arayuzde kucuk farklar olabilir):

1. Figma'da QRPOC dosyasini ac (https://www.figma.com/design/PD58ocGJ0ogUJ0DSk3rxwn/QRPOC).
2. Resources (Shift+I) > Plugins > "html.to.design" ara; kurulu degilse Community'den calistir (divRIOTS'un eklentisi).
3. Eklenti penceresinde **Import** (dosyadan iceri alma) bolumune gec.
4. `references/menu-tiger-screens/` klasorundeki .h2d dosyalarini surukleyip birak (veya dosya seciciyle sec). Her dosya, yakalandigi andaki sayfayi katmanlariyla birlikte frame olarak olusturur.
5. Once tek dosyayla dene (`www_app_menutigr_com_portal_1440w_1470w_default.h2d`); sorunsuzsa kalanlari al.

Notlar:
- Behance yakalamasi (12 MB, artik `references/ui-references/` altinda) buyuk; import uzun surebilir.
- Yakalamalar 2026-05-18 tarihli; portalin bugunku halinden kucuk farklar olabilir (canli gezi 2026-08-14 goruntuleri `references/portal/` altinda).
- Ucretsiz planda import sayisi sinirli olabilir; eklenti uyarirsa en degerli uc dosya: portal (dashboard), portal_menus, menu-editor.
