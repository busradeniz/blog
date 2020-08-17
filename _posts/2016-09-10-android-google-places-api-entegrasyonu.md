---
id: 95
title: Android Google Places API Entegrasyonu
date: 2016-09-10T14:53:49+01:00
author: Busra Deniz
layout: post
guid: http://busradeniz.com/?p=95
permalink: /android-google-places-api-entegrasyonu/
asalah_show_meta:
  - "0"
asalah_show_share:
  - "0"
asalah_show_title:
  - "0"
show_author_box:
  - 'no'
asalah_custom_description:
  - ""
asalah_sidebar_position:
  - "0"
socialcount_TOTAL:
  - "0"
socialcount_facebook:
  - "0"
socialcount_linkedin:
  - "0"
socialcount_reddit:
  - "0"
socialcount_stumbleupon:
  - "0"
social_aggregate_score:
  - "0"
social_aggregate_score_detail:
  - 'a:4:{s:5:"total";d:0;s:13:"social_points";i:0;s:11:"view_points";d:0;s:14:"comment_points";i:0;}'
social_aggregate_score_decayed:
  - ""
social_aggregate_score_decayed_last_updated:
  - "1528667181"
socialcount_LAST_UPDATED:
  - "1528667181"
image: /wp-content/uploads/2017/07/android_places_api_title_2-825x510.jpg
categories:
  - Android
  - Mobile
tags:
  - android
  - android google maps
  - android harita ekleme
  - android konum alma
  - android location
  - android place picker
  - android placepicker
  - android places api
  - android yer ekleme
  - place picker
  - place picker kullanimi
---
<p class="p1">
  <img class="aligncenter size-full wp-image-96" src="http://busradeniz.com/wp-content/uploads/2017/07/android_places_api_title_2.jpg" alt="" width="960" height="640" srcset="https://www.busradeniz.com/wp-content/uploads/2017/07/android_places_api_title_2.jpg 960w, https://www.busradeniz.com/wp-content/uploads/2017/07/android_places_api_title_2-300x200.jpg 300w, https://www.busradeniz.com/wp-content/uploads/2017/07/android_places_api_title_2-768x512.jpg 768w, https://www.busradeniz.com/wp-content/uploads/2017/07/android_places_api_title_2-600x400.jpg 600w" sizes="(max-width: 960px) 100vw, 960px" />
</p>

<p class="p3">
  <span class="s2">Lokasyon ve harita bazlı uygulamalarda harita ile etkileşim gerektiren, yer arama, bulunduğun yeri işaretleme ve etrafındaki yerleri arama gibi işlemler bir miktar sıkıntılı olmuştur. Google burayı daha sorunsuz hale getirmek adına Play Services 7.0 ile Google Places API&#8217;sini biz sevgili geliştiricilerinin kullanımına sundu. Temel olarak Places API&#8217;nin getirdiklerini şöyle sıralayabiliriz :</span>
</p>

<ul style="list-style-type: circle;">
  <li class="p3">
    <span class="s2"><span class="s2"><strong>Place Picker :</strong><i> </i>Places API ile birlikte gelen Place Picker UI elemanı içerisinde yerleşik olarak Google Maps&#8217;i barındırıyor. PlacePicker ile kullanıcınıza şuanki lokasyonunu ve etrafındaki yerleri harita üzerinde gösterip, harita üzerinde herhangi bir lokasyon seçmesini sağlayabilirsiniz.</span></span>
  </li>
  <li class="p3">
    <span class="s2"><span class="s2"><b>Anlık Konum &#8211; PlaceDetectionApi.getCurrentPlace() :</b> Places API ile birlikte kullanıcının anlık konumunu ve etrafında olabilecek yerlerin listesini edinebilirsiniz.</span></span>
  </li>
  <li class="p3">
    <span class="s2"><b>Otomatik Tamamlama :</b> Kullanıcının yazmaya başladığı kelime ile ilgili olası yerleri kullanıcıya göstererek seçim yapmasını sağlayabilirsiniz.</span>
  </li>
</ul>

<p class="p3">
  <span class="s2">Bu ana işlemler dışında Places API ile yerler hakkında ayrıntılı bilgi (isim, adres, lokasyon, id, fotoğraf, vb) çekebilir, yeni yer ekleyebilir veya raporlayabilirsiniz. Görüldüğü gibi kullanıcıdan veri alınırkenki hata payının düşürülmesi üzerine gayet kullanışlı ve yaşanan çoğu probleme çözüm getiriyor.</span>
</p>

<p class="p3">
  <span class="s2">Ben bu yazımda Places API&#8217;nin Place Picker, anlık konum ve otomatik tamamlama özelliklerini nasıl kullanacağımız üzerinde duracağım. Bunun için oluşturduğum örnek projeyi </span><a href="https://github.com/busradeniz/android_places_api_sample"><span class="s3"><b>GitHub</b></span></a><span class="s2">&#8216;dan inceleyebilirsiniz.</span>
</p>

## <span class="s2">Place Picker</span> {.p4}

<p class="p3">
  <span class="s2">Place Picker gömülü olarak içerisinde Google Maps&#8217;i barındıran ve hemen altında kullanıcının etrafındaki yerlerin listesini gösteren UI elemanıdır. Place Picker ile kullanıcı</span>
</p>

<p class="p3">
  <span class="s3"><b>* </b></span><span class="s2"><span class="Apple-converted-space">  </span>Anlık konumunu ve etrafındaki yerleri görüntüleyebilir.</span>
</p>

<p class="p3">
  <span class="s3"><b>* </b></span><span class="s2"><span class="Apple-converted-space">  </span>Harita ile etkileşimde bulunup harita üzerinde istediği lokasyonu ve etrafındaki yerleri seçebilir.</span>
</p>

<p class="p3">
  <span class="s3"><b>* </b></span><span class="s2"><span class="Apple-converted-space">  </span>Arama çubuğu ile yer arayarak harita üzerinde görüntüleyebilir.</span>
</p>

<p class="p3">
  <span class="s2">Basit ve kolay kullanılabilir arayüzü ile kullanıcıdan alınacak olan lokasyon bilgisindeki hatayı minimuma indirmekte ve kullanıcıya esnek bir arayüz sağlamaktadır. Tüm bu harita ve lokasyon işlemleri kendimizin geliştirdiğini düşündüğümüzde geliştirme zamanını da ciddi miktarda azaltmaktadır.</span>
</p>

<table style="border:none;">
  <tr style="border:none;">
    <td style="width: 338px;border:none;">
      <img class="aligncenter wp-image-97" src="http://busradeniz.com/wp-content/uploads/2017/07/place_picker_android_1-576x1024.png" alt="" width="338" height="601" srcset="https://www.busradeniz.com/wp-content/uploads/2017/07/place_picker_android_1-576x1024.png 576w, https://www.busradeniz.com/wp-content/uploads/2017/07/place_picker_android_1-576x1024-169x300.png 169w, https://www.busradeniz.com/wp-content/uploads/2017/07/place_picker_android_1-576x1024-225x400.png 225w" sizes="(max-width: 338px) 100vw, 338px" />
    </td>
    
    <td style="width: 338px;border:none;">
      <img class="aligncenter wp-image-98" src="http://busradeniz.com/wp-content/uploads/2017/07/place_picker_android_2-576x1024.png" alt="" width="338" height="601" srcset="https://www.busradeniz.com/wp-content/uploads/2017/07/place_picker_android_2-576x1024.png 576w, https://www.busradeniz.com/wp-content/uploads/2017/07/place_picker_android_2-576x1024-169x300.png 169w, https://www.busradeniz.com/wp-content/uploads/2017/07/place_picker_android_2-576x1024-225x400.png 225w" sizes="(max-width: 338px) 100vw, 338px" />
    </td>
    
    <td style="width: 338px;border:none;">
      <img class="aligncenter wp-image-99" src="http://busradeniz.com/wp-content/uploads/2017/07/place_picker_android_3-576x1024.png" alt="" width="338" height="601" srcset="https://www.busradeniz.com/wp-content/uploads/2017/07/place_picker_android_3-576x1024.png 576w, https://www.busradeniz.com/wp-content/uploads/2017/07/place_picker_android_3-576x1024-169x300.png 169w, https://www.busradeniz.com/wp-content/uploads/2017/07/place_picker_android_3-576x1024-225x400.png 225w" sizes="(max-width: 338px) 100vw, 338px" />
    </td>
  </tr>
</table>

### <span class="s2">Peki Place Picker&#8217;ı uygulamamıza nasıl entegre ederiz ?</span> {.p4}

<p class="p3">
  <span class="s2">Place Picker&#8217;ı uygulamanıza eklemeden önce Google Places API&#8217;yi kullanabilmeniz için yapmanız gereken işlemler var. Bu hem Place Picker hem de diğer özellikler için geçerli gereklidir.</span>
</p>

<p class="p3">
  <span class="s2">İlk yapmamız gereken işlem olarak </span><a href="https://console.developers.google.com"><span class="s3"><b>Google geliştirici konsolundan</b></span></a><span class="s2"> uygulamanız için Android API key oluşturmanız ve aşağıdaki gibi <i>AndroidManifest.xml</i> dosyanızda belirtmeniz gerekiyor.</span>
</p>

<pre class="top-margin:25 bottom-margin:25 lang:default decode:true" title="AndroidManifest">&lt;meta-data android:name="com.google.android.geo.API_KEY"
android:value="Android_API_Key" /&gt;</pre>

<p class="p3">
  <span class="s2">Ardından tabiki <i>google-playservices-places </i> kütüphanesini dependency olarak <i>build.gradle </i>dosyanıza eklemelisiniz.<br /> </span>
</p>

<pre class="top-margin:25 bottom-margin:25 lang:default decode:true" title="build.gradle">compile 'com.google.android.gms:play-services-places:9.+'</pre>

<p class="p3">
  <span class="s2">Place picker için gerekli olan ACCESS<i>_FINE_</i>LOCATION iznini ekledikten sonra artık kod kısmına geçebilirsiniz.<br /> </span>
</p>

<pre class="lang:default decode:true" title="AndroidManifest.xml">&lt;uses-permission android:name="android.permission.ACCESS_FINE_LOCATION" /&gt;</pre>

<p class="p3">
  <span class="s2">Benim uygulamamda <i>PlacePickerSampleActivity</i> sınıfımın içindeki butona tıklandığında Place Picker açılıyor ve kullanıcı yer seçimini yaptıktan sonra ekranda textview olarak adresi ve yerin ismini yazıyor.</span>
</p>

<p class="p3">
  <span class="s2">Place Picker ekranını açmak için  <b><i>PlacePicker.IntentBuilder </i></b> oluşturarak <b><i>startActivityForResult()</i></b> methoduna parametre olarak veriyoruz. <b><i>startActivityForResult() </i></b>methodunu çağırdığınızda yeni place picker yeni bir activity başlatır ve kullanıcı o ekran üzerinde yer seçimini yapar.</span>
</p>

<p class="p3">
  <span class="s2">Builder&#8217;ın <b><i>setLatLngBounds()</i></b> methodunu kullanarak başlangıç lokasyonunu değiştirebilirsiniz, aksi halde varsayılan olarak cihazın anlık lokasyonunu gösterecektir.</span>
</p>

<pre class="lang:java decode:true ">private static int PLACE_PICKER_REQUEST = 1;

private void openPlacePickerView(){
      PlacePicker.IntentBuilder builder = new PlacePicker.IntentBuilder();
      try {
           startActivityForResult(builder.build(this), PLACE_PICKER_REQUEST);
      } catch (GooglePlayServicesRepairableException e) {
           e.printStackTrace();
      } catch (GooglePlayServicesNotAvailableException e) {
           e.printStackTrace();
      }
}</pre>

&nbsp;

<p class="p3">
  <span class="s2">Place Picker ekranında kullanıcı yer seçimini yaptıktan sonra ekran kapanır ve çağırdığınız activity sınıfının <b><i>onActivityResult() </i></b> methodu tetiklenir. Dönen Intent objesini kullanarak seçilen yerle ilgili bilgileri edinebilirsiniz.</span>
</p>

<p class="p3">
  <span class="s2">Burda dikkat etmeniz gereken nokta, kullanıcı Google Maps üzerinde daha önce tanımlanmamış, rasgele bir lokasyon seçtiğinde isim, address, id gibi değerlere ulaşamayacaksınız. Sadece latitude ve longitude olarak elde edebilirsiniz.</span>
</p>

<pre class="lang:default decode:true ">protected void onActivityResult(int requestCode, int resultCode, Intent data) {

     if (requestCode == PLACE_PICKER_REQUEST) {
           if (resultCode == RESULT_OK) {
                Place place = PlacePicker.getPlace(this, data);
                Log.i(LOG_TAG, String.format("Place Name : %s", place.getName()));

                Log.i(LOG_TAG, String.format("Place Address : %s", place.getAddress()));
                Log.i(LOG_TAG, String.format("Place Id : %s", place.getId()));

                txtPlaceName.setText(String.format("Place : %s - %s" , place.getName() , place.getAddress()));

             }
       }
}</pre>

## <span class="s2">Anlık konum &#8211; Etrafımdaki Yerler</span> {.p4}

<p class="p3">
  <span class="s2">Places API ile <b><i>PlacesDetectionApi.getCurrentPlace()</i></b> methodunu çağırarak kullanıcının etrafındaki yerlerin listesini alabilirsiniz. Google yer bilgilerine benzerlik (likelihood) oranını da ekleyerek dönüyor. Benzerlik oranı 0 ile 1.0 arasında bir değer olarak dönüyor ve sizin kendi kullanım durumunuza göre yorumlamanızı sağlıyor.</span>
</p>

<p class="p3">
  <span class="s2"><b><i>getCurrentPlace()</i></b> methodunu kullanmadan önce <b><i>GoogleApiClient</i></b> örneğini oluşturmanız ve GoogleApiClient.OnConnectionFailedListener arayüzünü implemente etmeniz gerekiyor.</span>
</p>

<pre class="lang:default decode:true">GoogleApiClient googleApiClient = new GoogleApiClient.Builder(this)
                         .addApi(Places.PLACE_DETECTION_API)
                         .addApi(Places.GEO_DATA_API)
                         .enableAutoManage(this, this)
                         .build();</pre>

<p class="p3">
  <span class="s2">Ardından  <b><i>getCurrentPlace()</i></b> çağırarak yer listesini alıyoruz. Method parametre olarak <b><i>GoogleApiClient</i></b> ve <b><i>PlaceFilter</i></b> alıyor. Eğer dönecek olan yer listesinde bir filtreleme yapmak isterseniz <b><i>PlaceFilter</i></b> objesi oluşturarak methoda vermeniz gerekiyor.</span>
</p>

<pre class="lang:java decode:true ">PendingResult&lt;PlaceLikelihoodBuffer&gt; result = Places.PlaceDetectionApi.getCurrentPlace(googleApiClient, null);
result.setResultCallback(new ResultCallback&lt;PlaceLikelihoodBuffer&gt;() {

       @Override
       public void onResult(PlaceLikelihoodBuffer likelyPlaces) {

              Log.i(LOG_TAG, String.format("Result received : %d " , likelyPlaces.getCount() ));
              StringBuilder stringBuilder = new StringBuilder();
              for (PlaceLikelihood placeLikelihood : likelyPlaces) {
                    stringBuilder.append(String.format("Place : '%s' %n",
                    phttp://busradeniz.com/wp-admin/post-new.php#laceLikelihood.getPlace().getName()));
              }

              likelyPlaces.release();
              txtLocation.setText(stringBuilder.toString());
        }
});</pre>

<p class="p3">
  <span class="s2"><b><i>getCurrentPlace()</i></b> methodunu çağırırken lokasyon izin kontrollerine de dikkat etmeniz gerekiyor. Burda sadece method kullanımına odaklandığım için kod örneğinde ona yer vermedim ama tamamını </span><a href="https://github.com/busradeniz/android_places_api_sample"><span class="s3"><b>Github&#8217;daki projeden</b></span></a><span class="s2"> inceleyebilirsiniz.</span>
</p>

## <span class="s2">Place Autocomplete</span> {.p4}

<p class="p3">
  <span class="s2">Place autocomplete ile kullanıcı arama yaparken ilgili sonuçları göstererek seçim yapabilmesini sağlıyor. Aslında Place Picker içerisinde Place Autocomplete servisini kullanıyoruz. Herhangi bir ekranda autocomplete servisini kullanmak için activity sınıfınıza <b>PlaceAutocompleteFragment</b> eklemeniz gerekiyor.<br /> </span>
</p>

<pre class="lang:default decode:true">&lt;fragment
android:id="@+id/fragment_autocomplete"
android:layout_width="match_parent"
android:layout_height="wrap_content"
android:name="com.google.android.gms.location.places.ui.PlaceAutocompleteFragment"
/&gt;</pre>

<p class="p3">
  <span class="s2">PlaceSelectionListener ile de kullanıcının yaptığı seçimleri yönetebilirsiniz.</span>
</p>

<pre class="lang:default decode:true ">PlaceAutocompleteFragment autocompleteFragment = (PlaceAutocompleteFragment)
getFragmentManager().findFragmentById(R.id.fragment_autocomplete);
autocompleteFragment.setOnPlaceSelectedListener(new PlaceSelectionListener() {
         @Override
         public void onPlaceSelected(Place place) {
               Log.i(LOG_TAG, "Place: " + place.getName());
               txtSelectedPlaceName.setText(String.format("Selected places : %s - %s" , place.getName(), place.getAddress()));
         }

         @Override
         public void onError(Status status) {

               Log.i(LOG_TAG, "Place cannot be selected: " + status);
               Toast.makeText(AutoCompleteActivity.this, "Place cannot be selected!!", Toast.LENGTH_SHORT).show();
         }
});</pre>

<table style="border:none;">
  <tr style="border:none;">
    <td style="width: 314px;border:none;">
      <img class="aligncenter wp-image-100" src="http://busradeniz.com/wp-content/uploads/2017/07/autocomplete_android_1-576x1024.png" alt="" width="338" height="601" srcset="https://www.busradeniz.com/wp-content/uploads/2017/07/autocomplete_android_1-576x1024.png 576w, https://www.busradeniz.com/wp-content/uploads/2017/07/autocomplete_android_1-576x1024-169x300.png 169w, https://www.busradeniz.com/wp-content/uploads/2017/07/autocomplete_android_1-576x1024-225x400.png 225w" sizes="(max-width: 338px) 100vw, 338px" />
    </td>
    
    <td style="width: 315px;border:none;">
      <img class="aligncenter wp-image-101" src="http://busradeniz.com/wp-content/uploads/2017/07/autocomplete_android_2-576x1024.png" alt="" width="338" height="601" srcset="https://www.busradeniz.com/wp-content/uploads/2017/07/autocomplete_android_2-576x1024.png 576w, https://www.busradeniz.com/wp-content/uploads/2017/07/autocomplete_android_2-576x1024-169x300.png 169w, https://www.busradeniz.com/wp-content/uploads/2017/07/autocomplete_android_2-576x1024-225x400.png 225w" sizes="(max-width: 338px) 100vw, 338px" />
    </td>
  </tr>
</table>

## <span class="s2">Google Places API Kullanım Limiti</span> {.p4}

<p class="p3">
  <span class="s2">Places API sorguları için her uygulamanın günlük 1000 sorgu için izni var, bu sınır aşıldığında uygulamanız hata vermeye başlayabilir. Eğer bu limit uygulamanız için az ise ücretli versiyonlarına geçerek kullanıma devam edebiliriz. Place Picker kullanımı bu limite bağlı olmamakla birlikte diğer tüm sorguların toplamı günlük olarak 1000&#8217;i geçmemelidir.</span>
</p>

<p class="p3">
  <span class="s2">Benim Places API kullanımım bir üniversite projesi için olmuştu, çok hızlı ve kolay bir şekilde lokasyon bazlı özellikleri tamamlayabilmiştim. Bu yazıdaki örnek projeyi de </span><a href="https://github.com/busradeniz/android_places_api_sample"><span class="s3"><b>https://github.com/busradeniz/android_places_api_sample</b></span></a><span class="s2"> linkinden edinebilirsiniz.</span>
</p>