---
id: 92
title: iOS Google Places API Entegrasyonu
date: 2016-09-15T16:06:52+01:00
author: Busra Deniz
layout: post
guid: http://busradeniz.com/?p=92
permalink: /ios-google-places-api-entegrasyonu/
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
  - "1528594514"
socialcount_LAST_UPDATED:
  - "1528594514"
image: /wp-content/uploads/2017/07/ios_places_api_title-825x510.jpg
categories:
  - iOS
  - Mobile
tags:
  - ios
  - ios anlik konum
  - ios current location
  - ios google maps
  - ios lokasyon alma
  - ios place picker
  - ios places api
  - ios yakin yerleri alma
  - swift google maps
  - swift lokasyon alma
  - swift place picker
  - swift turkce
---
<img class="aligncenter size-full wp-image-93" src="http://busradeniz.com/wp-content/uploads/2017/07/ios_places_api_title.jpg" alt="" width="960" height="640" srcset="https://www.busradeniz.com/wp-content/uploads/2017/07/ios_places_api_title.jpg 960w, https://www.busradeniz.com/wp-content/uploads/2017/07/ios_places_api_title-300x200.jpg 300w, https://www.busradeniz.com/wp-content/uploads/2017/07/ios_places_api_title-768x512.jpg 768w, https://www.busradeniz.com/wp-content/uploads/2017/07/ios_places_api_title-600x400.jpg 600w" sizes="(max-width: 960px) 100vw, 960px" />

<p class="p3">
  <span class="s2">Android ortamında Google Places API&#8217;nin nasıl entegre edileceğinden </span><a href="http://busradeniz.com/android-google-places-api-entegrasyonu/"><span class="s3"><b>burda</b></span></a><span class="s2"> bahsetmiştim, bahsederken Places API&#8217;nin getirdiği avantajlarına ve limitlerine değinmiştim. Bu nedenle tekrar burda tekrar açıklamayıp, direkt olarak iOS platformunda nasıl kullanılacağından bahsedeceğim.</span>
</p>

## <span class="s2">Places API kütüphanesinin eklenmesi</span> {.p4}

<p class="p3">
  <span class="s2">Places API kütüphanelerini </span><a href="https://www.gstatic.com/cpdc/2b9e8b99fc05d124-GooglePlaces-2.0.1.tar.gz"><span class="s3"><b>manuel olarak da indirip</b></span></a><span class="s2"> projenize ekleyebilirsiniz ama ben CocoaPods kullanarak devam etmeyi tercih ettim. İlk olarak <b>Pod.file</b> dosyamıza aşağıdaki şekilde gerekli kütüphaneleri ekliyoruz :</span>
</p>

<p class="p3">
  <span class="s2"><i>(</i><strong><em>ios_places_api_sample</em></strong> yerine sizin kendi projenizin ismi gelmeli )</span>
</p>

<pre class="lang:default decode:true ">source 'https://github.com/CocoaPods/Specs.git'
target 'ios_places_api_sample' do
  pod 'GooglePlaces'
  pod 'GooglePlacePicker'
  pod 'GoogleMaps'
end</pre>

<p class="p5">
  <p class="p3">
    <span class="s2">Ardından projemizin klasörüne girip, pod install komutunu çalıştırıp kütüphanelerin indirilmesini bekliyoruz.</span>
  </p>
  
  <pre class="lang:default decode:true">pod install</pre>
  
  <p class="p3">
    <span class="s2">Ben burda şu şekilde bir hata ile karşılaştım vecocoapods klasörünün içine girip <b>**git pull**</b> yaptığımda çözüldü. Bu hata sizde görülmeyebilir, benim cocoapods sürümümle ilgili bir sorundu.</span>
  </p>
  
  <p class="p3">
    <span class="s2"><b>Hata</b> : Unable to find a specification for </span><span class="s3"><i>GooglePlacePicker</i></span>
  </p>
  
  <pre class="lang:default decode:true">~/.cocoapods/repos/master

git pull</pre>
  
  <p class="p3">
    <span class="s2">Başarılı bir şekilde tamamlanan <b>pod install</b> komutundan sonra artık api anahtarımızı oluşturup projemize eklememiz gerekiyor. </span><a href="https://console.developers.google.com/"><span class="s3"><b>Google Console</b></span></a><span class="s2">&#8216;dan yine oluşturduğumuz proje için <b>iOS key</b> seçeneğini seçerek api anahtarınızı üretebilirsiniz.</span>
  </p>
  
  <p class="p3">
    <span class="s2">Ardından AppDelegate.swift dosyasında didFinishLaunchingWithOptions methodunun içerisinde api anahtarımızı ekliyoruz.</span>
  </p>
  
  <pre class="lang:default decode:true ">import GooglePlaces</pre>
  
  <pre class="lang:default decode:true ">GMSPlacesClient.provideAPIKey("API_KEY");</pre>
  
  <p class="p5">
    <p class="p3">
      <span class="s2">Benim için yine işler çok düzgün gitmedi ve api anahtarını yukarıdaki gibi kullanıp uygulamayı çalıştırdığımda şöyle bir hata aldım : </span>
    </p>
    
    <p class="p3">
      <span class="s2"><b>Hata :</b> Terminating app due to uncaught exception &#8216;GMSServicesException&#8217;, reason: &#8216;Google Maps SDK for iOS must be initialized via </span><span class="s3"><i>`[GMSServices provideAPIKey:&#8230;]`</i></span><span class="s2"> prior to use&#8217;</span>
    </p>
    
    <p class="p3">
      <span class="s2">Uygulamamın Google Console&#8217;daki özelliklerini ve yaptığım adımları tekrar gözden geçirdim ama problemi ancak GMSServices provideAPIKey methodunu da çağırarak çözebildim.</span>
    </p>
    
    <p class="p5">
      <pre class="lang:default decode:true">GMSServices.provideAPIKey("API_KEY");</pre>
      
      <p class="p3">
        <span class="s2">Henüz mantıklı bir cevap bulabilmiş değilim, sorunu tam anladığımda burayı da güncelleyeceğim.</span>
      </p>
      
      <p class="p3">
        <span class="s2">Bu işlemin de sonunda artık kütüphanelerimizi kullanabilir hale geliyoruz. O zaman Place Picker&#8217;ı uygulamamıza ekleyerek başlayalım.</span>
      </p>
      
      <h2 class="p4">
        <span class="s2">Place Picker</span>
      </h2>
      
      <p class="p3">
        <span class="s2">Benim örnek uygulamamda <b><i>Select Place </i></b>butonuna tıkladığımızda  <b>place picker</b> ekranı açılıyor ve kullanıcı istediği lokasyonu seçtiğinde, lokasyon bilgisi ekrana yazdırılıyor. Place picker kullanmanız için uygulamanızda lokasyon kullanım izinlerini almanız gerekiyor.</span>
      </p>
      
      <p class="p3">
        <span class="s2">( <b><i><a href="https://github.com/busradeniz/ios_places_api_sample/blob/master/ios_places_api_sample/LocationManager.swift">LocationManager</a> </i></b>benim anlık konumu almak için bu projede oluşturduğum bir sınıf, siz istediğiniz şekilde anlık konumu alıp burda <b>latitude</b> ve <b>longitude</b> değerlerine tanımlayabilirsiniz. )</span>
      </p>
      
      <pre class="lang:default decode:true">var placePicker: GMSPlacePicker?

func openPlacePickerView() -&gt; Void {

        let (latitude, longitude) = LocationManager.sharedInstance.getLocation();

        let northEast = CLLocationCoordinate2DMake(latitude + 0.001, longitude + 0.001)

        let southWest = CLLocationCoordinate2DMake(latitude - 0.001, longitude - 0.001)

        let viewport = GMSCoordinateBounds(coordinate: northEast, coordinate: southWest)

        let config = GMSPlacePickerConfig(viewport: viewport)

        placePicker = GMSPlacePicker(config: config)

        placePicker?.pickPlaceWithCallback({ (place: GMSPlace?, error: NSError?) -&gt; Void in

            if let error = error {

                print("Place Picker error: \(error.localizedDescription)")

                return

            }

            if let selectedPlace = place {

                print("Place name : \(selectedPlace.name)  - place address : \(selectedPlace.formattedAddress)" );

                self.lblName.text = selectedPlace.name

                self.lblAddress.text = selectedPlace.formattedAddress!.componentsSeparatedByString(", ").joinWithSeparator("\n")

            }

        })

    }

</pre>
      
      <p class="p3">
        <span class="s2">Place picker uygulamanızda şu şekilde görülecek :</span>
      </p>
      
      <table style="border:none;">
        <tr style="border:none;">
          <td style="border:none;">
            <img class="aligncenter wp-image-107" src="http://busradeniz.com/wp-content/uploads/2017/07/place_picker_ios_1-576x1024.png" alt="" width="338" height="600" srcset="https://www.busradeniz.com/wp-content/uploads/2017/07/place_picker_ios_1-576x1024.png 576w, https://www.busradeniz.com/wp-content/uploads/2017/07/place_picker_ios_1-576x1024-169x300.png 169w, https://www.busradeniz.com/wp-content/uploads/2017/07/place_picker_ios_1-576x1024-225x400.png 225w" sizes="(max-width: 338px) 100vw, 338px" />
          </td>
          
          <td style="border:none;">
            <img class="aligncenter wp-image-108" src="http://busradeniz.com/wp-content/uploads/2017/07/place_picker_ios_2-576x1024.png" alt="" width="338" height="600" srcset="https://www.busradeniz.com/wp-content/uploads/2017/07/place_picker_ios_2-576x1024.png 576w, https://www.busradeniz.com/wp-content/uploads/2017/07/place_picker_ios_2-576x1024-169x300.png 169w, https://www.busradeniz.com/wp-content/uploads/2017/07/place_picker_ios_2-576x1024-225x400.png 225w" sizes="(max-width: 338px) 100vw, 338px" />
          </td>
          
          <td style="border:none;">
            <img class="aligncenter wp-image-109" src="http://busradeniz.com/wp-content/uploads/2017/07/place_picker_ios_3-576x1024.png" alt="" width="338" height="600" srcset="https://www.busradeniz.com/wp-content/uploads/2017/07/place_picker_ios_3-576x1024.png 576w, https://www.busradeniz.com/wp-content/uploads/2017/07/place_picker_ios_3-576x1024-169x300.png 169w, https://www.busradeniz.com/wp-content/uploads/2017/07/place_picker_ios_3-576x1024-225x400.png 225w" sizes="(max-width: 338px) 100vw, 338px" />
          </td>
        </tr>
      </table>
      
      <h2 class="p4">
        <span class="s2">Anlık konum – Etrafımdaki Yerler</span>
      </h2>
      
      <p class="p3">
        <span class="s2">Places API ile birlikte kullanıcının anlık konumunu ve konuma bağlı olarak etrafındaki yerleri elde edebilirsiniz. Bunun için kullanıcıdan <b>lokasyon izni</b> almanız gerekiyor.</span>
      </p>
      
      <p class="p3">
        <span class="s2">Ardından <b>GMSPlacesClient</b> örneğini oluşturup <b>currentPlaceWithCallback</b> methodu ile birlikte kullanıcının etrafındaki yerlere ulaşabilirsiniz. <b>currentPlaceWithCallback</b> methodu <b>GMSPlaceLikelihood</b> listesi dönecektir, her GMSPlaceLikelihood objesi bir yer bilgisi ve benzerlik oranı içerir. Benzerlik oranı (likelihood) ne kadar yüksekse bulunduğu konum olma olasılığı daha yüksek anlamına gelir.</span>
      </p>
      
      <pre class="lang:default decode:true ">var placesClient: GMSPlacesClient?

func getCurrentPlace() {

        placesClient = GMSPlacesClient.sharedClient();

        placesClient?.currentPlaceWithCallback({(placeLikelihoodList: GMSPlaceLikelihoodList?, error: NSError?) -&gt; Void in

            if let error = error {

                print("Pick Place error: \(error.localizedDescription)")

                return

            }

            if let placeLikelihoodList = placeLikelihoodList {

                for place in placeLikelihoodList.likelihoods {

                    let selectedPlace = place.place as GMSPlace;

                    print("Place Name : \(selectedPlace.name) - \(selectedPlace.formattedAddress)");

                    self.lblPlaces.text = self.lblPlaces.text?.stringByAppendingString(selectedPlace.name + " \n ");

                }

            }

        })

    }</pre>
      
      <h2 class="p4">
        <span class="s2">Place Autocomplete</span>
      </h2>
      
      <p class="p3">
        <span class="s2"><img class="alignleft size-medium wp-image-110" src="http://busradeniz.com/wp-content/uploads/2017/07/places_api_autocomplete_1-300x276.png" alt="" width="300" height="276" srcset="https://www.busradeniz.com/wp-content/uploads/2017/07/places_api_autocomplete_1-300x276.png 300w, https://www.busradeniz.com/wp-content/uploads/2017/07/places_api_autocomplete_1-768x708.png 768w, https://www.busradeniz.com/wp-content/uploads/2017/07/places_api_autocomplete_1-434x400.png 434w, https://www.busradeniz.com/wp-content/uploads/2017/07/places_api_autocomplete_1.png 931w" sizes="(max-width: 300px) 100vw, 300px" />Autocomplete bileşeni ise kullanıcıdan alınan arama anahtarına göre GMSPlace objelerini geri döndürür. Kullanıcı seçtiği yer nesnesi ile yer ile ilgili ayrıntılı bilgileri elde edebilir. Autocomplete servisini bir UI elemanı olarak uygulamanıza ekleyebilir ya da sadece kodun içerisinde çağırarak kullanabilirsiniz. Arayüz elemanı olarak kullanmak istediğinizde de farklı şekillerde ekleme ve arayüzü </span><a href="https://developer.apple.com/library/ios/documentation/UIKit/Reference/UIAppearance_Protocol/index.html"><span class="s3"><b>UIAppearance protokol</b></span></a><span class="s2"> kullanarak kendinize göre değiştirme şansınız var. Ben yandaki şekilde eklemeyi tercih ettim ama hem arayüz olarak farklı şekillerde ekleyebilir hem de <b>GMSPlacesClient</b>&#8216;ın <b>autocompleteQuery:bounds:filter:callback</b> methodu ile kod tarafında da yer bilgilerini çekebilir ve kullanabilirsiniz.</span>
      </p>
      
      <p class="p3">
        <span class="s2">Ben <b>GMSAutocompleteViewController</b> kullanarak ilerleyeceğim. UISearchController oluşturarak searchResultController parametresi olarak GMSAutocompleteViewController veriyoruz ve bunu ekrana ekliyoruz.</span>
      </p>
      
      <p class="p5">
        <pre class="lang:default decode:true ">var resultsViewController: GMSAutocompleteResultsViewController?

var searchController: UISearchController?

var resultView: UITextView?

override func viewDidLoad() {

        super.viewDidLoad()

        resultsViewController = GMSAutocompleteResultsViewController()

        resultsViewController?.delegate = self;

        searchController = UISearchController(searchResultsController: resultsViewController)

        searchController?.searchResultsUpdater = resultsViewController

        let subView = UIView(frame: CGRectMake(0, 75, self.view.frame.size.width, 60.0))

        subView.addSubview((searchController?.searchBar)!)

        self.view.addSubview(subView)

        searchController?.searchBar.sizeToFit()

        searchController?.hidesNavigationBarDuringPresentation = false

        self.definesPresentationContext = true

}</pre>
        
        <p class="p3">
          <span class="s2">Arama sonuçlarını ve hata durumlarını yönetebilmek için ise GMSAutocompleteResultsViewControllerDelegate protokolünü uygulamanız gerekir.</span>
        </p>
        
        <pre class="lang:default decode:true ">class AutoCompleteViewController: UIViewController , GMSAutocompleteResultsViewControllerDelegate</pre>
        
        <pre class="lang:default decode:true ">func resultsController(resultsController: GMSAutocompleteResultsViewController, didAutocompleteWithPlace place: GMSPlace) {

        searchController?.active = false

        print("Place name: ", place.name)

        print("Place address: ", place.formattedAddress)

    }

    func resultsController(resultsController: GMSAutocompleteResultsViewController,

                           didFailAutocompleteWithError error: NSError){

        print("Error: ", error.description)

    }

    func didRequestAutocompletePredictionsForResultsController(resultsController: GMSAutocompleteResultsViewController) {

        UIApplication.sharedApplication().networkActivityIndicatorVisible = true

    }

    func didUpdateAutocompletePredictionsForResultsController(resultsController: GMSAutocompleteResultsViewController) {

        UIApplication.sharedApplication().networkActivityIndicatorVisible = false

    }</pre>
        
        <p class="p5">
          <h2 class="p4">
            <span class="s2">Google Places API Kullanım Limiti</span>
          </h2>
          
          <p class="p3">
            <span class="s2">Google Places API&#8217;nin maalesef ücretsiz kullanım için limiti var. Günde 1000 sorgu olan bu limiti aştığınızda uygulamanızda hatalarla karşılaşabilirsiniz. Eğer çok fazla sorgu isteği alacak olan bir uygulamanız var ise ücretli versiyonlara geçmeniz gerekir. Bu sorgu limiti yakın yerlerin sorgusu, autocomplete sorgularının toplamı olarak hesaplanıyor. PlacePicker kullanımı bu limite dahil değil, onu sınırsız şekilde kullanabilirsiniz.</span>
          </p>
          
          <p class="p1">
            <span class="s1">Bu yazıdaki örnek projeyi de </span><a href="https://github.com/busradeniz/ios_places_api_sample"><span class="s2"><b>https://github.com/busradeniz/ios_places_api_sample</b></span></a><span class="s1"> linkinden indirip inceleyebilirsiniz.</span>
          </p>