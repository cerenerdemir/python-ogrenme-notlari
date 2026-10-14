```markdown
# Python Temelleri: Değişkenler ve Stringler

Bu doküman; Python'da temel değişken kuralları, aritmetik işlemler, yorum satırları, string indeksleme/dilimleme yöntemleri ve veri tipi değiştirilemezliği (immutability) konularını içerir.

---

## 1. Değişkenler ve Tanımlama Kuralları

Değişkenler, belirli bir veri tipinden değer tutan temel birimlerdir. Python'da **dinamik tiplendirme (dynamic typing)** özelliği bulunur; bir değişkenin tipi çalışma esnasında farklı bir tipe güncellenebilir.

### Adlandırma Kuralları
1. **Sayı ile Başlayamaz:** Değişken isimlerinin ilk karakteri rakam olamaz (`1sayi` geçersiz, `sayi1` geçerlidir).
2. **Boşluk İçeremez:** Kelimeler arasında boşluk kullanılamaz; standart olarak alt çizgi tercih edilir (`sayi degeri` yerine `sayi_degeri`).
3. **Özel Karakter Kısıtlaması:** Alt çizgi (`_`) haricinde hiçbir noktalama/sembol kullanılamaz (`: ' " , < > / ? | \ ( ) ! @ # $ % ^ & * ~ - +`).
4. **Rezerve Kelimeler:** Python'a ait anahtar sözcükler (`while`, `not`, `for`, `def`, `class` vb.) değişken ismi olarak seçilemez.

### Temel Değişken İşlemleri

```python
# Değerleri birbiriyle takas etme (Tuple Unpacking)
a = 4
b = 3
a, b = b, a  # Sonuç: a = 3, b = 4

# Artırma işleci
a = a + 1
a += 1  # a = a + 1 işleminin pratik yazımı

```

---

## 2. Yorum Satırları ve Aritmetik İşlemler

### Yorum Satırları

```python
# Tekli yorum satırı: Yalnızca bulunduğu satırı kapsar
print("murat")

"""
Çoklu yorum satırı:
Birden fazla satıra yayılan açıklamalar
veya dokümantasyon metinleri (docstring) için kullanılır.
"""
print("murat")

```

### Sayısal İşlemler

```python
# Bölme İşlemi (/)
# Python 3'te tam bölme olsa dahi sonuç kesinlik sağlamak adına float olarak döner:
sonuc = 4 / 2  # Çıktı: 2.0

# Üs Alma ve Karekök (**)
# Bir sayının 0.5 üssü o sayının kareköküdür:
karekok = 64 ** 0.5  # Çıktı: 8.0

# Modülüs - Kalan Bulma Operatörü (%)
# Bir sayının çift/tek kontrolünde veya bölme artıklarını bulmada kullanılır:
kalan = 15 % 2  # Çıktı: 1 (Tek sayı)

```

---

## 3. String (Karakter Dizisi) Yapısı

Stringler tek tırnak (`'`), çift tırnak (`"`) veya üç tırnak (`"""`) kullanılarak tanımlanabilir. Metin içinde kesme işareti geçerken kaçış karakteri (`\`) ya da farklı tırnak tipleri seçilmelidir:

```python
# Hatalı: 'Murat'ın bugün dersi var.' -> SyntaxError

# Doğru kullanımlar:
mesaj_1 = "Murat'ın bugün dersi var."
mesaj_2 = 'Murat\'ın bugün dersi var.'  # Ters eğik çizgi (\) kaçış karakteridir

```

### İndeksleme (Indexing)

Stringler karakter dizileridir ve indeks numaraları `0`'dan başlar. Negatif indeksler ise sondan geriye doğru sayar (`-1` son elemandır).

```python
a = "ali"
print(a[0])  # Çıktı: 'a'

b = "murat"
print(b[-1])  # Çıktı: 't' (Son eleman)

```

### Dilimleme (Slicing)

Bir stringin belirli bir aralığını almak için `[başlangıç : bitiş : adım]` sözdizimi kullanılır. **Bitiş indeksi dahil edilmez.**

```python
a = "Python Programlama Dili"

# 4. indeksten başla, 10. indekse kadar (dahil değil) al
print(a)    # 'on Pro'

# Başlangıç belirtilmemişse en baştan başlar
print(a[:10])     # 'Python Pro'

# Bitiş belirtilmemişse en sona kadar gider
print(a[4:])      # 'on Programlama Dili'

# İki değer de boşsa tüm stringi kopyalar
print(a[:])       # 'Python Programlama Dili'

# Son karaktere kadar al (son karakter hariç)
print(a[:-1])     # 'Python Programlama Dil'

# Baştan sona 2 adım atlayarak al
print(a[::2])     # 'Pto rgalm ii'

# 4'ten 12'ye kadar 3'er atlayarak al
print(a[4:12:3])  # 'oPg'

# String'i ters çevirme
print(a[::-1])    # 'iliD amalmargorP nohtyP'

```

### String Özellikleri ve Değiştirilemezlik (Immutability)

String veri tipi **immutable** (değiştirilemez) bir tiptir. Bir string bellekte tanımlandıktan sonra karakterleri doğrudan indeks üzerinden güncellenemez.

```python
a = "Python Programlama Dili"

# Uzunluk bulma
print(len(a))  # Çıktı: 23

# String çoğaltma
print("Python" * 3)  # Çıktı: 'PythonPythonPython'

# Bellek Yönetimi ve Yeniden Atama:
# Aşağıdaki işlemde mevcut string yerinde değiştirilmez; 
# bellekte yeni bir string nesnesi üretilip değişkene atanır:
a = "Mustafa "
a = a + "Murat Coşkun"  # Eski "Mustafa " referansı boşa çıkar, yeni nesne atanır.

```

---

## 4. Kod Analizi: String Elemanına Doğrudan Atama

### İncelenen Kod Parçası

```python
a = "Python"
a[0] = 'C'
a

```

### Çalışma Analizi ve Hata Çıktısı

1. `a` değişkenine bellekte `"Python"` string nesnesi bağlanır.
2. `a[0] = 'C'` satırı çalıştığında Python, string veri tipinin `__setitem__` metodunu desteklemediğini kontrol eder.
3. Stringler **immutable** olduğu için atama başarısız olur ve program çöker.

**Terminal Çıktısı:**

```text
TypeError: 'str' object does not support item assignment

```

> **Çözüm Yolu:** Stringi değiştirmek yerine dilimleme yöntemiyle yeni bir string oluşturulup değişkene yeniden atanabilir:
> ```python
> a = "C" + a[1:]  # Çıktı: 'Cython'
> 
> ```
> 
> 

```

```
