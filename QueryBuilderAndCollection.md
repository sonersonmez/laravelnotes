# Laravel Notlarım


## Laravel Query Builder Fonksiyonları

 - DB::table('tabloadi) ile kullanılır. DB Kütüphanesini "use" ile namespace'in üstünde çağırmak gerekir.
 - DB::table('tabloadi')->get();  bir DİZİ halinde döner, foreach ile birlikte ekrana basabiliriz.
 - DB::table('tabloadi')->first(); Tabloya kayıtlı ilk record(kayıt)ı getirir.
 - DB::table('tabloadi')->where('columnName', 'value')->first(); where ile birlikte ilk değerimiz sütun adı, ikinci değerimiz ise ne olduğudur.
 - DB::table('tabloadi')->find(3) ID'si 3 olan elemanı çeker.
 - DB::table('tabloadi')->pluck *
 - DB::table('tabloadi')->chunk(3)  Collection yapısı ile birlikte dönen diziyi chunk'la belirttiğimiz kadar parçalara böler. Bootstrap grid sistemiyle uyumludur.
 - DB::table('tabloadi')->orderBy('id') ID numarasına göre sıralar.
 - DB::table('tabloAdi')->count() Tablodaki toplam eleman sayısını geri döner.
 - DB::table('tabloAdi')->max('price') Price değeri en yüksek olanı getirir.
 - DB::table('tabloAdi')->min('price') Price değeri en düşük olanı getirir.

### Çoklu Where Query'leri yapılabilir.
 - DB::table('tabloAdi')->where('is_active', '=', 1)->where('age', '>', 35)->get();

## Collection Özellikleri
  Collectionlar, dizilerin daha gelişmişi olarak kullanılan bilen yapılardır.

  Örneğin, bir dizi oluşturup bunu collection nesnesi haline çevirmek için: 
  $products = ['Bilgisayar', 'Telefon', 'Tablet'] // Dizimiz
  $products = collect(['Bilgisayar', 'Telefon', 'Tablet']); // Artık bir collection nesnesi.

  $salaries = collect([3500, 6000, 12500, 8600]);
  return $salaries->avg(); // avg fonksiyonuyla birlikte ortalama(average) alabiliyoruz.

  $uberSuperArray = collect([[1,2,5], 28, ['Ayşe', 'Fatma', 'Hayriye']]); // Bu şekilde kullanırsak array içinde 2 farklı array,28 değerinde int olduğunu görürüz.
  return $uberSuperArray->collapse(); // Bu şekilde kullanırsak array içerisindeki arrayleri kaldırıp tek bir array olarak dönüş alırız.

  $collection = collect(['name' => 'Desk', 'price' => 100]);
  $collection->contains('Desk'); // true
  $collection->contains('New York'); // false
  contains() metoduyla birlikte bir değerin olup olmadığını kontrol edebiliriz. True veya False (boolean) dönecektir.

  $collection = collect([1, 2, 3, 4, 5]);
  $diff = $collection->diff([2, 4, 6, 8]);
  $diff->all(); // Çıktı olarak [1, 3, 5] verecektir.
  
  İki collectionumuz varsa, 1. ve 2. collection'u eşleştirip açıkta kalan(eşleşmeyen) value'ları görebiliriz.

###  Transform ve Map arasındaki farklar

  Bizim oluşturduğumuz ya da response olarak gelen collection içerisinde, o collection'a ait kod yazmamış gerekiyorsa transform kullanabiliriz.
  $collection = collect([1, 2, 3, 4, 5]);
 
  $collection->transform(function ($item, $key) {
    return $item * 2;
  });
 
  $collection->all(); // [2, 4, 6, 8, 10] Çıktı olarak collection'umuzun değerlerinin 2 ile çarpıldığı durumu aldık. Eğer işlem sonucunda üretilen collection'u ayırmak   istersek, o zaman map kullanabiliriz. Map ile birlikte hem collection'umuz kendi değerlerini korur, hem de işlem sonucu üretilen yeni collection'u ayırıp               kullanabiliriz.
  
