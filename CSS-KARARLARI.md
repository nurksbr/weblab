# CSS Kararları

## 1. Breakpoint Seçimi
- **Neden 640px ve 1024px seçtim?**
  Modern cihaz dağılımlarını temel alarak; 640px tabletleri (ve yatay telefonları), 1024px ise dizüstü ve masaüstü bilgisayarları hedeflemek için standart kabul gören (Tailwind vb. kütüphanelerle uyumlu) güvenli sınır değerlerdir.
- **İçeriğim bu noktalarda nasıl değişiyor?**
  Mobil boyutta (< 639px) içerik tamamen dikey yığınlanır (menü ve profil alt alta). 640px'te yan yana mizanpaja ve hizalı metinlere geçilir. 1024px üzerinde ise proje kartlarının geniş ekranı değerlendirip 3'lü tam sütun yapısına yayılması sağlanır.

## 2. Layout Tercihleri
- **Header için neden Flexbox seçtim?**
  Header içindeki logo ve navigasyon menüsünü yatay eksende pratik bir şekilde hizalamak, aralarına boşluk bırakmak (`space-between`) ve kolayca dikey/yatay yönlemler arasında (`flex-direction`) geçiş yapmak Grid'e kıyasla çok daha verimli olduğu için Flexbox tercih edilmiştir.
- **Proje kartları için neden Grid seçtim?**
  Proje listesi gibi aynı yapıya sahip, her iki eksende (satır ve sütun) kontrollü bir boşluk (gap) isteyen düzenlerde Grid matematikleri kusursuz bir denge sağlar. Flexbox'tan farklı olarak son satırdaki öğelerin uzayıp asimetri yaratmasını engeller.
- **`auto-fit` mi `auto-fill` mi kullandım, neden?**
  `auto-fit` kullandım. `minmax(280px, 1fr)` kuralıyla birlikte boşluk kalırsa o satırdaki hücrelerin büyüyerek var olan tüm esnek alanı doldurmasını sağlar. Bu sayede ekran geniş olsa bile sağda solda yetim boşluklar bırakmayan harika, duyarlı (responsive) bir görünüm elde edilir.

## 3. Design Tokens
- **Hangi renk paletini seçtim ve neden?**
  Dikkat çeken, modern bir his veren Mor/İndigo (Primary/Lavender/Slate) renk skalasını seçtim. Amacım düz siyah/beyazdan ziyade yüzey derinliğini belli eden modern bir tonlamayla (Surface Muted) profesyonel ve estetik (Premium) bir etki oluşturmaktı.
- **Spacing skalasını nasıl belirledim?**
  Evrensel ölçeklendirme prensibi olan "8 Noktalı (8px) Izgara Sistemi" üzerinden ilerledim (Örnek: `var(--spacing-2) = 0.5rem = 8px`, `var(--spacing-4) = 1rem = 16px`). Amacım görsel bütünlük sağlayarak bileşenler arasındaki tahmin edilebilir ahengi korumaktı.
- **Fluid typography için clamp değerlerini nasıl ayarladım?**
  Her font değişkenine `clamp(min, preferred vw, max)` yazarak minimum okunabilirlik sınırını (örneğin mobil için en az 1rem) ve masaüstü sınırını (max value) sabitleyerek fontları birer Media Query kurmadan tamamen akıcı şekilde büyür küçülür kurguladım.

## 4. Responsive Stratejiler
- **Mobile-first yaklaşımını nasıl uyguladım?**
  CSS dosyamdaki tüm küresel (`root`/`body`/`p`/`form`) temel değerleri doğrudan mobil ekrana (0-639px) göre tanımladım. Sadece ekran genişledikçe yatay olması gereken özel elemanlara `@media (min-width: ...)` blokları vasıtasıyla ekleme/aşım (.override) uygulayarak stil kodunu hafiflettim.
- **Hangi elemanlar breakpoint'lerde değişiyor?**
  Dikey yığında olan Header navigasyonu `min-width: 640px`'te yan yana geçer, Profil fotoğrafı ve metin formata uygun hizalanır (`flex-direction: row`). Masaüstünde (`1024px`) kapsayıcım ortalanarak sabit (`limit 1200px`) bir okuma alanı oluşturur.
- **Görsel boyutları nasıl yönettim?**
  Genel kural olarak kapsayıcı taşmalarını önlemek adına tüm imajlara `max-width: 100%; height: auto;` verdim. Sadece Proje kartlarındaki `.project-card img` gibi özel görsellere sabit `200px` height ve `object-fit: cover;` uygulayarak çözünürlük oranı/orijinal yapısı bozulmadan tutarlı kalmasını sağladım.
