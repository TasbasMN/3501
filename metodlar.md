## Verilerin Ön İşlenmesi

Laboratuvar kaynaklı, yüksek kalite miRNA-mRNA bağlanma verileri (Helwak et al., 2013) makalenin sunduğu bağlantılardan elde edilmiştir. İndirilen ham veriden, makine öğrenmesi metodunda kullanmak için gereken şu kolonlar elde edilmiştir; miRNA adı, miRNA sekansı, miRNA sekansının hangi nükleotitlerinin bağlanmada görev aldığı, mRNA adı, mRNA'nın hangi nükleotitlerinin bağlanmada görev aldığı, bağlanmada görev alan kısmın olgun mRNA sekansı, etkileşimde görev alan baz çifti sayısı, çekirdek bölgesindeki baz çifti sayısı. Her satırdaki mRNA sekansı, elimizdeki sekans veritabanı ile karşılaştırıp uyuşmazlıklar kontrol edilmiştir. Verisetinin makalesinde sekansların Ensembl (Harrison et al., 2023) veritabanı 60. versiyonu kullanıldığı görüldüğü için karşılaştırma Ensembl60 versiyonu sekansları kullanılarak yapılmıştır. Ensembl web sitesinden temin edilen 60. versiyon sekansları ile makalenin verisetinde temin edilmiş sekansların karşılaştırılması sonucu DDX21 adlı transkriptin sekansında uyuşmazlık tespit edilmiştir. Bu transkripti içeren 6 adet miRNA-mRNA ikilisi veritabanından çıkartılmıştır. Bağlantı bölgesinin, verilen sekansın sınırlarında çıkması ihtimaline karşılık, her satırdaki mRNA dilimlerinin her iki ucu da 30'ar nükleotit uzatılmıştır. Elimizdeki sekans verileri 5'-3' yönlü cDNA formunda olduğu için bu çalışmadaki bütün sekanslar bu formda kullanmak üzere standardize edilmiştir.
  
  

CLASH (Helwak et al., 2013) adı verilen deneysel protokolün sınırları dolayısıyla her ikili komplekste yer alan mRNA molekülünün tam olarak hangi nükleotitlerinin bağlanmada görev aldığı bilinmemekle birlikte, verisetinde bağlantı bölgesini de içerdiğinden emin olunan daha büyük bir sekans parçası verilmiştir. Sekans temelli modelimizin düzgün çalışması için tam olarak hangi nükleotitlerin bağlanmada görev aldığını bilmemize ihtiyaç vardır. Yapılan literatür araştırması doğrultusunda ViennaRNA (Lorenz et al., 2011) adlı biyoenformatik araçları paketinin içerisinde yer alan RNADuplex adlı programın kullanımı uygun görülmüştür. RNADuplex, kendisine verilen iki adet mRNA sekansının termodinamik açıdan en kararlı hangi konformasyonda bağlanacağını hesaplayıp kullanıcıya şu verileri sunar; tam olarak hangi nükleotitlerin bağlanmada görev aldığı, bağlanmanın şematik çizimi ve hesaplanan gibbs serbest enerji değeri. RNAduplex çıktıları kullanılarak, ham verideki her satır için, o satırdaki mRNA'nın tam olarak hangi bölgesinin bağlantıda rol aldığı hesaplanmıştır. Literatürde MRE (miRNA recognition element, miRNA tanıma bölgesi) olarak geçen bu bölge, ilerleyen aşamalarda önemli bir görev üstlenecektir.Bu hesaplama ile birlikte elimizdeki her bir miRNA-mRNA etkileşimi için MRE pozisyonları ve o etkileşimlerin kaç nükleotitten oluştuğu elde edilmiştir. 

## Pozitif veriseti oluşturulması

Doğruluğundan tam emin olunan bir pozitif veri seti hazırlamak, makine öğrenmesi metotlarının başarısında çok önemli bir adımdır[ref_needed]. Bu yüzden, elimizdeki verileri filtreleyip pozitif veriseti oluşturduk. Bunun için, çekirdek tipi 6mer, 7mer ve 8mer görünmesine rağmen çekirdek bölgesinde 4'ten az sayıda baz çifti içeren satırları filtreledik. Ayrıca, bağlantı enerjisi -5 kcal/mol'den yüksek olan ikilileri, yapıları stabil olmayacağı için filtreledik. Ayrıca, MRE bölgesinde 5'ten az baz çifti olan satırları da filtreledik. En son adım olarak, CLASH tarafından temin edilen baz çifti sayısı ile RNADuplex tarafından tahmin edilen baz çifti sayısı arasındaki fark 1'den büyük olan satırları da filtreledik.

## Negatif Veriseti Oluşturulması

Negatif veriseti hazırlamak, makine öğrenme modelinin düzgün tahmin etmesi bakımından en az pozitif veriseti hazırlamak kadar önemlidir[ref_needed]. Yapılan literatür taraması sonucunda, nükleotit sekansı için negatif veri seti hazırlamaya yönelik farklı yaklaşımlar değerlendirilip, Klimentova et al. (2022)'de anlatılan negatif veriseti üretme metodunun değiştirilmiş bir halinin kullanmasına karar verilmiştir. Bu yaklaşımda, CLASH tarafından temin edilen miRNA-mRNA ikililerindeki her miRNA için, o miRNA'nın sekansına en uzak Levenshtein mesafesine sahip başka bir miRNA sekansı bulunarak negatif veri seti oluşturulmuştur. Levenshtein mesafesi, iki dizgi arasındaki minimum düzenleme mesafesini ölçen bir algoritmadır. Bu mesafe, bir dizgiyi diğerine dönüştürmek için gereken ekleme, silme veya değiştirme işlemlerinin sayısını ifade eder. Elimizdeki her miRNA için, ona en uzak Levenshtein mesafeli miRNA'yı seçtiğimizde, o miRNA'nın verilen MRE bölgesine bağlanmayacağından emin olabiliriz.

Negatif sekanslar üretildikten sonra, negatif miRNA sekansları ve MRE bölgesini içeren mRNA sekansları, yine RNADuplex programına gönderilip çıktıları alınmıştır. Son adım olarak, negatif ve pozitif verisetleri ortak bir verisetinde toplanmış ve pozitif veriler 1, negatif veriler ise 0 kullanarak etiketlenmiştir.

# Öznitelik mühendisliği


RNADuplex programı, verilen iki RNA molekülünün etkileşim şemasını nokta parantez notasyonu (dot bracket notation) kullanarak resmeder. Bu notasyonda birbiriyle WC etkileşiminde bulunan nükleotitler parantezle, herhangi bir WC etkileşiminde bulunmayan nükleotitler ise nokta ile resmedilir. miRNA ve mRNA için ayrı ayrı elde edilen nokta parantez notasyonları, kolaylık açısından 1'ler ve 0'lar kullanan bir gösterime çevrilip hizalama dizisi (alignment_string) olarak yeniden adlandırılmıştır. 1'ler WC etkileşimini temsil ederken 0'lar boşta kalan nükleotitleri temsil eder.

Bu hizalama dizisi temel alınarak toplam baz çifti (base pair) sayısı, çekirdek (seed) bölgesindeki baz çifti sayısı, çekirdek bölgesindeki baz çiftlerinin diziliminden elde edilen çekirdek tipi (seed_type) elde edilmiştir. Ayrıca CLASH verisetinden gelen baz çifti sayısı ve çekirdek baz çifti sayısı değerleri ile RNADuplex ile hesaplanan baz çifti değerlerinin farkları da birer öznitelik olarak eklenmiştir.

Her satırdaki olgun mRNA'nın adı ve MRE koordinatları kullanılarak etkileşimde bulunan bölgenin sekans bilgisi (mre_region), olgun mRNA MRE başlangıç (mre_start) ve bitiş (mre_end) koordinatları hesaplanmıştır.

Her satırdaki miRNA'nın adı kullanılarak o miRNA'lara dair şu öznitelikler verisetine eklenmiştir; miRNA sekans uzunluğu ve TargetScan'den (Agarwal et al., 2015) elde edilen, o miRNA'nın evrimsel korunumunu simgeleyen sayısal değer.

Hedef yoğunluğu (target abundance, TA) değeri, Garcia et al. (2011) tarafından ortaya konan ve  Agarwal et al. (2015) tarafından her miRNA için hesaplanan, o miRNA'nın bütün 3' UTR'larda olan bilinen etkileşim yerlerini sembolize eden bir değerdir. Çekirdek bağlanma stabilitesi (seed pairing stability, SBS) değeri de yine Garcia et al. (2011) tarafından ortaya konan ve  Agarwal et al. (2015) tarafından olası her miRNA çekirdek sekansı için hesaplanmış, o çekirdeğin bağlantı sırasındaki termodinamik stabilitesini simgeleyen bir değerdir. Bu değerler de öznitelik olarak eklenmiştir.

Çekirdek bölgesinin yapısını sembolize eden 6mer, 7mer, 8mer, 8mer-1-mismatch gibi öznitelikler de 1/0 şeması kullanılarak eklenmiştir. Bu öznitelikler tasarlanırken, Steinkraus et al. (2016) makalesi 1. figür örnek olarak kullanılmıştır.

AU içeriği, miRNA bağlanmasında ve miRNA-mRNA kompleksinin stabilitesinde önemli bir rol oynar (Grimson et al., 2007). MRE bölgesinin ve 30'ar nükleotit çevresindeki bölgenin AU içeriği hesaplanarak yeni birer kolon olarak eklenmiştir.

Bir MRE'nin yakın çevresinde aynı miRNA'nın başka bir MRE'si olma durumu, bu iki MRE'nin sinerjik çalışıp etkilerinin artmasına sebep olur (Sætrom et al., 2007). Bu yüzden, her MRE için, eğer 13-35 nükleotit mesafede aynı miRNA'nın başka bir MRE'si tespit edilirse bu veri 1/0 şeması kullanılarak eklenmiştir.

MRE'nin, olgun mRNA transkriptinin neresinde olduğu da gen represyonu açısından önemli bir veridir (Grimson et al., 2007). Olgun mRNA'nın iki ucuna doğru olan MRE'lerin, ortasında olan MRE'lere göre daha etkili olduğu görüldüğü için, MRE'nin, olgun mRNA üzerindeki görece pozisyonu da ek bir öznitelik olarak eklenmiştir.

## Ekstrem Gradyan Arttırma (Extreme Gradient Boosting, XGBoost) modeli eğitilmesi

Hazırlanan veriseti, XGBoost algoritmasına verilerek eğitimi sağlanmıştır. Eğitim sırasında verisetinin %80'i eğitim için, geri kalanı ise test için ayrılmıştır. Bu ayırma uygulanırken pozitif ve negatif verilerin, gruplara eşit miktarda dağıldığından emin olunmuştur. Eğitimden önce, nümerik öznitelikler 0 ile 1 arasına sıkıştırılıp, çok büyük sayısal verilerin tahmini etkilemesinin öüne geçilmek istenmiştir.

Eğitim gerçekleştikten sonra, eğitimin detaylarını incelemek amacıyla Lundberg ve Lee (2017) tarafından geliştirilmiş SHAP (Shapley Eklemeli Açıklamalar) metodolojisi kullanılmış ve eğitimde kullanılan her özniteliğin, sonuç tahmin etmeye katkısı test edilmiştir. Kullanılan iki tane özniteliğin, tahmine katkısı olmadığı tespit edildiği için MRE'nin olgun mRNA üzerindeki göreli pozisyonu ve yakındaki aynı miRNA'nın diğer MRE'lerini sembolize eden öznitelikler verisetinden çıkarılmıştır.

Ayrıca, kullanılan özniteliklerin birbirleriyle olan korelasyonları kontrol edilerek, birbirine çok yakın özniteliklerin tespiti amaçlanmıştır. Yakındaki AU içeriği ve MRE AU içeriği dışında, birbirine çok yakın öznitelikler tespit edilmemiştir. Bu durum, genomların belirli bölgelerinin benzer GC içeriğine sahip olmasından kaynaklanmaktadır (Pozzoli et al., 2008) (Romiguier & Roux, 2017).

Birden fazla eğitim deneyi yapılarak, bu deneylerde farklı değişkenleri değiştirerek, yüksek performanslı bir XGBoost modeli oluşturmak hedeflenmiştir. Yapılan deneylerden bazıları şunlardır:
- Negatif verinin çekirdek tipinin 0 olarak işaretlenmesi 
- Düşük öneme sahip özniteliklerin çıkarılması
- Yüksek korelasyona sahip özniteliklerin çıkarılması
- Tahmine en çok katkı sağlayan gibbs serbest enerjisi kolonunun çıkarılması
- Her özniteliğin tek tek çıkarılıp, eğitim sonuçlarının karşılaştırılması

Ayrıca, yapılan her deney için, üstdeğişken ince ayarı (hyperparameter tuning) işlemi yapılıp, eğitim oranı (learning rate) ve maksimum derinlik gibi farklı değişkenlerin model üzerindeki etkileri gözlenmiştir.

Yapılan bütün eğitim deneylerinin sonuna en performanslı model, json dosyasına sonra tahminde kullanmak üzere kaydedilmiştir.


# Kanser Mutasyonlarının Analizi

Nik-Zainal et al. (2016) çalışmasında paylaşılan 560 meme kanseri hastası mutasyonlarının her biri üzerinde uygulanan adımlar aşağıda belirtilmiştir.

## vcf dosyasının ön işlenmesi

Mutasyonların bulunduğu variant call (vcf) dosyalarındaki kromozom:pozisyon koordinatları ve mutasyon öncesi bulunan nükleotitler elimizdeki genom ile karşılaştırılarak uyumsuz örnek çıkması durumunda sonra analiz etmek amacıyla ayrı bir dosyaya kaydedilir. Bir sonraki adımda verilen koordinatın bir miRNA genine düşüp düşmediği kontrol edilir. MiRNA genine düşmeyen mutasyonlar tip 1, miRNA genine düşen mutasyonlar tip 2 olarak sınıflandırılır.

## Tip 1 mutasyonların analizi

Genomik koordinatlar ve mutasyon öncesi/sonrası nükleotitler kullanılarak, mutasyon bölgesinden iki yöne doğru 30'ar nükleotitlik bölgeyi kapsayan doğal ve mutasyona uğramış sekans dizileri elde edilir. Elimizdeki her mutasyon için, elimizdeki her bilinen insan miRNA'sı için sekans ikilileri hazırlanıp bu ikililer RNADuplex adlı programa gönderilip sonuçlar alınır. Aynı işlem hem doğal sekans için, hem de mutasyona uğramış sekans için gerçekleştirilir. RNADuplex, gönderilen 61 nükleotitlik bölge içerisinde o miRNA'nın bağlanabileceği en stabil koordinatları ve o bağlantının enerjisi ve nokta parantez şemasını hesaplar. Sonra her mutasyon için, en iyi bağlanmayı sağlayan kısmının MRE sekansı hesaplanır. Bu MRE sekansı ve RNADuplex çıktıları kullanarak, bir önceki "Öznitelik Mühendisliği" paragrafında yer alan metotlar tekrar uygulanıp veriseti, XGBoost modelimiz ile tahmine uygun hale getirilir. Elimizdeki her miRNA-mRNA ikilisi adayı, XGBoost modelimiz kullanılarak bağlanma olur-bağlanma olmaz diye sınıflandırılır. Bu işlem sonucunda elimizde miRNA-mRNA ikilisi adayları ve onların etkileşim kurma olasılığı verisi (0-1 arasında) bulunmaktadır. Bu etkileşim kurma olasılığı eğer 0.5'in altında ise bağlanma yoktur, üstünde ise bağlanma vardır kabul edilir.

## Tahmin sonuçlarının anlamlandırılması

Bir önceki basamakta üretilen miRNA-mRNA etkileşim adayları, vcf dosyasındaki her mutasyon için kendi içinde gruplandırılıp mutasyonun bağlanma olasılığına olan etkisi kontrol edilir. Mutasyonun etkileşim dinamiğini değiştirmediği hesaplanan girdiler filtrelenir ve geriye mutasyonun etkileşim dinamiğini değiştirdiği düşünülen miRNA-mRNA ikilileri kalır.

Her ikili için XGBoost olasılıklarının farkı hesaplanır. Eğer mutasyon öncesi miRNA etkileşimi yoksa ve mutasyon sayesinde bu etkileşim oluştu ise, o mutasyona fonksiyon kazanımı (gain of function, GoF) mutasyon etiketi, tam tersine ise fonksiyon kaybı (loss of function, LoF) mutasyon etiketi verilir. Böylelikle hangi mutasyonun, hangi miRNA'nın etkileşim dinamiklerini değiştirdiği açığa çıkarılmış olur.

Elimizdeki her anlamlı mutasyon-miRNA-mRNA girdisi için, analizde gereken öznitelikler tekrardan hesaplanır. Bunun için, mRNA'yı kodlayan gen isimleri ve o genler hakkında literatürden toplanan muhtelif detaylar, miRNA isimleri ve o miRNA'lar hakkında literatürden toplanan muhtelif detaylar analiz verisetine eklenir.

## Tip 2 mutasyonların analizi [needs discussion]

Tip 2 mutasyonlar, mRNA yerine miRNA sekansında değişime sebep olduğu için farklı bir yaklaşıma ihtiyaç vardır. Her miRNA'nın mutasyon öncesi ve sonrası sekansları hazırlanır. Bu sekanslar kullanılarak, hücre içinde ifade edildiği bilinen bütün RNA dizileri ile eşleştirilip, mutasyon öncesi ve sonrası ikililer RNADuplex kullanılarak işlemden geçirilir.