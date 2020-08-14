---
id: 12
title: WebRTC Nedir ?
date: 2016-07-05T11:17:41+01:00
author: Busra Deniz
layout: post
guid: http://busradeniz.com/?p=12
permalink: /webrtc-nedir/
asalah_show_meta:
  - 'yes'
asalah_show_share:
  - 'yes'
asalah_show_title:
  - "0"
show_author_box:
  - 'no'
asalah_custom_description:
  - ""
asalah_sidebar_position:
  - none
hits:
  - "3"
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
  - "1528590272"
socialcount_LAST_UPDATED:
  - "1528590272"
image: /wp-content/uploads/2017/06/webrtc_title-825x510.png
categories:
  - WebRTC
tags:
  - peer to peer
  - real time communication
  - rtc
  - webrtc
  - webrtc android
  - webrtc chrome
  - webrtc desteklenen platformlar
  - webrtc dokuman
  - webrtc firefox
  - webrtc ios
  - webrtc kaynak
  - webrtc mobile
  - webrtc nedir
  - webrtc safari
  - webrtc supported platforms
  - webrtc türkçe
  - webrtc türkçe blog
  - webrtc türkçe tutorial
  - webrtc tutorial
  - what is webrtc
---
###<img class="alignnone size-full wp-image-14" src="http://busradeniz.com/wp-content/uploads/2017/06/webrtc_title.png" alt="" width="960" height="640" srcset="https://www.busradeniz.com/wp-content/uploads/2017/06/webrtc_title.png 960w, https://www.busradeniz.com/wp-content/uploads/2017/06/webrtc_title-300x200.png 300w, https://www.busradeniz.com/wp-content/uploads/2017/06/webrtc_title-768x512.png 768w, https://www.busradeniz.com/wp-content/uploads/2017/06/webrtc_title-600x400.png 600w" sizes="(max-width: 960px) 100vw, 960px" />  
WebRTC Nedir ? {.graf.graf--figure}

<p class="graf graf--p">
  WebRTC son zamanlarda, özellikle 2015 yılıyla birlikte adını daha da sık duyduğumuz bir teknoloji olmaya başladı. Genellikle Türkiye’deki konferanslarda, etkinliklerde tanıştığım insanların WebRTC’yi ya hiç duymadıklarını ya da sadece isim olarak bildiklerini ama çok bir fikirlerinin olmadığını gözlemledim.
</p>

<p class="graf graf--p">
  Benim WebRTC ile tanışmam ise Netaş’taki işime başlamamla birlikte oldu. 2014 Şubat’ında Netaş’ta Google’ın WebRTC kütüphanesini kullanarak Android ve iOS platformlarında native gerçek zamanlı görüşme sağlayan SDK’ler yazılan bir projeye dahil oldum. Bu zamana kadar hep mobil uygulama geliştirip ve temelde sunucudan veri alıp, binbir çeşit şekilde gösterim döngüsünde ilerlediğim için SDK geliştirme ve hiç bilmediğim WebRTC bana ilginç gelmiş ve sıfırdan başlayan bir projeye dahil olmuştum.
</p>

<p class="graf graf--p">
  Ama işte tembelliğim yine ön plana çıktı ya da hayatın cilvesi midir bilemem, WebRTC ile ilgili ilk blog yazımı 2 yıl çalıştığım projeden ve Netaş’tan ayrıldıktan sonra yazıyorum :)
</p>

<p class="graf graf--p">
  Başlamadan önce şu karışıklığı açıklamak gerek sanırım. WebRTC hem W3C ve IETF organizasyonları tarafından yürütülen ve tanımlanmaya çalışılan bir standarttır hem de bu standart tanımının Google tarafından geliştirilen projesinin ismidir. Standart olarak WebRTC (<a class="markup--anchor markup--p-anchor" href="https://www.w3.org/TR/webrtc/" target="_blank" rel="noopener" data-href="https://www.w3.org/TR/webrtc/">WebRTC 1.0</a>) henüz tamamlanmamış durumda ve güncellenmeye devam ediyor, en güncel WebRTC tanımına <a class="markup--anchor markup--p-anchor" href="https://www.w3.org/TR/webrtc/" target="_blank" rel="noopener" data-href="https://www.w3.org/TR/webrtc/">burdan</a> ulaşabilirsiniz. Benim bu yazıda bahsedeceğim <a class="markup--anchor markup--p-anchor" href="https://webrtc.org/" target="_blank" rel="noopener" data-href="https://webrtc.org/">WebRTC</a> ise Google tarafından geliştirilen ve WebRTC 1.0 spesifikasyonunun bir uygulaması olan açık kaynak projedir. WebRTC’nin Ericsson tarafından geliştirilen <a class="markup--anchor markup--p-anchor" href="http://www.openwebrtc.org/" target="_blank" rel="noopener" data-href="http://www.openwebrtc.org/">OpenWebRTC</a> isimli yine açık kaynaklı uygulaması da bulunmaktadır.
</p>

### Google WebRTC {.graf.graf--h3}

<p class="graf graf--p">
  Şu sıralar <a class="markup--anchor markup--p-anchor" href="https://groups.google.com/forum/#!topic/discuss-webrtc/I0GqzwfKJfQ" target="_blank" rel="noopener" data-href="https://groups.google.com/forum/#!topic/discuss-webrtc/I0GqzwfKJfQ">5. yaşı</a> kutlanan WebRTC projesi Google tarafından 2011 I/O sırasında duyuruldu ve herkese açıldı. WebRTC en temelde peer-to-peer olarak gerçek zamanlı sesli ve görüntülü iletişimi ve data paylaşımını sağlamaktadır.
</p>

<p class="graf graf--p">
  En büyük avantajlarından bir tanesi Chrome, Firefox, Opera gibi oldukça kullanılan tarayıcılarda hali hazırda gömülü olarak gelmesi ve kullanıcıların ekstra hiç bir eklenti yüklemeden WebRTC uygulamalarını direkt olarak tarayıcılarında çalıştırabilmeleridir. WebRTC’nin plugin-free olması sizi uygulama geliştirici olarak güvenlik, eklenti kurma gibi kullanıcılarınıza zorluk yaratacak adımları ortadan kaldırması anlamına geliyor.
</p><figure class="graf graf--figure">

<img class="alignnone size-full wp-image-58" src="http://busradeniz.com/wp-content/uploads/2017/07/webrtc_advantages-1024x529.png" alt="" width="1024" height="529" srcset="https://www.busradeniz.com/wp-content/uploads/2017/07/webrtc_advantages-1024x529.png 1024w, https://www.busradeniz.com/wp-content/uploads/2017/07/webrtc_advantages-1024x529-300x155.png 300w, https://www.busradeniz.com/wp-content/uploads/2017/07/webrtc_advantages-1024x529-768x397.png 768w, https://www.busradeniz.com/wp-content/uploads/2017/07/webrtc_advantages-1024x529-774x400.png 774w" sizes="(max-width: 1024px) 100vw, 1024px" /> </figure> 

<p class="graf graf--p">
  Ayrıca peer-to-peer iletişim sayesinde sisteminizde herhangi bir medya sunucusu bulundurmadan uygulamalarınıza multi-media özelliği kazandırabiliyorsunuz. (Bazı kısıtlı ağ tiplerinde P2P çalışılamadığını ve başka çözümlere ihtiyaç duyacağınızı şimdiden söyleyeyim ama Google’a göre aramaların %86 sı P2P olabiliyor.) SIP (Session Initiation Protocol) gibi bu zamana kadarki telekom dünyası çözümlerinde her zaman bir medya sunucusu bulundurmanız ve devam ettirmeniz gerekiyordu. Bu oldukça pahalı çözümler nedeniyle telekom dünyasında genellikle hep büyük oyuncular rol almış ve iş yapmış ama WebRTC dünyasına baktığınızda birçok WebRTC çözümünü sunmuş ve ciddi yatırımlar, satın almalar olan startuplar göreceksiniz. WebRTC biraz da küçük oyuncuları telekom dünyasına girişini sağlamıştır.
</p>

<p class="graf graf--p">
  Yine SIP gibi telekom çözümlerinde bir uygulama çıkarabilmek için protokole özel bir uzmanlık gerekiyor. SIP alanında çalışmış, çalışma mantığını bilen insanlar ile ancak bir çözüm çıkarabilyorsunuz fakat WebRTC sağladığı basit API ile tüm telekom ve real time iletişim karmaşıklığını size soyutluyor ve bir mobil ya da web geliştiricisi olarak basit bir API kullanımı ile uygulamaya multi-media özelliği ekleyebiliyorsunuz.
</p>

<p class="graf graf--p">
  Son olarak WebRTC ücretsiz ve BSD lisansı ile duyurulmuş açık kaynaklı bir proje, yani istediğiniz şekilde indirip kullanabiliyorsunuz.
</p>

### Desteklenen Platformlar {.graf.graf--h3}

<p class="graf graf--p">
  WebRTC şuan native olarak Chrome, Opera, Firefox, Chrome Android, Firefox Android ve Opera Android tarayıcılarında ve Android ve iOS platformlarında native kütüphane olarak desteklenmektedir. WebRTC özelliklerinin tarayıcı bazında desteklenme durumlarına <a class="markup--anchor markup--p-anchor" href="http://iswebrtcreadyyet.com/" target="_blank" rel="noopener" data-href="http://iswebrtcreadyyet.com/">burdan</a> bakabilirsiniz.
</p>

<p class="graf graf--p">
  Safari’nin WebRTC destekleyeceği düşünülüyor ama henüz hiç bir API’si desteklenir durumda değil, WebRTC için eklenti yazmanız gerekiyor.
</p>

<p class="graf graf--p">
  Microsoft tarafında işler biraz daha ilginç, Google’ın WebRTC’yi duyurmasından sonra Microsoft da <a class="markup--anchor markup--p-anchor" href="http://ortc.org/" target="_blank" rel="noopener" data-href="http://ortc.org/">ORTC</a> projesini duyurmuştu. ORTC Edge’de şuan desteklenir durumda ve WebRTC’yi de destekleyeceği duyuruldu.
</p><figure class="graf graf--figure">

<img class="size-full wp-image-59 aligncenter" src="http://busradeniz.com/wp-content/uploads/2017/07/webrtc_supported_platforms-1024x342.png" alt="" width="1024" height="342" srcset="https://www.busradeniz.com/wp-content/uploads/2017/07/webrtc_supported_platforms-1024x342.png 1024w, https://www.busradeniz.com/wp-content/uploads/2017/07/webrtc_supported_platforms-1024x342-300x100.png 300w, https://www.busradeniz.com/wp-content/uploads/2017/07/webrtc_supported_platforms-1024x342-768x257.png 768w, https://www.busradeniz.com/wp-content/uploads/2017/07/webrtc_supported_platforms-1024x342-940x314.png 940w" sizes="(max-width: 1024px) 100vw, 1024px" /> </figure> 

<p class="graf graf--p">
  Şuan 2 milyardan fazla WebRTC’nin eklentisiz olarak kullanılabildiği kullanıcı sayısından bahsediliyor.
</p>

### WebRTC kullanım durumu, nerelerde kullanılıyor? {.graf.graf--h3}

<p class="graf graf--p">
  Gitgide daha da iyi bir duruma gelen (hala özellikle mobil için bilinen sıkıntıları olsa da) WebRTC aslında günlük hayatta kullandığımız çoğu uygulama tarafından kullanılıyor. Facebook Messenger, Hangouts, Whatsapp, Snapchat, beta durumda olan Slack bunlardan bazıları. Atlassian’ın HipChat i, AT&T’nin müşterilerine açtığı WebRTC API’leri ve Skype for Business’ın WebRTC desteği ile aslında indirme sayısı milyarları geçen WebRTC uygulamalar markette yerini alıyor.
</p>

<p class="graf graf--p">
  Son kullanıcıya yönelik uygulamalar dışında PaaS (Platform-As-A-Service ) şeklinde kendi çözümlerini sunan birçok startup şirket var. CafeX, Tokbox, Twilio, Bistri ve Kandy gibi şirketler kendi WebRTC SDK’lerini müşterilerine sağlayarak daha hızlı ve kolay multi-media entegrasyonu sağlıyorlar. WebRTC’nin sektördeki durumunu daha detaylı olarak <a class="markup--anchor markup--p-anchor" href="https://bloggeek.me/where-webrtc/" target="_blank" rel="noopener" data-href="https://bloggeek.me/where-webrtc/">buradaki</a> yazıdan öğrenebilirsiniz.
</p>

<p class="graf graf--p">
  Geliştirici tarafından bakıldığında ise WebRTC topluluğu diğer teknolojilere göre biraz daha küçük sayılır. Aktif sayılabilecek bir <a class="markup--anchor markup--p-anchor" href="https://groups.google.com/forum/#!forum/discuss-webrtc" target="_blank" rel="noopener" data-href="https://groups.google.com/forum/#!forum/discuss-webrtc">mail grubu</a> bulunuyor fakat kendi sitesi dışında düzenli ve tecrübelerden oluşan blog sayıları çok az. WebRTC ile biraz zaman geçirdikten sonra yaşadığınız sorunların (çok temel problemler hariç) cevabını öyle hemen bulabilmeyi ümit etmeyin :)<a class="markup--anchor markup--p-anchor" href="http://stackoverflow.com/questions/tagged/webrtc" target="_blank" rel="noopener" data-href="http://stackoverflow.com/questions/tagged/webrtc"> Stackoverflow</a>’da bile <a class="markup--anchor markup--p-anchor" href="http://stackoverflow.com/questions/tagged/webrtc" target="_blank" rel="noopener" data-href="http://stackoverflow.com/questions/tagged/webrtc">webrtc</a> etiketi ile açılmış soru sayısı 3000&#8217;i bulmamış durumda :(<br /> Tabi WebRTC’nin daha telekom dünyasına özel bir teknoloji olması da bunda etkili olmuştur.
</p><figure class="graf graf--figure">

<img class="alignnone size-full wp-image-60" src="http://busradeniz.com/wp-content/uploads/2017/07/webrtc_developer_statistics-1024x549.png" alt="" width="1024" height="549" srcset="https://www.busradeniz.com/wp-content/uploads/2017/07/webrtc_developer_statistics-1024x549.png 1024w, https://www.busradeniz.com/wp-content/uploads/2017/07/webrtc_developer_statistics-1024x549-300x161.png 300w, https://www.busradeniz.com/wp-content/uploads/2017/07/webrtc_developer_statistics-1024x549-768x412.png 768w, https://www.busradeniz.com/wp-content/uploads/2017/07/webrtc_developer_statistics-1024x549-746x400.png 746w" sizes="(max-width: 1024px) 100vw, 1024px" /> </figure> 

<p class="graf graf--p">
  Ama Google genel olarak sorularınıza cevap alabildiğiniz, aktif ve erişilebilir bir WebRTC takımı barındırıyor.
</p>

### WebRTC API {.graf.graf--h3}

<p class="graf graf--p">
  Burda detaylı olarak WebRTC API’sinden bahsetmeyeceğim. İlerleyen ve daha teknik olan WebRTC yazılarımda buna değinmeyi planlıyorum ama en temelde yapılan iş bazında WebRTC API’sini 3 ana bölüme ayırabiliriz :
</p>

### MediaStream (aka getUserMedia)<img class="aligncenter wp-image-61 size-medium" src="http://busradeniz.com/wp-content/uploads/2017/07/webrtc_mediastream_api-1-300x286.png" alt="" width="300" height="286" srcset="https://www.busradeniz.com/wp-content/uploads/2017/07/webrtc_mediastream_api-1-300x286.png 300w, https://www.busradeniz.com/wp-content/uploads/2017/07/webrtc_mediastream_api-1-419x400.png 419w, https://www.busradeniz.com/wp-content/uploads/2017/07/webrtc_mediastream_api-1.png 710w" sizes="(max-width: 300px) 100vw, 300px" /> {.graf.graf--h3}

<p class="graf graf--p">
  MediaStream; genel olarak medya akışları (stream) ile ilgilidir. Cihazda bulunan kamera ve mikrofon seçeneklerine erişiminizi sağlayan, bunların kullanımı için gerekli izinlerin alınmasını yöneten ve buralardan aldığı ses ve görüntü streamlerini içeren API’dir. <em class="markup--em markup--p-em">getUserMedia()</em> methodu ile alındığı için bu ismiyle de kullanılıyor. MediaStream objesi bir etiket ve <em class="markup--em markup--p-em">getAudioTracks()/getVideoTracks()</em> methodları ile alabileceğiniz <em class="markup--em markup--p-em">MediaStreamTrack</em> nesnelerini içerir. <em class="markup--em markup--p-em">MediaStreamTrack</em> ise ‘audio’ ve ‘video’ olacak şekilde bir tipe, bir isime ve bir yada birden fazla ses ve görüntü kanalını içerirler.
</p>

### PeerConnection  
<img class="aligncenter wp-image-62 size-medium" src="http://busradeniz.com/wp-content/uploads/2017/07/webrtc_peerconnection_api-1024x900-300x264.png" alt="" width="300" height="264" srcset="https://www.busradeniz.com/wp-content/uploads/2017/07/webrtc_peerconnection_api-1024x900-300x264.png 300w, https://www.busradeniz.com/wp-content/uploads/2017/07/webrtc_peerconnection_api-1024x900-768x675.png 768w, https://www.busradeniz.com/wp-content/uploads/2017/07/webrtc_peerconnection_api-1024x900.png 1024w, https://www.busradeniz.com/wp-content/uploads/2017/07/webrtc_peerconnection_api-1024x900-455x400.png 455w" sizes="(max-width: 300px) 100vw, 300px" />  {.graf.graf--h3}

<p class="graf graf--p">
  RTCPeerConnection, eşler arasındaki veri akımının, P2P iletişimin yönetildiği WebRTC’nin en temel bileşenidir.
</p>

<p class="graf graf--p">
  Aşağıdaki WebRTC mimarisinde de görüldüğü gibi PeerConnection aslında daha alt katmanlarda gerçekleşen ve real time iletişimi sağlayan tüm işleri biz ObjC, Java, JS geliştiricisinden soyutlar ve
</p>

<ul class="postList">
  <li class="graf graf--li">
    Medyanın karşıdaki kullanıcıya gönderilip, alınması
  </li>
  <li class="graf graf--li">
    Medya kodlaması/çözümlemesi (encoding/decoding) işlemleri
  </li>
  <li class="graf graf--li">
    Güvenlik
  </li>
  <li class="graf graf--li">
    Band genişliği ve paket yönetimi
  </li>
  <li class="graf graf--li">
    Yankı giderimi (echo cancellation)
  </li>
  <li class="graf graf--li">
    Automation Gain Control
  </li>
  <li class="graf graf--li">
    Gürültü azaltımı ve önlenmesi (noise reduction ve suppression )
  </li>
</ul>

<p class="graf graf--p">
  gibi real-time iletişim için gerekli kritik işlemleri yönetir.
</p><figure class="graf graf--figure">

<img class="aligncenter size-large wp-image-63" src="http://busradeniz.com/wp-content/uploads/2017/07/webrtc_architecture-1024x570-1024x570.png" alt="" width="960" height="534" srcset="https://www.busradeniz.com/wp-content/uploads/2017/07/webrtc_architecture-1024x570.png 1024w, https://www.busradeniz.com/wp-content/uploads/2017/07/webrtc_architecture-1024x570-300x167.png 300w, https://www.busradeniz.com/wp-content/uploads/2017/07/webrtc_architecture-1024x570-768x428.png 768w, https://www.busradeniz.com/wp-content/uploads/2017/07/webrtc_architecture-1024x570-719x400.png 719w" sizes="(max-width: 960px) 100vw, 960px" /> </figure> 

### DataChannel  
<img class="aligncenter size-medium wp-image-64" src="http://busradeniz.com/wp-content/uploads/2017/07/webrtc_datachannel_api-300x290.png" alt="" width="300" height="290" srcset="https://www.busradeniz.com/wp-content/uploads/2017/07/webrtc_datachannel_api-300x290.png 300w, https://www.busradeniz.com/wp-content/uploads/2017/07/webrtc_datachannel_api-413x400.png 413w, https://www.busradeniz.com/wp-content/uploads/2017/07/webrtc_datachannel_api.png 693w" sizes="(max-width: 300px) 100vw, 300px" />  {.graf.graf--h3}

<p class="graf graf--p">
  WebRTC’nin en öne çıkan özelliği P2P sesli ve görüntülü iletişim olsa da, aslında DataChannel API aracılığıyla istediğiniz biçimdeki veriyi yine peer-to-peer olarak iletebiliyorsunuz. Eşler arasında güvenli ve düşük gecikme miktarlarıyla veri iletimi yapabiliyorsunuz. Genellikle dosya transferi, uzak masaüstü bağlantı uygulamaları, gerçek zamanlı mesajlaşma uygulamaları ve oyunlarda DataChannel API’si tercih edilebiliyor.
</p>

### Son {.graf.graf--h3}

<p class="graf graf--p">
  WebRTC 101 tadındaki bu yazıdan sonraki planım ise daha teknik detaylarla dolu WebRTC ortamı, WebRTC dünyasında girdiğinizde sıklıkla duyacağınız bazı sunucular, protokoller ve mobil platformlar için build edilmesinden bahsetmeyi planlıyorum.
</p>

<p class="graf graf--p">
  Daha detaylı olarak dinlemek isterseniz de aşağıdaki sunumumu inceleyebilirsiniz.
</p>

<p class="graf graf--p">
  <a class="markup--anchor markup--p-anchor" href="http://www.slideshare.net/BuraDenizCSM/webrtc-voxxed" target="_blank" rel="nofollow noopener noopener" data-href="http://www.slideshare.net/BuraDenizCSM/webrtc-voxxed">http://www.slideshare.net/BuraDenizCSM/webrtc-voxxed</a>
</p>

<p class="graf graf--p">
  GDG DevFest Ukraine 2015 , <a class="markup--anchor markup--p-anchor" href="https://www.youtube.com/watch?v=YWaOdwCenZM" target="_blank" rel="noopener" data-href="https://www.youtube.com/watch?v=YWaOdwCenZM">WebRTC on Mobile</a>
</p>

<p class="graf graf--p">
  VoxxedDays İstanbul 2015, <a class="markup--anchor markup--p-anchor" href="https://www.youtube.com/watch?v=1XlswJv6g8k&index=3&list=PLbi72StPQe2xUwJL0GCuXQafg9v6gKT68" target="_blank" rel="noopener" data-href="https://www.youtube.com/watch?v=1XlswJv6g8k&index=3&list=PLbi72StPQe2xUwJL0GCuXQafg9v6gKT68">WebRTC on Mobile </a>
</p>