<!--
Provenance: delivered verbatim by Yaren in chat on 2026-08-15.
Binding per its own §1. Do not edit without Yaren's approval.
-->

# QRPOC UI/UX Product Brief

## 1. Dokümanın statüsü

Bu doküman QRPOC UI/UX çalışmasının **güncel ve bağlayıcı ürün brief'idir**.

Bu aşamada ürün kapsamı kilitlidir.

Tasarım sırasında:

* yeni feature eklenmeyecek,
* yeni ürün amacı eklenmeyecek,
* yeni kullanıcı rolü eklenmeyecek,
* mevcut feature'lar varsayımla genişletilmeyecek,
* belirsiz bir alan yeni fonksiyon icat edilerek çözülmeyecek.

Bir konu bu brief'te veya mevcut üründe açık değilse, tasarımcı bunu **açık soru / implementation dependency** olarak işaretlemelidir. Sessizce ürün kararı vermemelidir.

---

# 2. Source of truth ve öncelik sırası

Kaynaklar birbiriyle çelişirse şu sıra geçerlidir:

1. **Bu brief**
2. **Bu brief'i oluşturan kilitlenmiş güncel ürün kararları**
3. **Mevcut backend, database ve çalışan güncel ürün davranışı**
4. **MenuTiger referans analizi**, yalnızca UX pattern ve görsel sistem referansı olarak
5. **`qrpoc-atlas.html`**, yalnızca eski / mevcut prototype kodunun teknik envanteri olarak
6. Daha eski analiz ve karar notları

Eski dokümanlardaki bir karar bu brief ile çelişiyorsa **eski karar geçersizdir**.

`qrpoc-atlas.html` hedef ürün requirement dokümanı değildir. Mevcut / eski prototipin ne yaptığını anlatır.

---

# 3. Ürünün doğru zihinsel modeli

QRPOC tek bir dashboard değildir.

"Admin panel + müşteri menüsü" şeklinde iki parçalı bir ürün de değildir.

QRPOC, aynı restoran sistemini kullanan fakat farklı görevler için tasarlanmış birkaç uygulamadan oluşan bir **ürün ekosistemidir**.

```text
QRPOC ECOSYSTEM

Customer App
Waiter App
Kitchen App
Service Manager App
Admin / Operations Portal
```

Bu uygulamalar aynı sistemin parçalarıdır ancak aynı UI'ın role göre gizlenmiş varyasyonları değildir.

Her birinin:

* farklı kullanıcısı,
* farklı point of entry'si,
* farklı ana görevi,
* farklı bilgi ihtiyacı,
* farklı kullanım bağlamı,
* gerektiğinde farklı navigation ve layout yapısı

vardır.

**Roller yalnızca access level değildir. Farklı görevler için farklı ürün yüzeyleridir.**

Örneğin Admin Portal'ın sidebar yapısının Kitchen App'e taşınması yanlış olur.

---

# 4. Kullanıcı hiyerarşisi yok

Ürün için tek bir "primary user" tanımlanmamalıdır.

İki taraf da ürünün başarısı için kritiktir:

| Taraf                 | Temel ihtiyaç                                        |
| --------------------- | ---------------------------------------------------- |
| Customer              | Düşük friction, anlaşılır menü, hızlı sipariş, güven |
| Restaurant operations | Hız, görünürlük, kontrol, operasyonel netlik         |

İşletme ürünü satın alan veya yapılandıran taraf olabilir.
Bu, müşteri deneyimini ikincil yapmaz.

Customer App kötü çalışırsa işletme tarafındaki ürün değeri de zarar görür.

Bu nedenle hedef:

**iki tarafı birlikte optimize eden bir ekosistem kurmaktır.**

---

# 5. Ortak tasarım ilkesi

Ürünün en önemli UI/UX ilkesi:

> **Her yüzey tek bir ana işi mümkün olduğunca iyi yapmalı.**

Sistemin tamamı karmaşık olabilir.
Her uygulamanın karmaşık olması gerekmez.

Karmaşıklık tüm rollere dağıtılmamalıdır.

Bir kullanıcıya yalnızca kendi görevini yerine getirmesi için gerekli bilgi ve aksiyonlar gösterilmelidir.

Bir role ait olmayan bilgi "belki yararlı olur" gerekçesiyle o yüzeye taşınmamalıdır.

---

# 6. Canonical rol ve uygulama isimleri

Brief boyunca aşağıdaki terminoloji kullanılacaktır:

| Ürün yüzeyi                   | Kullanıcı                        |
| ----------------------------- | -------------------------------- |
| **Customer App**              | Customer / Restaurant Guest      |
| **Waiter App**                | Waiter / Garson                  |
| **Kitchen App**               | Kitchen Staff / Mutfak Personeli |
| **Service Manager App**       | Service Manager / Şef Garson     |
| **Admin / Operations Portal** | Admin / İşletmeci                |

"Service Manager" ve "Şef Garson" bu brief bağlamında aynı rolü ifade eder.

---

# 7. Terminoloji

Bazı kavramlar özellikle birbirinden ayrılmalıdır.

### Check

`Check`, masa hesabını / hesabın operasyonel kaydını ifade eder.
Bu kavram ödeme sağlayıcısı anlamına gelmez.

### Checkout

Customer tarafında sipariş / hesap akışındaki ilerleme aksiyonudur.
Gerçek payment processing olduğu anlamına gelmez.

### Payment

Gerçek finansal ödeme işlemi.
**Mevcut MVP kapsamında gerçek payment processor yoktur.**

### Request / CTA

Restoran tarafından Customer App için yapılandırılan servis talebi aksiyonudur.

Örnek:

* garson çağır,
* hesap iste,
* soya sosu iste,
* zencefil iste.

Bunlar genel navigation veya rastgele shortcut değildir.

### Guest session

Login olmadan Customer App kullanan kişi için server tarafında tutulan gerçek session'dır.
Geçici mock state anlamına gelmez.

---

# 8. Customer App

## Kullanıcı

Restoran müşterisi.

## Temel amaç

Müşterinin mümkün olan en az sürtünmeyle:

```text
menu
→ item
→ customize
→ add
→ order
```

akışını tamamlamasıdır.

Customer App bir restaurant management aracı değildir.

---

## Entry ve onboarding

Customer App'in tek bir zorunlu giriş şekli varsayılmamalıdır.

QR önemli bir point of entry'dir ve masa bağlamını taşıyabilir.

Ancak ürün modeli:

```text
entry
→ optional login / onboarding context
→ menu
```

şeklindedir.

Customer mümkün olduğunca hızlı biçimde düz menüye ulaşmalıdır.

---

## Authentication

Customer sipariş vermek için login olmak zorunda değildir.

İki geçerli kullanım şekli vardır:

```text
Guest
→ guest session
→ full ordering flow
```

ve

```text
Google Auth
→ authenticated customer session
→ ordering flow
```

Google Auth opsiyoneldir.
Login, ordering'in önünde zorunlu bir gate olarak kullanılmamalıdır.

Guest session server tarafında loglanır ve normal ürün state'inin parçasıdır.

---

## QR context

QR ile giriş yapıldığında mevcut sistemin sağladığı restoran / masa bağlamı korunmalıdır.

Kullanıcıya sistemin zaten bildiği bilgi tekrar sorulmamalıdır.

QR bir dekoratif bağlantı değil, mevcut restoran bağlamına giriş mekanizmasıdır.

---

## Menü

Müşteri menüye ulaştığında ana içerik iki şeydir:

1. menu items
2. restaurant-configured CTA / request actions

Menü:

* hızlı taranmalı,
* fiyatları açık göstermeli,
* item'a geçişi kolaylaştırmalı,
* restoran içeriğini ön plana çıkarmalı,
* navigation ile içeriği boğmamalıdır.

MenuTiger Customer App burada güçlü bir behavioral reference'tır.
Ancak görsel olarak kopyalanmayacaktır.

---

## Item interaction

Item açıldığında kullanıcı ilgili ürün üzerinde mevcut kapsamın desteklediği:

* seçme,
* ekleme,
* çıkarma,
* customize etme,
* sepete / siparişe ekleme

işlemlerini yapabilmelidir.

Bu ekranın görevi yalnızca seçilen ürün üzerindeki kararı tamamlamaktır.
Ürün dışı bilgi veya gereksiz navigation eklenmemelidir.

---

## Restaurant-configured CTA'lar

Restoran Customer App'te hangi servis talebi CTA'larının görüneceğini belirleyebilir.

Örnek kullanım:

```text
Sushi restaurant
→ Soy sauce
→ Pickled ginger
→ Call waiter
→ Request check
```

Başka bir restoran başka talepler tanımlayabilir.

Tasarım:

* dinamik sayıda CTA'yı desteklemeli,
* CTA isimlerini hardcode etmemeli,
* ekranı CTA duvarına çevirmemeli,
* menu items ile request actions arasındaki farkı açık tutmalıdır.

CTA sistemi yeni bir feature olarak genişletilmeyecektir. Yalnız mevcut configurable request modelinin UI'ı tasarlanacaktır.

---

# 9. Kitchen App

## Kullanıcı

Kitchen Staff.

## Kullanım bağlamı

Kitchen App tablet üzerinde sürekli açık kalabilecek kadar sade ve operasyonel olmalıdır.

Bu kullanıcı sistem içinde araştırma yapmaz.
Siparişi görür ve ilerletir.

---

## Görmesi gereken temel bilgi

Kitchen App'in çekirdeği:

```text
TABLE NUMBER
ORDER DETAILS
STATUS
```

Bunun dışındaki admin / analytics / customer / service-management bilgileri burada bulunmamalıdır.

---

## Ana ekran

Temel layout üç kolondur:

```text
PENDING
PREPARING
READY
```

İsimler mevcut sistemdeki canonical order-item status isimleriyle eşleştirilmelidir.
Tasarım kendi status modelini yaratmamalıdır.

Bir order / item üzerindeki temel interaction, mevcut akışa uygun biçimde onu bir sonraki status'a taşımaktır.

Interaction:

* hızlı,
* büyük touch target'lı,
* kolay taranabilir,
* yanlışlık riskini düşük tutan,
* yoğun servis sırasında kullanılabilir

olmalıdır.

Kitchen App'e gereksiz dashboard, chart, analytics veya configuration eklenmemelidir.

---

# 10. Waiter App

## Kullanıcı

Waiter / Garson.

## Ana görev

Garsonun servis sırasında ihtiyacı olan üç ana domain:

```text
TABLE
ORDER
CHECK
```

Waiter App bu üç domain etrafında kurulmalıdır.

Garson:

* masayı bulabilmeli,
* masanın order bilgisini anlayabilmeli,
* check durumunu görebilmeli,
* mevcut garson aksiyonlarını hızlıca gerçekleştirebilmelidir.

Admin configuration burada gösterilmemelidir.

---

## Floor plan

İki boyutlu floor-plan gelecekte değerlendirilebilir.
**Mevcut scope'un parçası değildir.**

MVP UI floor-plan gerektiriyormuş gibi tasarlanmamalıdır.

---

# 11. Service Manager App

## Kullanıcı

Service Manager / Şef Garson.

## Ana görev

Servis operasyonunun tamamındaki mevcut durumu ve müdahale gerektiren noktaları görmek.

Service Manager App:

```text
Waiter-level service information
+
table request overview
+
all relevant checks
+
pending requests
```

bilgilerini bir araya getirir.

Şef garson, garsonun gördüğü temel servis bağlamını görebilir ancak ek olarak operasyonun tamamındaki bekleyen servis taleplerini izleyebilir.

Bu yüzey analytics portalı değildir.

Ana soru:

> **Şu anda serviste neye dikkat etmem veya müdahale etmem gerekiyor?**

Henüz ürün kapsamına açıkça eklenmemiş yeni alert türleri bu tasarıma dahil edilmemelidir.

---

# 12. Admin / Operations Portal

## Kullanıcı

Restaurant operator / Admin.

Bu ürün yüzeyi için back office gerçekten ana çalışma alanıdır.

Bu kural yalnızca Admin Portal için geçerlidir.
Kitchen, Waiter, Service Manager ve Customer uygulamalarının "primary surface"ı Admin Portal değildir.

---

## Admin kapsamı

Mevcut ürün kapsamındaki ağır configuration ve management işleri burada bulunur.

Bunlar arasında:

* menu management,
* QR / table configuration,
* analytics,
* inventory / stock,
* procurement,
* recipe configuration,
* mevcut admin-level operational settings,
* mevcut integrations,
* POS integration work,
* mevcut SAP / vertical integration alanları

yer alabilir.

Bu liste yeni admin feature üretmek için kullanılmamalıdır.
Yalnızca üründe zaten bulunan veya kilitli kapsamda yer alan modüller tasarlanacaktır.

---

## Portal karakteri

Admin Portal:

* sakin,
* ferah,
* öngörülebilir,
* düşük görsel gürültülü,
* tekrar eden patternleri olan,
* fazla özellik taşısa bile taranabilir

olmalıdır.

Amaç "minimal ürün" yapmak değildir.
Amaç **yüksek capability + kontrollü density** kombinasyonudur.

---

# 13. MenuTiger'ın rolü

MenuTiger ürün spesifikasyonu değildir.
Tasarım referansıdır.

## Customer tarafında

Özellikle şu konularda güçlü referanstır:

* menu browsing,
* item cards,
* item detail,
* cart,
* request interaction.

## Admin tarafında

İyi bir başlangıç noktasıdır:

* layout logic,
* spacing rhythm,
* list patterns,
* forms,
* editors,
* information hierarchy,
* density discipline.

Ancak Admin Portal için hedef MenuTiger seviyesinde durmak değildir.
**Daha iyi çözümler üretilebilir ve beklenir.**

---

## MenuTiger'dan alınabilecekler

```text
structure
interaction grammar
spacing rhythm
component behaviour
information hierarchy
density discipline
```

## MenuTiger'dan kopyalanmayacaklar

```text
brand
logo
color palette
illustration language
icons
copy
commercial upsell mechanics
exact layouts
```

Referansın kendisinde de copy ve consistency hataları vardır.

Bu nedenle:

> **Reference is evidence, not authority.**

---

# 14. Visual design direction

## Neutral-first

Ana yüzeylerin çoğu nötr olmalıdır.

Renk dekorasyon için değil, görev için kullanılmalıdır.

Örnek rol dağılımı:

| Rol            | Kullanım                       |
| -------------- | ------------------------------ |
| Primary accent | action, selected, active       |
| Success        | başarılı / tamamlanmış durum   |
| Warning        | dikkat gerektiren mevcut durum |
| Destructive    | delete / irreversible action   |
| Neutrals       | yüzeyler, gövde, ikincil bilgi |

Primary brand color henüz MenuTiger teal'i olarak kabul edilmemelidir.

---

## Ferahlık

Ferahlık boş ekrana dekorasyon eklemekle değil, kontrollü information density ile sağlanmalıdır.

Bir ekranın görevi küçükse kalan alanın doldurulması gerekmez.

---

## Predictability

Tekrarlanan görevlerde tekrar eden component ve interaction patternleri kullanılmalıdır.

"Clever" interaction yerine kolay öğrenilebilir, tutarlı davranış tercih edilmelidir.

---

## App-specific density

Aynı design system, aynı layout anlamına gelmez.

Örneğin:

| Surface         | Karakter                                    |
| --------------- | ------------------------------------------- |
| Customer        | mobile-oriented, visual, low friction       |
| Kitchen         | tablet-oriented, operational, large targets |
| Waiter          | fast scanning, touch-first                  |
| Service Manager | operational overview                        |
| Admin           | detailed, structured, spacious              |

---

# 15. Branding

QRPOC'un product brand'i MenuTiger'dan farklıdır.

İki ayrı kavram karıştırılmamalıdır:

```text
QRPOC PRODUCT BRAND
```

ve

```text
RESTAURANT CUSTOMER-FACING BRANDING
```

MenuTiger'ın white-label özelliğe sahip olması QRPOC'un MenuTiger görsel kimliğini takip etmesi gerektiği anlamına gelmez.

Mevcut scope dışında yeni white-label feature tasarlanmayacaktır.

---

# 16. Dashboard

Dashboard tasarlanabilir.

Ancak dashboard stat-card branding yönü henüz nihai olarak kilitli değildir.

Bu nedenle:

* hierarchy,
* layout,
* component structure,
* information presentation

çözülebilir.

Güçlü bir branding fikri oluşursa kullanılabilir.
Ancak dashboard branding kararı ürünün geri kalan tasarımını bloke etmemelidir.

---

# 17. Multilingual content model

Ürün iki dile hardcode edilmemelidir.

## MVP

Başlangıçta:

```text
Turkish
English
```

desteklenir.

## Ürün modeli

Content localization modeli:

```text
1..n enabled languages
```

olmalıdır.

En az bir content language bulunur.

Kullanıcı sisteme yeni bir dil ekleyebilir ve ilgili customer-facing içeriği o dile bağlayabilir.

Örneğin:

```text
Turkish
Menu item name: Mercimek Çorbası

English
Menu item name: Lentil Soup

German
Menu item name: Linsensuppe
```

Burada German örneği yeni bir product feature değildir. Sistemin arbitrary-language modelini açıklamak içindir.

---

## Sistem ne sağlamalı?

Gerekli olan:

* dil ekleyebilmek,
* seçili dile content bağlayabilmek,
* karakterleri doğru saklamak,
* karakterleri doğru render etmek.

Gerekli olmayan:

* automatic translation,
* AI translation,
* grammar correction,
* translation service,
* language-specific content generation.

---

## Editor UI

TR ve EN iki sabit kolon olarak hardcode edilmemelidir.

Dil alanları dinamik olmalıdır.

Şu interaction patternlerinden hangisinin kullanılacağı henüz kilitli değildir:

* selector,
* tabs,
* locale switcher,
* Localize section,
* başka ölçeklenebilir bir model.

Tasarımcı en temiz `1..n languages` çözümünü önermelidir.

Ancak **Localize tab zorunlu değildir ve yasak da değildir**.
Karar yalnızca ölçeklenebilirlik ve kullanım kolaylığı üzerinden verilmelidir.

---

# 18. Backend ve state gerçekliği

Ürün yalnız front-end prototype değildir.

Güncel sistemde:

```text
Backend: exists
Database: exists
Server-side state: exists
Auth: exists
External integrations: exist
```

Backend ürünün tamamı için yazılmıştır.

UI tasarımı typed mock fixture üzerine kurulmuş varsayımsal bir demo gibi ele alınmamalıdır.

Mevcut development ortamında gerçek database kayıtları ve restoran verisi bulunmaktadır.

Mevcut kayıt sayısı ürün kapasitesi veya IA kararı olarak yorumlanmamalıdır.

---

## State tasarımı

UI gerçek server state'i doğru göstermelidir.

Gereken yerlerde mevcut sistem davranışına karşılık gelen:

* loading,
* empty,
* error,
* pending,
* active,
* completed,
* disabled

gibi state'ler tasarlanmalıdır.

Yeni workflow veya status ismi icat edilmemelidir.
Canonical state isimleri backend ile eşleştirilmelidir.

---

# 19. Payment ve POS

## Real payment

MVP'de gerçek payment processor yoktur.

Bu nedenle tasarlanmayacaklar:

* card payment UI,
* Stripe-style payment flow,
* saved cards,
* fake processor confirmation,
* payment success experience pretending money moved.

UI, sistemde gerçek ödeme yokken ödeme gerçekleşmiş izlenimi vermemelidir.

---

## POS

POS integration MVP kapsamındadır.

POS entegrasyonu çalışılacaktır.

Bu nedenle mevcut POS bağlantısı için gerekli configuration ve operational feedback UI'ı desteklenebilir.

Yeni POS ürün özellikleri veya entegrasyon sağlayıcıları tasarlanmayacaktır.

---

# 20. External / vertical integrations

External API entegrasyonları ürünün gerçek parçasıdır.

SAP entegrasyonu mevcut örneklerden biridir ve database / operasyon verisi almak için kullanılmaktadır.

Başka vertical integrations ürünün gelişiminde gerekebilir.

Ancak mevcut UI/UX scope'unda:

* varsayımsal yeni entegrasyonlar eklenmeyecek,
* yeni integration marketplace tasarlanmayacak,
* mevcut olmayan provider listeleri oluşturulmayacaktır.

Tasarım yalnız mevcut ve açıkça kapsamda olan entegrasyon ihtiyaçlarını destekler.

---

# 21. Commercial gating

Bu prototype / MVP UI kapsamının dışında:

* upsell,
* plan comparison,
* paid gating,
* feature lock,
* upgrade CTA,
* trial wall

bulunur.

MenuTiger'daki ticari gating patternleri QRPOC için referans alınmayacaktır.

Kitchen / KDS için trial experience şu anda tasarlanmayacaktır.
İleride demo için ayrıca talep edilirse bu ayrı scope olarak ele alınır.

---

# 22. Teknik UI yönü

Mevcut frontend yönü:

```text
Next.js
TypeScript
Tailwind
shadcn/ui
```

Şimdilik default teknoloji seti budur.

Menu veya başka özel bir yüzey için farklı bir UI yaklaşımı ancak mevcut stack gerçek bir ürün gereksinimini karşılamıyorsa değerlendirilmelidir.

Yeni teknoloji kullanmak kendi başına hedef değildir.

---

# 23. Shared design system

Ürün ailesi ortak bir visual ve interaction vocabulary paylaşmalıdır.

Ortaklaştırılması beklenenler:

* typography,
* spacing,
* semantic colors,
* radius,
* buttons,
* form controls,
* badges,
* feedback states,
* icons,
* accessibility rules.

Ortaklaştırılması zorunlu olmayanlar:

* page shell,
* navigation model,
* information density,
* card layout,
* content hierarchy.

Örneğin Kitchen App ve Admin Portal aynı component library'yi kullanabilir ama aynı sidebar layout'unu kullanmak zorunda değildir.

---

# 24. Admin Portal component grammar

MenuTiger'dan özellikle tekrar kullanılabilecek interaction ailesi:

### Page shell

```text
navigation
page context
primary actions
main work surface
```

### List

```text
filters / search
primary action
rows / cards
```

### Inline editor

```text
context
editable content
save
```

Edit işlemi için otomatik olarak modal tercih edilmemelidir.

### Master-detail

```text
selection
→ selected object
```

### Repeating field groups

Örnek:

* prices,
* recipe ingredients,
* options,
* hours.

### Toggle / settings rows

Benzer configuration problemleri benzer componentlerle çözülmelidir.

Yeni ekran geldiğinde ilk soru:

> **Bunu mevcut patternlerden biri zaten çözüyor mu?**

olmalıdır.

---

# 25. Tasarım ve geliştirme sırası

Aşağıdaki sıra **ürün hiyerarşisi değildir**.
Bu yalnızca işi kontrollü ve doğrulanabilir şekilde ilerletmek için önerilen çalışma sırasıdır.

Her adım tamamlanmadan tüm ekosistemi high-fidelity olarak tasarlamaya çalışmayın.

---

## Step 0. Scope map

İlk artifact:

```text
QRPOC APP MAP
```

Beş uygulama için yalnızca şunları gösterin:

| App             | Entry                              | Primary job           | Main objects              | Explicitly not responsible for |
| --------------- | ---------------------------------- | --------------------- | ------------------------- | ------------------------------ |
| Customer        | mevcut customer entry / QR context | browse and order      | menu, item, request       | management                     |
| Kitchen         | staff session                      | progress kitchen work | table, order/item, status | analytics/config               |
| Waiter          | staff session                      | serve tables          | table, order, check       | admin config                   |
| Service Manager | staff session                      | service overview      | tables, requests, checks  | back-office config             |
| Admin           | admin session                      | configure and operate | management domains        | frontline task UI              |

Bu çalışma scope'u değiştirmez.
Yalnızca sınırları görünür hale getirir.

---

## Step 1. Domain ve state vocabulary

UI çizmeden önce ortak domain isimlerini ve mevcut state'leri doğrulayın.

Özellikle:

```text
table
order
order item
check
request
menu item
guest session
```

ve mevcut status'lar.

Aynı obje farklı uygulamalarda farklı isimlerle anlatılmamalıdır.

---

## Step 2. Shared visual foundation

Tanımlayın:

* typography,
* spacing,
* neutral surfaces,
* semantic color roles,
* radius,
* controls,
* state feedback,
* icon language.

Bu aşamada bütün uygulamalar için tek shell tasarlanmayacaktır.

---

## Step 3. Customer Menu + Admin Menu Editor vertical slice

İlk tam domain olarak **Menu** ele alınmalıdır.

İki taraf birlikte tasarlanır:

```text
Admin Menu Editor
↓
Customer Menu
```

Customer tarafında:

```text
browse
→ item
→ customize
→ add
→ order
```

Admin tarafında mevcut kapsamın izin verdiği:

```text
menu structure
item content
item configuration
languages
```

çözülür.

Amaç:

> Admin'de değiştirilen şey ile Customer'da görülen şey arasında açık bir zihinsel bağlantı kurmak.

---

## Step 4. Customer Order → Kitchen

Sonra siparişin mutfağa ulaştığı mevcut zincir çözülür.

```text
customer order
→ kitchen receives
→ pending
→ preparing
→ ready
```

Kitchen UI bu aşamada sade üç kolonlu çalışma yüzeyi olarak tamamlanır.

---

## Step 5. Waiter

Kitchen sonrası garsonun gerçek operasyon zinciri çözülür.

Ana domain:

```text
table
order
check
```

Garson için başka app'lere ait yönetim araçları eklenmez.

---

## Step 6. Requests + Service Manager

Customer'ın configurable CTA / request sistemi ile Service Manager'ın request overview'i aynı vertical slice içinde kontrol edilir.

```text
Customer action
→ server request
→ Service Manager visibility
```

İki taraf aynı domain event'ini farklı ihtiyaçlarla görür.

---

## Step 7. Admin operational modules

Ana frontline akışlar oturduktan sonra Admin Portal'ın mevcut ağır modülleri çözülür.

Örneğin mevcut scope dahilinde:

```text
QR / tables
analytics
inventory
procurement
recipes
integrations
```

Yeni interaction grammar yalnız mevcut component sistemi yetersizse oluşturulur.

---

## Step 8. Multilingual pass

Bütün customer-facing editable content `1..n language` modeli açısından kontrol edilir.

Test:

> Üçüncü bir dil eklendiğinde UI yapısal olarak bozuluyor mu?

Bozuluyorsa çözüm ölçeklenebilir değildir.

---

## Step 9. State pass

Her ekran yalnız happy path ile değerlendirilmemelidir.

Mevcut backend state'lerinin gerekli olanları:

```text
loading
empty
error
pending
active
completed
disabled
```

tutarlı şekilde tasarlanmalıdır.

---

## Step 10. Cross-app consistency pass

Aynı domain objesinin beş uygulamadaki temsili karşılaştırılır.

Örneğin `order`:

| Surface         | Order'ın anlamı                 |
| --------------- | ------------------------------- |
| Customer        | my order                        |
| Kitchen         | work to prepare                 |
| Waiter          | table service                   |
| Service Manager | operational state               |
| Admin           | operational / analytical record |

Bilgi miktarı değişebilir.
Domain anlamı ve status mantığı çelişmemelidir.

---

# 26. Her ekran için acceptance checklist

Bir ekran bitmiş kabul edilmeden önce aşağıdakiler kontrol edilir.

### Purpose

* Tek ana görev açık mı?
* Bu görev gerçekten bu role ait mi?

### Information hierarchy

* İlk görülmesi gereken bilgi açık mı?
* Secondary bilgi gerçekten secondary mi?

### Scope

* Yeni feature eklenmiş mi?
* Eski prototype'tan yanlışlıkla product requirement taşınmış mı?

### Density

* Boş alan yalnız dolsun diye içerik eklenmiş mi?
* Gereksiz card / container var mı?

### Actions

* Primary action belirgin mi?
* Aynı seviyede gereğinden fazla CTA var mı?

### Roles

* Başka uygulamaya ait yönetim fonksiyonu buraya sızmış mı?

### State

* Kullanıcı sistemin ne durumda olduğunu anlayabiliyor mu?
* UI backend'de olmayan state yaratıyor mu?

### Multilingual

* Dil sayısı hardcode edilmiş mi?
* Yeni locale eklendiğinde structure bozuluyor mu?

### Consistency

* Aynı problem başka yerde zaten çözülmüş mü?
* Yeni component gerçekten gerekli mi?

### Customer friction

Customer-facing ekran ise:

* Login gereksiz yere zorunlu hale gelmiş mi?
* Menüye ulaşma veya order verme gereksiz adımlarla uzamış mı?

---

# 27. Explicitly out of scope

Aşağıdakiler bu aşamada tasarlanmayacaktır:

* yeni feature,
* yeni ürün amacı,
* yeni rol,
* zorunlu customer login,
* customer ordering için auth wall,
* gerçek payment processor flow,
* saved cards,
* yeni payment provider,
* yeni POS provider,
* yeni vertical integration fikri,
* integration marketplace,
* upsell,
* plan gating,
* KDS trial flow,
* iki boyutlu waiter floor plan,
* automatic translation,
* AI translation,
* TR / EN hardcoded two-column editor,
* yeni alert türleri,
* sırf dashboard'u doldurmak için yeni KPI,
* bütün rolleri aynı dashboard shell'ine sokmak,
* MenuTiger'ın birebir kopyası.

---

# 28. Tasarımcı karar verirken kullanılacak protokol

Bir tasarım kararı belirsizse şu sırayla ilerleyin:

### 1

Bu brief açıkça cevaplıyor mu?
Evetse brief'i uygulayın.

### 2

Mevcut backend / çalışan ürün davranışı cevaplıyor mu?
Evetse bunu görünür ve kullanılabilir hale getirin.

### 3

MenuTiger aynı UX problemini çözüyor mu?
Evetse patterni inceleyin, davranışı öğrenin, QRPOC'a uygun hale getirin.

### 4

Yalnız eski prototype / atlas'ta mı var?
Bunu otomatik olarak hedef requirement kabul etmeyin.

### 5

Hâlâ belirsiz mi?
Yeni feature veya varsayım üretmeyin.
Soruyu açık bırakın ve karar isteyin.

---

# 29. Kalite hedefi

QRPOC için hedef yalnızca "modern" veya "güzel" görünmek değildir.

Ürün ailesi şu niteliklere sahip olmalıdır:

> **calm, clear, refined, operationally obvious**

Admin:

> **high capability, low visual noise**

Customer:

> **low friction, clear choice, confidence**

Kitchen / Waiter:

> **immediate state recognition, fast action**

Service Manager:

> **clear overview, obvious intervention points**

Bunlar aynı design system'in farklı görevlerdeki ifadeleridir.

---

# 30. Ürünün tek sayfalık özeti

```text
                    QRPOC
        shared backend + shared domain system
                         │
        ┌────────────────┼─────────────────┐
        │                │                 │
    Customer          Kitchen           Waiter
        │                │                 │
 menu + CTA       table + order      table + order
 item              + status            + check
 customize
 order
        │
        └────────────────┬─────────────────┘
                         │
                 Service Manager
                         │
              service overview
              requests + checks
                         │
                         │
                 Admin / Operations
                         │
             configure + manage
             analyse + integrate
```

Ana tasarım ilkesi:

> **Ekosistem karmaşık olabilir. Her yüzey olmak zorunda değildir.**

Ve kapsam ilkesi:

> **Var olan ürünü daha anlaşılır hale getir. Yeni bir ürün icat etme.**
