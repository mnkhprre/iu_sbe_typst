# İÜ SBE — Typst Tez Şablonu

[![Typst](https://img.shields.io/badge/Typst-%E2%89%A50.15-23B3A9?style=flat-square)](https://typst.app)
[![Dil: Türkçe](https://img.shields.io/badge/dil-T%C3%BCrk%C3%A7e-2C2A25?style=flat-square)](#)
[![Lisans: MIT](https://img.shields.io/badge/lisans-MIT-blue?style=flat-square)](LICENSE)
[![Derleme: kararlı](https://img.shields.io/badge/derleme-ba%C5%9Far%C4%B1l%C4%B1-2E7D32?style=flat-square)](#h%C4%B1zl%C4%B1-ba%C5%9Flang%C4%B1%C3%A7)

İstanbul Üniversitesi Sosyal Bilimler Enstitüsü (SBE) **tez hazırlama ve biçimlendirme yönergesine** göre hazırlanmış, [Typst](https://typst.app) ile çalışan tez şablonu. Şablon; ön kısım, metin kısmı, kaynakça, ekler ve özgeçmiş bölümlerini yönergedeki madde sırasına göre otomatik olarak üretir ve filoloji / mısıroloji / hititoloji çalışmaları için hazır transliterasyon blokları içerir.

> [!WARNING]
> Bu depo **İstanbul Üniversitesi veya Sosyal Bilimler Enstitüsü'nün resmi şablonu değildir**. Öğrenci çalışması olarak, yönergedeki kuralları birebir modellemek amacıyla hazırlanmıştır. Resmî bir güncelleme veya onay süreci yoktur; kullanılan yönerge için bkz. [`tez_hazırlama_yönergesi.pdf`](tez_hazırlama_yönergesi.pdf).

## İçindekiler

- [Gereksinimler](#gereksinimler)
- [Hızlı başlangıç](#hızlı-başlangıç)
- [Tavsiye edilen program: Texpile](#tavsiye-edilen-program-texpile)
- [Depo yapısı](#depo-yapısı)
- [Belge akışı: `main.typ` sırası](#belge-akışı-maintyp-sırası)
- [Yönerge madde eşlemesi](#yönerge-madde-eşlemesi)
- [Tipografi ve sayfa kuralları](#tipografi-ve-sayfa-kuralları)
- [Yardımcı fonksiyonlar](#yardımcı-fonksiyonlar)
- [Filolojik transliterasyon blokları](#filolojik-transliterasyon-blokları)
- [Tablo, şekil ve çapraz referans](#tablo-şekil-ve-çapraz-referans)
- [Kaynakça](#kaynakça)
- [Yeni bölüm ekleme](#yeni-bölüm-ekleme)
- [Derleme sorunlarını giderme](#derleme-sorunlarını-giderme)
- [Geliştirme notları](#geliştirme-notları)
- [Lisans](#lisans)

---

## Gereksinimler

| Gereksinim | Not |
| --- | --- |
| [Typst CLI](https://github.com/typst/typst) **0.15+** | `typst --version` ile doğrulayın. Şablon 0.15.1 ile test edilmiştir. |
| **Times New Roman** | Gövde metni. macOS/Windows'ta hazır; Linux'ta `ttf-mscorefonts-installer` veya benzeri paket gerekir. Yedek olarak `Times` aranır. |
| **Antinoou** | Yalnızca Mısırca transliterasyon bloğu (`#eb`) için. |
| **Aegyptus** | Yalnızca hiyeroglif çıktısı (`#hiero`) için. |
| **Noto Sans Cuneiform** | Yalnızca çivi yazısı çıktısı (`#cunei`) için. |

> Fontlar sistemde yoksa Typst derlemeyi durdurmaz; yalnızca uyarı verir ve metin yedek fontla dizilir. Enstitüye teslim edilecek PDF'te hatasız görünüm için yukarıdaki fontların kurulu olduğundan emin olun.

## Hızlı başlangıç

Depo kök dizinindeyken:

```sh
# Tek seferlik derleme
typst compile bolum/typ/main.typ main.pdf

# Kaydettiğinizde otomatik yeniden derleme (izleme modu)
typst watch bolum/typ/main.typ main.pdf
```

Yalnızca hata denetimi yapmak, PDF üretmemek istiyorsanız çıktı olarak geçici bir yol verin (macOS/Linux):

```sh
typst compile --diagnostic-format short bolum/typ/main.typ /dev/null
```

**Diğer editör seçenekleri**

- [VS Code + Tinymist Typst](https://github.com/Myriad-Dreamin/tinymist) veya [Typst Preview](https://github.com/enter-tainer/typst-preview): kaydettiğinizde canlı önizleme.
- [typst.app](https://typst.app) web uygulaması: kurulum gerektirmez, dosyaları sürükleyip bırakabilirsiniz.
- Komut satırı: yukarıdaki `watch` komutu yeterlidir.

İlk derlemeden sonra kök dizinde `main.pdf` üretilir; repodaki [`main.pdf`](main.pdf) güncel şablonun örnek çıktısıdır.

## Tavsiye edilen program: Texpile

Bu şablonla çalışmak için önerdiğimiz düzenleyici [**Texpile**](https://texpile.com)'dir.

> Texpile; **yerel ve çevrimdışı** çalışan, LaTeX ve **Typst** destekli ücretsiz bir düzenleyicidir ([AGPL-3.0](https://github.com/texpile/texpile), açık kaynak). Windows, macOS ve Linux'ta çalışır.

Şablonu kullanırken işinizi kolaylaştıran özellikleri:

| Özellik | Bu şablonda ne işe yarar |
| --- | --- |
| Yazarken güncellenen PDF önizlemesi | `main.typ` ve bölümleri düzenlerken çıktıyı anında görürsünüz. |
| Çok dosyalı proje desteği | `#include` ile birleşen `iusosbil.typ`, `kapak.typ`, `chap_*.typ` dosyaları ana dosyanın makro ve tanımlarıyla birlikte çözümlenir. |
| `@` ile etiket ve atıf tamamlama | `@tab_degiskenler`, `@fig_model` ve `kaynakca.bib` anahtarlarını listeler; bilinmeyen adı derlemeden önce işaretler. |
| Canlı denetimler | Yazım anında tanımsız ad/etiket uyarısı verir, derlemeyi beklemez. |
| Gömülü terminal | `typst compile` / `typst watch` komutlarını düzenleyiciden çalıştırabilirsiniz. |
| Sürüm geçmişi | Değişiklikleri aşama, commit at ve yan yana diff al. |
| Metin denetimi (imla) | Yazdığınız düz metni denetler; komut, matematik ve yorum satırlarını atlar. |

İndirme: [texpile.com/download](https://texpile.com/download) — [Typst editörü dokümanları](https://texpile.com/typst-editor).

## Depo yapısı

```
iu_sbe_typst/
├── main.pdf                        # Örnek derlenmiş çıktı
├── tez_hazırlama_yönergesi.pdf     # Biçimlendirme esasının alındığı yönerge
├── README.md
├── .gitignore
└── bolum/typ/
    ├── main.typ                    # GİRİŞ NOKTASI — sırayı ve şablonu burada tanımlarsınız
    ├── iusosbil.typ                # Şablon fonksiyonu + tüm stil ve yardımcı komutlar
    ├── kapak.typ                   # İç kapak (Madde 9)
    ├── chap_approve.typ            # Tez onay sayfası ve jüri imza tablosu (Madde 10)
    ├── chap_frontmatter.typ        # Öz, Abstract, Önsöz, İçindekiler, listeler (Madde 11–15)
    ├── chap_intro.typ              # Giriş — numarasız (Madde 16/a, 17)
    ├── chap_1.typ                  # Bölüm 1 (Madde 16/c)
    ├── chap_2.typ                  # Bölüm 2 — tablo/şekil örnekleri (Madde 16/c)
    ├── chap_3.typ                  # Bölüm 3 (Madde 16/c)
    ├── chap_result.typ             # Sonuç ve Öneriler — numarasız (Madde 16/e)
    ├── bibliyografi.typ            # Kaynakça görünümü (Madde 22)
    ├── chap_attach.typ             # Ekler (Madde 23)
    ├── CV.typ                      # Özgeçmiş — şablonu BOŞ, doldurulacak
    └── kaynakca.bib                # BibTeX kaynak verisi
```

Kural basittir: **sadece `main.typ` ve ilgili bölüm dosyalarını düzenlersiniz.** Stil, ölçü, başlık ve dipnot kuralları `iusosbil.typ` içinde merkezîdir; bölüm dosyalarında tekrar tanımlamak yerine oradan değiştirin.

## Belge akışı: `main.typ` sırası

`main.typ` iki parçadan oluşur: şablonu tüm belgeye giydiren `#show` kuralı ve dosyaları sırayla içeren `#include` satırları.

```typst
#import "iusosbil.typ": iusosbil_tez

#show: iusosbil_tez.with(
  yazar: "Adı SOYADI",
  tez-turu: "DOKTORA TEZİ"
)

// A. ÖN KISIM  (Madde 8/A)
#include "kapak.typ"            // Madde 9  — sayfa numarasız (i sayılır)
#include "chap_approve.typ"     // Madde 10 — sayfa numarasız (ii sayılır)

#set page(numbering: "i", number-align: bottom + center)
#counter(page).update(3)        // iii'ten başlat
#include "chap_frontmatter.typ" // Madde 11–15

// B. METİN KISMI (Madde 8/B)
#set page(numbering: "1", number-align: bottom + center)
#counter(page).update(1)        // Giriş'te 1'den başlat

#include "chap_intro.typ"       // Madde 16/a, 17
#include "chap_1.typ"           // Madde 16/c, d
#include "chap_2.typ"
#include "chap_3.typ"
#include "chap_result.typ"      // Madde 16/e
#include "bibliyografi.typ"     // Madde 22
#include "chap_attach.typ"      // Madde 23
#include "CV.typ"               // Madde 8/B — doktora tezleri için zorunlu
```

| Aşama | Sayfa numarası | Kaynak |
| --- | --- | --- |
| İç kapak + tez onay sayfası | görünmez (i–ii sayılır) | `kapak.typ`, `chap_approve.typ` |
| Öz → Kısaltmalar listesi | Roma rakamı, alt ortada (iii'ten) | `chap_frontmatter.typ` |
| Giriş → Özgeçmiş | Arap rakamı, alt ortada (1'den) | `chap_*.typ`, `CV.typ` |

`yazar` ve `tez-turu` parametreleri şimdilik yalnızca şablon çağrısında bilgi taşır; **iç kapak ve onay sayfasındaki ad, numara, unvan ve tarih bilgilerini ilgili dosyalarda elle doldurun** (`kapak.typ`, `chap_approve.typ`, `chap_frontmatter.typ`).

## Yönerge madde eşlemesi

| Yönerge | İçerik | Dosya |
| --- | --- | --- |
| Madde 3/a–b | Sayfa numarası görünürlüğü, tablo/şekil numaraları | `main.typ`, `iusosbil.typ` |
| Madde 4/a | Kenar boşlukları (üst 4 cm, alt 2,5 cm, sol 4 cm, sağ 2,5 cm) | `iusosbil.typ` |
| Madde 4/b | İki yana yaslı, 1,5 satır aralığı | `iusosbil.typ` |
| Madde 5/a | Başlık biçimi ve hiyerarşisi | `iusosbil.typ` |
| Madde 8/A–B | Ön kısım / metin kısımı kurgusu | `main.typ` |
| Madde 9 | İç kapak | `kapak.typ` |
| Madde 10 | Tez onay sayfası ve jüri imza tablosu | `chap_approve.typ` |
| Madde 11 | Öz (TR) ve Abstract (EN), en fazla 250 kelime | `chap_frontmatter.typ` |
| Madde 12 | Önsöz (en fazla 2 sayfa) | `chap_frontmatter.typ` |
| Madde 13 | İçindekiler | `chap_frontmatter.typ` |
| Madde 14 | Şekiller ve tablolar listesi (otomatik) | `chap_frontmatter.typ` |
| Madde 15 | Kısaltmalar listesi | `chap_frontmatter.typ` |
| Madde 16/a–b | Giriş | `chap_intro.typ` |
| Madde 16/c–d | En az üç bölüm (Giriş hariç) | `chap_1..3.typ` |
| Madde 16/e | Sonuç ve öneriler | `chap_result.typ` |
| Madde 17 | Giriş ve sonuç numaralandırılmaz | ilgili bölüm dosyaları |
| Madde 18/a, 18/e | Kısa alıntılar ve blok aktarma | `chap_1.typ` örneği |
| Madde 19/a | Dipnot: 10 punto, tek satır | `iusosbil.typ` |
| Madde 22 | Kaynakça | `bibliyografi.typ`, `kaynakca.bib` |
| Madde 23 | Ekler | `chap_attach.typ` |

## Tipografi ve sayfa kuralları

Bu değerlerin tamamı `bolum/typ/iusosbil.typ` içinde tanımlıdır. Değişiklik yaparken bölüm dosyalarına değil oraya bakın.

| Öğe | Kural |
| --- | --- |
| Kağıt / kenar | A4 — üst 4 cm, alt 2,5 cm, sol 4 cm, sağ 2,5 cm |
| Gövde metni | Times New Roman, 12 pt, iki yana yaslı, 1,5 satır aralığı |
| Paragraf girintisi | Her paragrafın ilk satırı 1 cm (boş satırlar dahil) |
| Başlıklar | 14 pt kalın; 1. seviye ortalanır ve yeni sayfada başlar |
| Başlık numaraları | `1`, `1.1`, `1.1.1` biçiminde otomatik |
| Dipnotlar | 10 pt, tek satır; **her ana bölümde sayaç sıfırlanır** |
| Transliterasyon blokları | 10–11 pt, tek satır (bkz. [Filolojik bloklar](#filolojik-transliterasyon-blokları)) |
| Sayfa numarası | Alt orta; ön kısım Roma (`i`, `iii`…), metin Arap (`1`, `2`…) rakam |
| Tırnaklar | Akıllı tırnak açık; kelime/nokta sonrası düz tırnak otomatik kapanışa çevrilir |

Yalnızca **bir blok** için farklı değer gerekiyorsa o bloğun içine yerel ayar ekleyin:

```typst
#[
  #set text(size: 11pt)
  #set par(leading: 1em)
  Yalnızca bu paragrafı etkileyen ayarlar.
]
```

## Yardımcı fonksiyonlar

`iusosbil.typ` şu yardımcıları dışa aktarır:

```typst
#import "iusosbil.typ": *            // hepsi, ya da
#import "iusosbil.typ": eb, hb, sup  // seçerek
```

| Fonksiyon | Ne yapar |
| --- | --- |
| `#translit[...]` | 11 pt italik transliterasyon metni; `[…]`, `⸢⸣`, `⟨⟩` işaretleri italikten çıkarılır. |
| `#sup[...]` | Üst simge üretir (`super` ile aynıdır). Örnek: `#sup[1]` ya da ikili yazımda `URU#sup[2]`. |
| `#hiero[𓂀]` | Hiyeroglif metnini **Aegyptus** fontuyla dizmek için. |
| `#cunei[𒀀]` | Çivi yazısı metnini **Noto Sans Cuneiform** fontuyla dizmek için. |
| `#tabletrule` | Tablo içi kısa yatay çizgi (uzunluk %40, kalınlık 0,5 pt). |
| `kt` | Kapanış tırnağı (`”`) kısayolu. |

## Filolojik transliterasyon blokları

Dört hazır blok vardır; hepsi aynı yapıyı paylaşır: künye satırı → ayırıcı çizgi → transliterasyon → (varsa) Türkçe çeviri.

| Fonksiyon | Dil / alan | Yazı tipi |
| --- | --- | --- |
| `#eb(...)` | Mısırca transliterasyon | Antinoou, 10 pt |
| `#hb(...)` | Hititçe transliterasyon | Times New Roman, 10 pt |
| `#yb(...)` | Eski Yunanca | Times New Roman, 10 pt |
| `#lb(...)` | Latince (Leiden işaretleri) | Times New Roman, 10 pt |

Ortak parametreler:

- `b:` — eser / metin adı (künye 1. satır)
- `m:` — yayın yeri, kolon, satır aralığı (künye 2. satır)
- `s:` — satır numarası (künye 3. satır; `hb` dışında `sat.` öneki otomatik gelir)
- `ceviri:` — Türkçe çeviri bloğu; bloğun soluna 1 cm kaydırılır

```typst
#eb(
  b: "İbana oğlu Ahmosis Otobiyografisi",
  m: "Urk. IV, 3.1-4.12",
  s: "4.12",
  ceviri: [ Çeviri metni buraya. ]
)[
  _ı͗ṯ.kwı͗ r pꜣ dpt mḥty ḥr ḳnn(.ı͗(??))_
]
```

Bu bloklarda dipnotlar gizlenir (künye dipnotu çakışmasın diye), köşeli parantezler ve `⸢⸣`/`⟨⟩` gibi filolojik işaretler italik dışı yazılır — şablonun otomatik tırnak düzeltmeleri de devrede kalır.

## Tablo, şekil ve çapraz referans

Tablo ve şekiller `#figure(...)` ile tanımlanır; numaraları ve listeleri (Madde 14) otomatik üretilir. Metin içinde `<etiket>` ile işaretleyip `@etiket` ile çağırırsınız:

```typst
#figure(
  caption: [Araştırmada İncelenen Değişkenlerin Dağılımı],
  table(
    columns: (1fr, 1fr, 1fr),
    [*Kategori*], [*N*], [*Oran (%)*],
    /* satır verileri */
  )
) <tab_degiskenler>

@tab_degiskenler incelendiğinde, örneklem gruplarının dağılımı görülmektedir.
```

`@etiket` kullanımı hem tablo/şekil numarasını hem de sayfa numarasını metne yazar; elle numara yazmayın.

## Kaynakça

Kaynakları `bolum/typ/kaynakca.bib` dosyasına BibTeX biçiminde ekleyin:

```bibtex
@book{ornek2026,
  author    = {Adı SOYADI},
  title     = {Eserin Adı},
  publisher = {Yayınevi},
  address   = {İstanbul},
  year      = {2026}
}
```

Metinde kaynak göstermek için `@ornek2026` (veya `#cite(<ornek2026>)`) yazın. Görünüm `bibliyografi.typ` içinde tanımlıdır:

```typst
#bibliography(
  "kaynakca.bib",
  title: none,   // başlık elle eklendiği için gizli
  style: "apa"   // asılı girintili APA
)
```

- Liste **yalnızca metinde atıf yapılan kaynakları** gösterir. Tüm girdileri basmak için `full: true` ekleyin.
- `title: none` satırını kaldırmayın; `KAYNAKÇA` başlığı `bibliyografi.typ` içinde elle eklenmiştir ve `outlined: true` olduğu için içindekilerde görünür.
- Stili değiştirmek için Typst'in yerleşik CSL stillerinden birini yazın, örn. `style: "chicago-author-date"`.

## Yeni bölüm ekleme

1. `bolum/typ/chap_4.typ` gibi yeni bir dosya oluşturun.
2. Başlığı `#heading(level: 1)[BÖLÜM BAŞLIĞI]` ile yazın — numara (`4`) otomatik gelir.
3. Alt başlıklar için `level: 2`, `level: 3`, `level: 4` kullanın.
4. Dosyayı `main.typ` içinde uygun sıraya ekleyin:

```typst
#include "chap_4.typ"
```

`level: 1` başlıkları zaten kendilerinden önce sayfa sonu uygular (`pagebreak(weak: true)`), ayrıca `#pagebreak()` yazmanıza gerek yoktur. Yine de bir bölümün ortasında zorla sayfa bölmek isterseniz `#pagebreak()` kullanabilirsiniz.

> Madde 16/d: Giriş bölümü hariç tez **en az üç bölümden** oluşmalıdır.

## Derleme sorunlarını giderme

Hata satırını okumak için kısa biçim kullanın:

```sh
typst compile --diagnostic-format short bolum/typ/main.typ main.pdf
```

| Belirti | Olası neden | Çözüm |
| --- | --- | --- |
| `file not found (searched at bolum/typ/...)` | Komut yanlış dizinden çalıştırıldı veya dosya adı yanlış | Kök dizinden `bolum/typ/main.typ` yolunu kullanın; ana dosya `thesis.typ` değil **`main.typ`**'dir. |
| Yeni bölüm PDF'te görünmüyor | `#include` satırı eklenmedi | `main.typ` içine `#include "chap_4.typ"` ekleyin. |
| `expected ...` / kapanmayan blok | Köşeli parantez `]` veya süslü parantez `}` eksik | Hata satırındaki dosya ve satır numarasını kontrol edin. |
| `citation key ... is not present` | `@anahtar` bib dosyasında yok | Anahtarı `kaynakca.bib` içine ekleyin, yazımı (büyük/küçük harf) kontrol edin. |
| `unknown font` uyarısı | Times New Roman / Antinoou / Aegyptus / Noto Sans Cuneiform kurulu değil | [Gereksinimler](#gereksinimler) bölümündeki fontları kurun. |
| Listede olmayan kaynak basılıyor | `full: true` açık | `bibliyografi.typ` içinde `full: true` satırını kaldırın. |
| İçindekiler / liste eski sayfayı gösteriyor | Tanıtımlar bayat | `typst watch` ile derleyin ya da PDF'i yeniden üretin. |
| İki kez aynı bölüm | Aynı dosya iki kez `#include` edilmiş | `main.typ` içinde tekrar eden satırı silin. |

## Geliştirme notları

- **Eski XeLaTeX sürümü artık bu depoda yok.** Depo adı geçmişi yansıtan `iu_sbe_latex` idi; XeLaTeX kaynakları silindi ve şablon tümüyle Typst'e taşındı.
- **Uç birim çıktısı tutmaz.** `bolum/typ/*.pdf` derleme artıklarıdır ve `.gitignore` ile hariç tutulmuştur; commit etmeyin.
- Kök dizindeki `main.pdf` ve `tez_hazırlama_yönergesi.pdf` kasıtlı olarak takip edilir.
- Katkı için fork → branch → pull request akışı uygundur. Değişiklikten önce `typst compile` ile derlemenin başarılı olduğunu doğrulayın.
- Yönerge değiştiğinde ilgili dosyadaki `// Madde ...` açıklamalarını güncelleyin; kod ile yönerge arasındaki bağın tek kaynağı onlardır.

## Lisans

Şablon kodu [MIT Lisansı](LICENSE) ile dağıtılır: kendi tezinizde serbestçe kullanabilir, değiştirebilir ve paylaşabilirsiniz. Tezinizin içeriği size aittir; lisans yalnızca şablon dosyalarını kapsar.

Depodaki [`tez_hazırlama_yönergesi.pdf`](tez_hazırlama_yönergesi.pdf) İstanbul Üniversitesi Sosyal Bilimler Enstitüsü'ne aittir ve bu lisansın kapsamında değildir; yalnızca başvuru amacıyla eklenmiştir.
