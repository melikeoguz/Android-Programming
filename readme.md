<h3>Android Programlama</h3>

    Bu bölümde android programlamaya dair önemli bilgiler ve hatırlatma yazıları bulunmaktadır.
----
 ![Android Emulator](http://eagle.phys.utk.edu/guidry/android/figs/nexus6Pemulator.png "Android Emulator")

* Eğer uygulamanızı hem yatay hem de dikey modda kullanmak isterseniz **manifest** kısmında **MainActivity** kısmının içine **orientation** yazarken otomatik olarak tamamlanan  `android:screenOrientation` kısmını **sensor** olarak yapabilirsiniz. Böylece kullanıcı ekranı sağa sola çevirdikçe uygulamanızın görünümü de değişecektir.
 
   * Bu adımları yaptığınızda horizontal moddaki görünüm karışık çıkabilir. Bunu engellemek için constraint layoutları hem yatay hem dikey görünüm için ayrı ayrı ayarlayabilirsiniz.
   * Tek yapmanız gereken **activity_main.xml** kısmına tıklayıp **design** sekmesine gelin. Sol üst kısımda `Orientation for Preview` imgesine tıklayıp **Create Landscape Variation** yazısını seçin. Böylelikle uygulamanızın yatay görünümünü de kontrol etmiş olursunuz.

----
<h3>~ Grid Layout ~</h3>

* Birden fazla image'i düzenli olarak yani koordinat ekseni üzerine yerleştirmek isterseniz **Grid Layout** 'u kullanmanız daha iyi olur.
 
  * Bunun için yapmanız gereken, `acivity_main.xml` kısmının **desing** kısmını açın. Sol üstte yer alan arama çubuğuna **grid layout** yazıp indirin. İndirme işlemi tamamlandıktan sonra grid layoutu sürükleyerek uygulamınızın üstüne bırakın.
  * Grid layout kullanırken xml üzerinden değişiklik yapmanız her zaman daha kolay olacaktır. O yüzden `activiy_main.xml`'in **text** kısmına geçerek istediğiniz düzenlemeleri yapabilirsiniz.

----

* Kullanıcı tarafından sisteme kaydedilen bilgileri almak için küçük bir database oluşturabilirsiniz.

  * Bunun için **SharedPrefences** adında bir nesne oluşturup **name** ve **mode** tanımlamanız gerekmektedir.
  *  **Name**, sizin projedeki adınız olup package yazısından sonra yazan **com.** ile başlayan kısımdır. **Mode** ise sadece bu uygulamaya özel olsun diye ayarlanabilir.
  *  Uygulamanıza özel bilgiler tanımlamak için mode bölümüne `Context.MODE_PRIVATE`yazabilirsiniz.
  
  ----
* Import edilmeyen bir özelliği sisteminize import etmek için, fare yardımıyla yazıyı taralı alan içine alıp `alt+ enter` tuşlarına basınız.
----
<h3>~ Edit Text ve Text View ~</h3>

* Programınıza  **edit text** ve **text view** ekleyecekseniz bunları **.java** uzantılı dosyaya da eklemeniz gerekmektedir.

  * Bunun için `EditText editText`, `TextView textView`olarak sisteme tanımlayıp edit texti adlandırdığınız ismi kullanarak `editText= findViewById(R.id.textin idsi)`yazınız.
  * Edit texte veri yazılıp yazılmadığını kontrol etmek için 
         
          ☼ if (!editText.getText().toString().matches( regex: ""))
         
     ifadesini kullanabilirsiniz.
----
<h3>~ Shared Preferences ~</h3>

* Kullanıcının verdiği bir değeri uygulamanız silinene kadar saklamak için **Shared Preferences** kullanmanız gerekmektedir.

>Birden fazla veri kaydetmek istiyorsanız **sharedPreferences** tercih edilmemelidir !
  

 * Integer bir değeri depolamak için `sharedPreferences.edit().putInt("data", degiskenAdi)` yazmalısınız. Ardından kaydetmek için **.apply()** yazmayı unutmayın.
     
   *  Kaydettiğiniz veriyi görüntülemek ve geri getirmek için
         
          sharedPreferences.getInt("data",degiskenAdi)
  
   * Kaydettiğiniz veriyi silmek için
    
         sharedPreferences.edit().remove("data").apply()

    
 > 
 ---   
 <h3>~ Alert Dialog ~</h3>
 
 * Kullanıcıya uyarı mesajları vermek için kullanılan  bir özelliktir. 
 * Bu özelliği kullanabilmek için kodlarınıza **Alert Dialog**'tan aşağıdaki nesne oluşturmanız gerekmektedir.
 
       AlertDialog.Builder alert= new AlertDialog.Builder();
     
    * Uyarı mesajınızın başlığını eklemek için
   
      alert.setTitle( " Baslik Ismi "); 
 * Alert dialog yapısında hazır olarak **positive** ve **negative** butonlar bulunmaktadır. Örneğin ;
     
         alert.setPositiveButton("Yes", new DialogInterface.OnClickListener() {
                    @Override
                    public void onClick(DialogInterface dialog, int which) {
                        
                    }
                }
        )

**OnClickListener**, kullanıcı yes butonuna tıkladığında ne olacağını yazdığımız kısımdır.

***Alert Dialog aşağıdaki gibi görünmektedir.***<br><br>
![Alert Dailog](https://i.ytimg.com/vi/men8GB-7yM0/maxresdefault.jpg "Alert Dialog")

----

<h3>~ Toast Message ~</h3>

* Ekranda uzun veya kısa süreli olarak belirecek olan iletidir. 

 * Eğer uygulamanız açılır açılmaz ekranda bir mesaj belirsin istiyorsanız **onCreate** metodu altına kodlarınızı yazmalısınız.
 * Mesajınızın kısa süreli görüntelenmesi için `Toast.LENGTH_SHORT`,	 uzun süreli görüntülenmesi için `Toast.LENGTH_LONG` yazılmalıdır.
  
        Toast.makeText(MainActivity.this,"Lütfen butonları kullanınız",Toast.LENGTH_LONG).show();
        
***Toast Message aşağıdaki gibi görünmektedir.***<bt><br>
<br>
![Toast Message](https://i0.wp.com/www.mehmetkarakose.com/wp-content/uploads/2016/09/ToastMesaj%C3%96rnek.png "Toast Message")
        
----
<h3>~ Context ~</h3>

* İki tane context çeşiti vardır. Bunlardan bir tanesi **Activity Context** bir diğeri ise **App Context**'tir.
* Activity contexte erişmek için **this** ya da **MainActivity.this** kullanılır. 
* App contexte erişmek için `getApplicationContext()`adındaki metodu kullanmamız gerekir.
* Eğer tüm appi ilgilendiren bir fonksiyon ya da işlem yapacaksanız `getApplicationContext'i`, sadece aktiviteyi ilgilendiren bir işlem yapacaksanız `MainActivity.this` ifadesini kullanmalısınız.
* Yanlış context android stüdyonun hata vermesine yol açar. 
  
     * **this** olarak adlandırdığımız şey this'i kullandığımız classtır.
    
    
     getApplicationContext() ifadesi tüm appi nitelendirdiği için 
     MainActivity.this yerine kullanıldığında uygulamanızda hatalara sebep olmaz !
     
---
<h3>~ Birden Fazla Aktivitenin Eklenmesi ~</h3>

* Projenize yeni bir aktive eklemek için projelerinizi görüntülediğiniz sol kısımda **java** klasörünün altında bulunan **com.android** ile başlayan kısma gelip sağ tık yapın.
* Tıkladıktan sonra **Activity** yazan kısma tıklayıp **Gallery** kısmına tıklayın.
*  Projenizi oluştururken projenizin türünü seçtiğiniz ekran yeniden karşınıza gelecektir. Oradan istediğiniz uygulama türünü seçip ilerleyin.

> Birden fazla aktiveniz olacağı için hangi aktivitenin ana ekran olacağını belirtmek için
> **Launcher Activity** özelliğini aktif etmelisiniz !!

* Yeni açılan aktivitenize isim belirleyerek işlemlerinize devam edebilirsiniz.

* Ekranlar arası geçiş yapabilmek için **Intent** classından obje oluşturmanız gerekmektedir.

      Intent intent= new Intent( AktiviteAdi.this, goruntulenecekEkraninAdi.class);
 
* Intent classından obje oluşturduktan sonra aktivitenizin başlaması için **startActivity** metodunu kullanıp parametre olarak da objeyi metoda göndermelisiniz. 

      startActivity(intent);
      
  ----
  
  <h3>~ Aktiviteler Arası Bigi Aktarımı ~</h3>
  
 * Aktarmak istediğiniz veriyi saklayacak alan oluşturduktan sonra **intent.putEkstra()**
 metodu ile istediğiniz veriyi saklayabilirsiniz.
 
      * putEkstra metodu, bir **anahtar kelime** ve **tutulacak bilginin adını** istemektedir.


   ***Örneğin;***
   
       ----- public class MainActivity extends AppCompatActivity ------
      
      EditText editText;
      String city;
       
       ----- protected void onCreate(Bundle savedInstanceState) -----
       
       editText=findViewById(R.id.editText2);
       city="";
       
       ----- public void example(View view) -----
       
       city=editText.getText().toString();
       
       Intent intent= new Intent(MainActivity.this,Main2Activity.class);
       
       intent.putExtra("input",city);
     
 * Bu işlemleri tamamladıktan sonra sıra, kullanıcı tarafından girilen bilginin tutulup görüntüleneceği classın **onCreate** metodu altında yazılması gereken kısma geliyor.

* Burada oluşturulan intent bilgileri almak amacıyla kullanılmalıdır. Bunun için **getIntent()** metodunu kullanabilirsiniz.

   * > **Intent intent =** getIntent();

* Kullanılacak bilgiyi hafıza tutmak için yeni classın içinde de tanımlama yapmalısınız.
* Tanımlama yapıldıktan sonra intent aracılığıyla tutulan string değerdeki bir bilgiyi **getStringExtra()** metoduyla alabilirsiniz.
  
  * Bu metod, parametre olarak kullanılacak bilgiye atadığımız **anahtar kelimeyi** alır.
  
  * > **String city =** intent.getStringExtra("input");



  <br>  ***Text View içerisinde aldığınız bilgiyi görüntülemek için;*** 
  
      textView.setText(city);
      
  ---

  <h3>~ Aktiviteye Image Eklemek ~ </h3>
  
  * Eklemek istediğiniz resimi indirin.
  * İndirme tamamlandıktan sonra resmi kopyalayıp Android Stüdioyu açıp sol tarafta  bulunan **project** kısmını açın.
  * Project **app** ve **Gradle Script** olmak üzere iki kısımdan oluşmaktadır. App kısmına tıklayıp oradan **res** başlığını açın.
  * Res başlığı altında bulunan **drawable** yazına sağ tıklayıp indirdiğiniz fotoğrafı buraya yapıştırın.
  * Karşınıza **drawable** ve **drawable-v24** seçenekleri çıkacaktır. Drawable seçeneğini işaretleyiniz.
  * Bu işlemler tamamlandıktan sonra **activity_main.xml** sayfasının **design** kısmını açıp **ImageView** ekleyebilirsiniz.<br>
  
        Resmi kaydederken adında Türkçe karakter olmamasına dikkat edin aksi halde sistem hata verecektir !!
  
      ***Tüm adımlar aşağıdaki fotoğrafta görülmektedir.***
  <br><br> 
  ![drawable](http://android-coffee.com/wp-content/uploads/2016/02/image-display.jpg)
  
  <h3>~ Random Bir Sayı Üretmek ~</h3>
  
  * Javada random bir sayı üretmek için var olan bir `Random class` mevcuttur.
  
          Random random = new Random();
    
    şeklinde tanımlama yaparak sayınızın, random classına ait bir değer olacağını belirleyebilirsiniz.
  
  * Eğer rastgele bir değer almasını istediğiniz sayınızın belirli aralıkta olmasını istiyorsanız random classında bulunan `nextInt()`metoduna parametre olarak sınır sayıyı gönderin.<br><br>
  
    *Örneğin 0'dan 9'a kadar bir sayı üretilmesini istiyorsanız aşağıdaki gibi yazabilirsiniz.*<br>
  
         int number = random.nextInt(bound: 9)
 

       
