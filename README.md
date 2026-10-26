# Smart Editor

Premiere Pro için Smart Editor paneli. Bu depoda kaynak kod yok, yalnızca imzalı kurulum paketleri var.

## İndir

**[SmartEditor_0.1.4.dmg](https://github.com/menestopal/SmartEditor-releases/releases/download/v0.1.4/SmartEditor_0.1.4.dmg)** (sürüm 0.1.4)

Önceki sürümler: [Sürümler](https://github.com/menestopal/SmartEditor-releases/releases). Sürüm sayfasında yalnızca `.dmg` dosyasını indirin;
"Source code" arşivlerini GitHub kendiliğinden ekler, kurulum için gerekmez.

## Smart Editor 0.1.4 — Kurulum

Smart Editor, Premiere Pro için bir panel ve onu bilgisayarınızda çalıştıran
yerel bir motordur. Kurulumun kendisi bir dakika sürer; eksik araçların
indirilmesi internet hızınıza bağlıdır.

Gereksinimler: macOS 12 ve üstü, Premiere Pro 25.0 ve üstü (26.3'te doğrulandı).
Windows desteklenmez.

### 1. Diski açın

İndirdiğiniz `SmartEditor_0.1.4.dmg` dosyasını çift tıklayın. Finder'da
**Smart Editor 0.1.4** adlı bir disk açılır, içinde üç dosya vardır:

| | |
|---|---|
| `Kur.command` | Kurulum: paketi yerine açar, Dock uygulamasını oluşturur, eksik araçları söyler |
| `KURULUM.html` | Kurulum talimatları — bu metin |
| `SmartEditor_0.1.4.zxp` | Premiere Pro eklentisi: panel ve motor bir arada, imzalı. Elle açmanız gerekmez |

### 2. Kurun

`Kur.command` dosyasını çift tıklayın. Terminal açılır, ne yaptığını yazar ve
sonunda eksik araçların listesini verir.

macOS ilk seferde "Apple doğrulayamadı" ya da "tanımlanamayan geliştirici"
diyerek dosyayı açmayabilir. Bu beklenen bir durum: dosya App Store'dan değil,
doğrudan Fokus Plus'tan geliyor. İki yol var:

- Uyarıda **Bitti**'ye basın. **Sistem Ayarları › Gizlilik ve Güvenlik**'i açın,
  sayfanın altındaki "Kur.command engellendi" satırında **Yine de Aç**'a basın,
  parolanızı girin, çıkan pencerede **Aç**'a basın.
- Ya da Terminal'i açın (**Uygulamalar › İzlenceler › Terminal**), `Kur.command`
  dosyasını Terminal penceresine sürükleyip bırakın ve Enter'a basın.

Kurulum iki yere yazar, başka hiçbir yere dokunmaz:

```
~/Library/Application Support/Adobe/CEP/extensions/net.fokusplus.smarteditor/   eklenti
~/Applications/Smart Editor.app                                                 Dock başlatıcısı
```

Kurulum bitince diski çıkarabilirsiniz (Finder'da diskin yanındaki ⏏ işareti);
`.dmg` dosyasını silebilirsiniz.

### 3. Araçlar

Motor dört komut satırı aracı kullanır; hepsi Homebrew'dan gelir. Kurulum
betiği hangilerinin eksik olduğunu yazar ve komutu verir; aynı şeyi panelin
**Ayarlar › Kurulum** bölümü de yapar — orada **Kur** düğmesi `brew install`i
sizin yerinize çalıştırır.

Homebrew yoksa önce onu kurun (Terminal'de, parola sorar):

```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

Sonra araçlar:

```bash
brew install node ffmpeg yt-dlp whisper-cpp deno
```

| Araç | Ne için |
|---|---|
| `node` | Motor bu çalışma zamanında koşar (20 ve üstü) |
| `ffmpeg` | Ses birleştirme, ölçüm, kare çıkarma |
| `yt-dlp` | YouTube, Vimeo, TikTok, X, Facebook, Instagram indirmeleri |
| `whisper-cpp` | Kayıttan kelime zamanları — hizalama ve altyazı |
| `deno` | İsteğe bağlı: YouTube'un oynatıcı bulmacaları için; yoksa node kullanılır |

### 4. Premiere'i yeniden başlatın

**Window › Extensions › Smart Editor.** Panel açılınca motoru kendisi başlatır.

### 5. Panelde bir kez

**Ayarlar › Kurulum** — listedeki her satırın yanında durum ve gerekli komut
vardır. Kırmızı olanları sırayla kapatın:

1. **Whisper modeli** — Ayarlar › Seslendirme › **İndir** (large-v3-turbo, 1,6 GB).
2. **ElevenLabs anahtarı** — Ayarlar › Anahtarlar.
3. İsteğe bağlı: **Tarayıcı kimliği** (TLS parmak izine bakan siteler),
   **Playwright** (Envato / Artlist), **görsel model sunucusu** (kadraj tespiti —
   LM Studio ya da Ollama).

**Ayarlar › Premiere › Şablon seç** — Premiere bir `.prproj` dosyasını
sıfırdan üretemez. Bir kez boş bir proje kaydedin ve burada gösterin; sonraki
her proje onun kopyasıdır.

### 6. Günlük kullanım

Dock'a **Smart Editor** uygulamasını koyun (Finder › Uygulamalar klasörünüz,
`~/Applications`). Premiere'in kendi simgesinden açmayın: Premiere'in başlangıç
ekranı eklenti yüklemez, proje açılmadan panel gelmez. Smart Editor başlatıcısı
klasörü hazırlar, projeyi şablondan kopyalar ve Premiere'i o projeyle açar.

### Güncelleme

Yeni sürümün `.dmg` dosyasını indirip aynı adımları izleyin. `Kur.command` eski
sürümün üzerine kurar; ayarlarınız, anahtarlarınız ve indirdiğiniz modeller
(`~/Library/Application Support/SmartEditor`) olduğu gibi kalır. Premiere
açıksa kurulumdan sonra yeniden başlatın.

### Kaldırma

```bash
rm -rf ~/Library/Application\ Support/Adobe/CEP/extensions/net.fokusplus.smarteditor
rm -rf ~/Applications/Smart\ Editor.app
rm -rf ~/Library/Application\ Support/SmartEditor      # ayarlar, anahtarlar, modeller, günlük
```

### Sorun olursa

- Panel listede yok → Premiere'i tamamen kapatıp açın; `Kur.command` çıktısında
  "Panel kuruldu" satırı var mı bakın.
- Panel açılıyor ama "motor başlatılamadı" → `brew install node`; sonra paneli
  kapatıp açın.
- Günlük: `~/Library/Application Support/SmartEditor/log/engine.log`
