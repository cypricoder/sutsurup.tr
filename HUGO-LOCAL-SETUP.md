# Hugo ile Yerel Önizleme (macOS)

Bu proje için küçük bir rehber: Hugo yüklü değilse nasıl kurup sitenizi yerel olarak çalıştırabileceğinizi ve alternatifleri anlatır.

1) Homebrew ile Hugo (en kolay)

Önce Homebrew yüklü değilse: https://brew.sh/ takip edin.

Terminal'de:

```bash
brew install hugo
```

Ardından sürümü kontrol edin (Extended olduğundan emin olun, SCSS için Extended gerekiyor):

```bash
hugo version
# Output örn: Hugo Static Site Generator v0.111.3-.../extended darwin/arm64
```

Çıktıda "extended" kelimesi varsa SCSS/asset pipeline çalışacaktır. Eğer "extended" yoksa Homebrew'den gelen paket eski/uyumsuz olabilir; bu durumda `brew uninstall hugo && brew install hugo` veya Docker seçeneğini kullanın.

2) Projeyi yerel sunucuda çalıştırma

Projeyi kök dizinde çalıştırmak için:

```bash
hugo server --minify --themesDir=./themes --baseURL=http://localhost:1313/
```

Tarayıcıda aşağıya gidin:
- Türkçe içerik anasayfası: http://localhost:1313/tr/
- Eklediğimiz örnekler: http://localhost:1313/tr/docs/interests/ ve http://localhost:1313/tr/docs/favorites/

3) Docker ile (Hugo yüklü değil veya extended yoksa)

Eğer Hugo kurmak istemiyorsanız Docker kullanabilirsiniz (image `klakegg/hugo:ext` extended sürümdür):

```bash
docker run --rm -it -p 1313:1313 -v "$PWD":/src klakegg/hugo:ext server --bind=0.0.0.0 --baseURL=http://localhost:1313 --minify --themesDir=./themes
```

4) Görseller ve placeholder'lar

Eklediğim içerik kartları `static/images/` altındaki resimlere işaret ediyor (ör. `album-okcomputer.jpg`, `inception.jpg`). Bu dosyalar henüz repoya eklenmedi.
İsterseniz şu iki seçenekten birini uygulayın:
- Kendi resimlerinizi `static/images/` dizinine koyun (önerilen isimlerle veya markdown içindeki path'leri güncelleyin).
- Hemen görmek için dış URL kullanın (ör. imgur/CDN linkleri) veya placeholder görseller ekleyin.

5) Hızlı sorun giderme
- Eğer stil değişiklikleri (SCSS) görünmüyorsa Hugo'nın extended sürümünü kullandığınızdan emin olun.
- Tema değişiklikleri gözükmüyorsa tarayıcı önbelleğini temizleyin veya sunucuyu yeniden başlatın.

6) Dağıtım/CI önerisi (kısa)

Netlify veya GitHub Pages ile otomatik deploy kurabilirsiniz. Tema `hugo-book` doc odaklı olduğu için Netlify ile uyumludur. CI pipeline içinde Hugo extended imajını kullanmanız SCSS için gerekir.

---

Eğer isterseniz şimdi şunları yapabilirim:
- (A) `static/images/` içine küçük placeholder görseller ekleyeyim ve commit'leyeyim.
- (B) İngilizce içerik kopyalarını (`content.en/docs/...`) otomatik oluşturayım.
- (C) `data/` + `layouts/partials/` ile kartları veri kaynaklı hale getireyim.

Hangi seçeneği tercih edersiniz? (A, B, C veya başka bir şey belirtin.)

