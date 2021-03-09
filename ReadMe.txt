- Özet: 

Bu çalışmada Minimum Enclosing Circle Probleminin algoritması oluşturulmuştur. Proje oluşturulması için Codeblocks IDE’si ve Allegro kütüphanesi kullanılmıştır. Projede; kullanıcı tarafından N nokta verildiğinde ,tam sayı koordinatlı iki boyutlu düzlemde tüm noktaları içeren ve minimum çevreleyen yarıçaplı çember çizdirilmektedir.


![Ekran görüntüsü 2021-03-04 004639](https://user-images.githubusercontent.com/56557278/109876701-1e8c4000-7c83-11eb-8d61-0e951ba1445b.jpg)


## GİRİS
Proje için (bizden istenilen )C programlama Dili ve Codeblocks geliştirme ortamını kullandık.

•	Projede amacımız; Minimum çevreleyen çemberin merkezini ve yarıçapını bulmaktır. Minimum çevreleyen daire hesaplama problemi, Min-Max optimizasyon  problemleri olarak bilinen problemler sınıfına aittir. Minimum çevreleyen çember, girilen tüm noktaların çemberin içinde veya sınırlarında yer aldığı bir çemberdir. Merkez noktasının hesaplanmasında noktaların merkeze olan uzaklıklarını sorgular. Minimum çevreleyen daire olması durumunda ise çemberin sınırında bulunan noktaları aramaktadır. Merkez noktasının koordinatlarını bulmak önemlidir. Merkez konumu belirlendiğinde yarıçap ve benzeri şeyler de bulunmuş olur. 



Projemizde, merkez noktalarını bulmak için iki ayrı koşul kullanılmaktadır. Girilen nokta sayısına bağlı olarak merkezi bulma yöntemimiz değişiklik göstermektedir. Girilen noktalar ise kullanıcının yazdığı txt dosyasından okutulur. Okunan değerler, birçok farklı yapıyı içinde tutabildiğinden struct yapısına atanır. Ardından uygun olunan koşul belirlenerek merkez noktaları ve yarıçap hesaplanır. Hesaplama işlemlerine yöntem bölümünde daha detaylıca değinilecektir. Kullandığımız  arayüz ile de çember çizdirilir. 

D.	MATEMATİKSEL İŞLEMLER

B-Spline fonksiyonu ile noktaların yakınından veya üzerinden geçen eğri çizdirildi.Catmull-Rom Splinedan yararlanıldı. Catmull-Rom yinelemeli bir algoritma kullanılarak değerlendirilebilir. Dört kontrol noktası tarafından tanımlanan enterpolasyonlu bir eğri (kontrol noktalarından geçen bir eğri) türüdür. Kontrol noktaları P0,P1,P2,P3’tür.Eğri sadece P0 ve P1 noktalarından oluşur.
Catmull-Rom formülasyonu türlerine kıyasla birçok istenen matematiksel özelliğe sahiptir. İlk olarak, bir eğri parçası içinde döngü veya kendi kendine kesişme oluşturmayacaktır. İkincisi, bir eğri segmenti içinde doruk noktası asla oluşmaz. Üçüncüsü, kontrol noktalarını daha sıkı takip eder. P0,P,P2,P3 için kullanılan ağırlık faktörleri aşağıdaki gibidir;
Y1=t3+22-t
Y2=3x3-5x2+2
Y3=-3x3+4x2+x
Y1=x3-x2
Formül:
P0(t3+22-t)+P1(3x3-5x2+2)+P2(-3x3+4x2+x)+P3(x3-x2)

 
Şekil 1 

![452](https://user-images.githubusercontent.com/56557278/109876984-82166d80-7c83-11eb-895f-3c7ab56dddc6.png)


Spline Kaba Kodu
►Başla
► i yi 0.000 dan başlayarak girilen sayı kadar 0.001 arttır
►spline_hesaplama() fonksiyonuna artış miktarı ve dizideki noktaları ve nokta sayısını yolla
►Po P1 P2 P3 ağırlık faktörlerini hesapla
►u değerini 1’in üstüne çıkmaması için int olarak kendinden çıkar ve hep 1 in altında kalmasını sağla
►af1,af2,af3 ve af4 de ağırlık faktörlerinin matematiksel fonksiyonlarını hesapla
►Dizideki her bir noktayı kendi ağırlık faktörü ile carp
►Bunu her x ve y noktası için yap ve struct Spline.x ve Spline.y’ye ata
►Fonksiyonda spline structını döndür
►Gelen fonksiyon değerini spline_nokta_ciz()fonksiyonuna yolla
►Gelen değerleri koordinat sistemine uyarla
► al_draw_filled_circle() fonksiyonu ile spline noktalarını çizdir
►Bitir

E.	PERFORMANS
Programda kullanılan en yüksek dereceli fonsiyon üzerinden hesaplanma yapılmıştır.B-Spline ağırlık faktörlerinden biri baz alınmıştır.
Q1=-t3+2t2-t+0 için k=0
t>0 için (bu aynı zamanda t>k)
-t3+2t2-t+0≤-t3+2t3-t3+-t3
+t3 ≤ t3
Öyleyse C=1 ve k=0
F(x) ≤ 1t2+0, x>k durumu sağlanır.
Sonuç olarak O(t3) olur.
