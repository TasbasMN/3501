Projemizin bu basamağı, kanser gelişiminde kritik roller oynayan mikroRNA'lar (miRNA'lar) ile mutasyonel imzalar arasındaki karmaşık ilişkiyi anlamayı amaçlamaktadır. Çalışmamız, mutasyonların ve onların bıraktığı mutasyonel imzaların miRNA-mRNA etkileşimleri üzerindeki etkilerini sistematik olarak inceleyerek, kanser biyolojisine yeni bir bakış açısı getirmeyi hedeflemektedir. Bu araştırma, kanser genomik verilerinin daha derinlemesine analizini sağlayarak, potansiyel olarak yeni terapötik hedeflerin belirlenmesine ve kişiselleştirilmiş tıp uygulamalarının geliştirilmesine katkıda bulunmayı hedeflemektedir.
# giriş

MiRNA'lar, gen ekspresyonunun düzenlenmesinde kritik roller oynayan küçük kodlamayan RNA'lardır (Catalanotto et al., 2016). MiRNA işlevinin bozulması, kanser dahil çeşitli hastalıklarla ilişkilendirilmiştir. Kanser özelinde, belirli miRNA'lar onkogen ve tümör baskılayıcı olarak işlev görebilir (MacFarlane & R. Murphy, 2010). Kanser genomlarındaki somatik mutasyonlar, miRNA bağlanma bölgelerini etkileyebilir ve potansiyel olarak miRNA aracılı gen düzenlemesini değiştirerek tümör oluşumuna katkıda bulunabilir. 

Canlılarda gözlemlenen mutasyonlar, çeşitli dış ve iç etkenlerden kaynaklanan mutasyonel süreçler sonucunda ortaya çıkabilir ve her biri kendine özgü bir mutasyonel imza bırakabilir (Alexandrov et al., 2013). Mutasyonel imzalar, kanser genomlarında tespit edilen mutasyon örüntülerini temsil eder ve belirli mutajenik süreçlerin sonucudur. Bu imzalar, farklı kanser türlerinde ve alt tiplerinde karakteristik özellikler sergileyebilir.

# bağlayıcı, neden çalışıyoruz

MiRNA'ların gen ekspresyonundaki kritik rolleri ve mutasyonel imzaların kanser genomlarındaki önemi göz önüne alındığında, bu iki alanın kesişimini incelemek büyük önem taşımaktadır. Ancak, bu karmaşık ilişkiyi incelemek ve anlamak, çeşitli zorlukları beraberinde getirmektedir. Örneğin, mevcut miRNA hedef tahmin araçlarının yüksek yanlış pozitif oranları, kodlamayan genomun ihmal edilmesi ve mutasyonların miRNA etkileşim dinamiklerine etkisinin yeterince ele alınmaması gibi sorunlar, bu alandaki araştırmaları zorlaştırmaktadır. Ayrıca, miRNA-mRNA etkileşimlerini deneysel olarak doğrulamanın teknik zorlukları da bu alandaki ilerlemeyi sınırlandırmaktadır.
# zorluklar

Klasik miRNA-mRNA hedef tahmin araçları genellikle potansiyel bağlanma bölgelerini tanımlamak için gen dizisi tamamlayıcılığını, evrimsel korunumu ve diğer bazı seçilmiş özellikleri kullanır (Peterson et al., 2014). Ancak, bu temel yaklaşımlar yüksek yanlış pozitif oranları ve sınırlı doğruluk gibi önemli sorunlarla karşı karşıyadır. Örneğin, Fridrich ve arkadaşlarının (2019) yaptığı kapsamlı bir analizde, yaygın olarak kullanılan miRNA hedef tahmin araçlarının çok yüksek yanlış pozitif oranları gösterdiği ortaya konmuştur. Bu çalışmaya göre, tahmin edilen hedeflerin %65-85'inin gerçek hedeflerden ziyade gürültü olarak belirlenmiştir.

Mevcut literatürün bir diğer önemli eksikliği, çoğu aracın 3' UTR gibi protein kodlayan bölgelere odaklanıp, kodlamayan genomu ihmal etmesidir (Peterson et al., 2014). Örneğin, popüler miRNA hedef tahmin araçlarından TargetScan (Agarwal et al., 2015) ve miRanda (Betel et al., 2010), analizlerini ağırlıklı olarak 3' UTR bölgelerine yoğunlaştırmakta, bu da potansiyel olarak önemli düzenleyici etkileşimlerin gözden kaçırılmasına neden olmaktadır. 

Ayrıca, mevcut metodolojiler mutasyonların miRNA etkileşim dinamiklerini ve mutasyonel imzalarla olan ilişkilerini yeterince ele almamaktadır. Alexandrov ve arkadaşlarının (2013) çalışmasında tanımlanan mutasyonel imzaların miRNA bağlanma bölgelerindeki etkileri henüz sistematik olarak incelenmemiştir. Bu durum, kanseri oluşturan mekanizmaların etraflıca analiz edilmesinin önüne geçmektedir.

Son olarak, miRNA-mRNA etkileşimlerini deneysel olarak doğrulamak oldukça zorlu bir süreçtir. Örneğin, Helwak ve arkadaşlarının (2013) geliştirdiği CLASH (çapraz bağlama, ligasyon ve hibrit dizileme) protokolünde, okumaların sadece yaklaşık %2'si elde edilebilmiştir (Plotnikova et al., 2019). Bu teknik zorluklar, miRNA'ların biyolojik fonksiyonlarının ve hastalık süreçlerindeki rollerinin tam olarak anlaşılmasını güçleştirmektedir.

# tahmini sınırlayan etmenler

MiRNA-mRNA etkileşimlerini anlamak için kapsamlı ve yüksek çözünürlüklü veri setlerine ihtiyaç vardır. Ancak, mevcut veritabanları ve çalışmalar bu konuda sınırlı kalmaktadır. Örneğin, miRNA-mRNA etkileşim verilerini içeren en kapsamlı veritabanlarından biri olan miRTarBase (Huang et al., 2021), çalışmamız için gerekli olan yüksek çözünürlüklü veriyi sağlamamaktadır. Literatürde, miRNA-mRNA etkileşimlerinin gerçekleştiği genomik koordinatları sunabilen yalnızca iki çalışma bulunmaktadır (Helwak et al., 2013; Moore et al., 2014). 
# önerilen yaklaşım

Yukarıda belirtilen sınırlamaları ele almak için, makine öğrenimi yöntemlerinin tahmin gücünü yeni keşfedilen mutasyonel imzalarla entegre eden yeni bir yaklaşım öneriyoruz. Yaklaşımımızın ana tahmin sürücüsü, yüksek performanslı bir makine öğrenimi yöntemi olan XGBoost (Extreme Gradient Boosting) algoritmasıdır. Chen ve Guestrin (2016) tarafından geliştirilen XGBoost, yüksek tahmin performansı, aşırı öğrenmeye karşı dayanıklılık, özellik önem sıralaması sunması, ve büyük veri setleri üzerinde hız ve verimlilik sağlaması nedeniyle tercih edilmiştir. 

Modelimiz, yüksek çözünürlüklü miRNA-mRNA çiftlerinden derlenmiş bir veri seti üzerinde eğitilmiştir. Bu veri seti, Helwak ve arkadaşlarının (2013) ve Moore ve arkadaşlarının (2014) çalışmalarından elde edilen, miRNA-mRNA etkileşimlerinin gerçekleştiği spesifik genomik koordinatları sunan çallışmalardan oluşturulmuştur. Eğitimde hem sekans hem de yapısal bilgileri yakalayan, literatürden özenle derlenmiş öznitelikler kullanılmıştır.

Somatik mutasyonların miRNA bağlanma davranışını nasıl değiştirdiğini değerlendirmek için, kanser hastalarından alınan mutasyonları dizilere uygulayarak yabanıl tip ve mutasyona uğramış miRNA-mRNA çiftleri hazırlanmıştır. Bu çiftler, eğitilmiş XGBoost sınıflandırıcımızı da içeren iş akışımız kullanılarak analiz edilmiştir. Bu analiz sonunda, hangi mutasyonun hangi miRNA'nın etkileşim profilini değiştirdiği bulunmuştur. 

İş akışımızın bir diğer basamağında, miRNA davranışını değiştirdiği tespit edilen mutasyonları COSMIC veritabanından alınan mutasyonel imza verileriyle eşleştireceğiz. Bu entegrasyon, hangi mutasyonun hangi mutasyonel süreçten kaynaklanabileceğini anlamamıza yardımcı olurken, aynı zamanda düşük seviyeli (low-level) bireysel mutasyonlar ile yüksek seviyeli (high-level) mutasyonel süreçler arasındaki bağlantıyı kurmamızı sağlayacaktır. Böylece, miRNA bağlanmasındaki değişiklikleri belirli mutasyonel süreçlerle ilişkilendirerek, bu mutasyonları ortaya çıkaran biyolojik süreçleri daha iyi anlamayı planlıyoruz. Bu yaklaşım, mutasyonel yükü yeni bir perspektiften gözlemlememize ve kanser gelişimindeki rolünü daha kapsamlı bir şekilde değerlendirmemize olanak tanıyacaktır.

# özgün değer


Çalışmamız, mutasyonel imzaların miRNA-mRNA etkileşimleri üzerindeki etkilerini sistematik olarak analiz eden ilk kapsamlı araştırma olma potansiyeline sahiptir. Metodolojik yeniliğimizin merkezinde, miRNA-mRNA etkileşim tahminlerinin mutasyonel imzalara bağlanması yer almaktadır. 

Yaklaşımımızın bir diğer özgün yönü, protein kodlayan ve kodlamayan genomun tamamını kapsayan geniş ölçekli bir analiz sunmasıdır. Bu, mevcut çalışmaların çoğunlukla kodlayan bölgeye odaklanmasının ilerisine giderek, miRNA düzenlemesinin daha kapsamlı bir resmini çizmemizi sağlayacaktır. 

Tamamen sekans tabanlı olan iş akışımız, kanser ve doku tipinden bağımsız olarak çeşitli hastalıklara ve dokulara uyarlanabilir olacaktır. Bu esneklik, yaklaşımımızın farklı kanser türlerinde kullanılmasına ve potansiyel olarak daha önce bilinmeyen düzenleyici dinamiklerin ortaya çıkarılmasına olanak tanıyacaktır.
