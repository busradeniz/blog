---
id: 66
title: WebRTC Kavramları ve Altyapısı
date: 2016-07-18T11:47:16+01:00
author: Busra Deniz
layout: post
guid: http://busradeniz.com/?p=66
permalink: /webrtc-kavramlari-ve-altyapisi/
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
  - "20"
social_aggregate_score_detail:
  - 'a:4:{s:5:"total";d:20;s:13:"social_points";i:0;s:11:"view_points";d:0;s:14:"comment_points";i:20;}'
social_aggregate_score_decayed:
  - "3.42971862854E-295"
social_aggregate_score_decayed_last_updated:
  - "1528590270"
socialcount_LAST_UPDATED:
  - "1528590270"
image: /wp-content/uploads/2017/07/webrtc_infrastructure-825x510.jpg
categories:
  - WebRTC
tags:
  - ice framework
  - p2p
  - peer to peer communication
  - peer to peer iletisim
  - real time communication
  - rtc
  - sdp
  - sdp nedir
  - session description protocol
  - stun
  - stun nedir
  - turn
  - turn nedir
  - webrtc altyapısı
  - webrtc evolution
  - webrtc ice
  - webrtc infrastructure
  - webrtc kavramları
  - webrtc nedir
  - webrtc signalling
  - webrtc sinyalleşme
  - webrtc sinyalleşme nedir
  - webrtc sunucuları
  - webrtc türkçe
  - webrtc türkçe blog
  - webrtc türkçe kaynak
  - what is webrtc
---
<p class="graf graf--p">
  <a class="markup--anchor markup--p-anchor" href="http://busradeniz.com/2016/07/05/webrtc-nedir/" target="_blank" rel="noopener" data-href="https://medium.com/@busradeniz/webrtc-nedir-8a483e686162#.dke3uc47n"><img class="aligncenter size-full wp-image-67" src="http://busradeniz.com/wp-content/uploads/2017/07/webrtc_infrastructure.jpg" alt="" width="960" height="640" srcset="https://www.busradeniz.com/wp-content/uploads/2017/07/webrtc_infrastructure.jpg 960w, https://www.busradeniz.com/wp-content/uploads/2017/07/webrtc_infrastructure-300x200.jpg 300w, https://www.busradeniz.com/wp-content/uploads/2017/07/webrtc_infrastructure-768x512.jpg 768w, https://www.busradeniz.com/wp-content/uploads/2017/07/webrtc_infrastructure-600x400.jpg 600w" sizes="(max-width: 960px) 100vw, 960px" /><br /> Bir önceki yazımda</a> WebRTC’nin ne olduğundan bahsetmiş, genel olarak tanımını yapmıştım. Bu yazımda ise WebRTC dünyasında girdiğiniz anda bol bol duyacağınız bazı konseptlerden bahsedeceğim. WebRTC ilk anlatıldığında, eşler arasında peer-to-peer medya iletişimi yapıyor, sadece API’sini kullanarak harikalar yaratıyorsunuz gibi bir izlenim bırakıyor ama işin içine girince aslında kullanmanız gereken sunucular, protokoller olduğunu ve bazı durumlarda peer-to-peer durumunun olamadığını öğreniyorsunuz.
</p>

<p class="graf graf--p">
  Bir WebRTC uygulaması yazarken sinyalleşme, offer/answer mekanizması, SDP, STUN, TURN, ICE gibi belki daha önce duymadığınız ama WebRTC ile uğraşırken öğrenmeniz gereken kavramlarla başlayalım.
</p>

### Sinyalleşme {.graf.graf--h3}

<p class="graf graf--p">
  Sinyalleşmeyi WebRTC çözümünüzün en temel parçası ve basit bir telefon aramasını düşündüğünüzde kimin kiminle nasıl konuşacağı probleminin çözüldüğü kısmı olarak düşünebilirsiniz. Karşılıklı iki eş arasındaki medya iletimini WebRTC’nin gerçekleştirdiğinden bahsetmiştik ama medya iletiminin başlaması için WebRTC’ye medyayı nasıl ve nereye göndereceğini haber vermeniz gerekir. Bu kısım sinyalleşme olarak adlandırılır ve tamamen kullanılacak olan yöntem ve protokoller size bırakılmıştır.
</p>

<p class="graf graf--p">
  WebRTC hem var olan tüm teknolojiler ile uyumlu olma adına hem de sinyalleşme işlemlerini de bünyesinde barındırıp karmaşıklığı arttırmamak ve kullanıcıyı belirli bir teknolojiye zorlamamak için herhangi bir protokol tanımlamıyor. Yani sinyalleşme sunucusunu kendinizin geliştirmesi ya da bunun için geliştirilmiş herhangi bir açık kaynaklı projeyi kullanmanız gerekiyor. Sinyalleşme için
</p>

<ul class="postList">
  <li class="graf graf--li">
    WebSockets
  </li>
  <li class="graf graf--li">
    WebRTC DataChannel
  </li>
  <li class="graf graf--li">
    XMPP
  </li>
  <li class="graf graf--li">
    SIP over WebSockets gibi yöntemleri kullanabilirsiniz. Kendi çözümünüzün gerekliliklerini göz önünde bulundurup herhangi bir yöntemle devam edebilirsiniz.
  </li>
</ul>

<p class="graf graf--p">
  Sinyalleşmeyi medya iletimi yapılacak kullanıcılar arasında koordinasyonu sağladığımız, bir aramanın gerçekleşmesi için gerekli bilgilerin karşılıklı olarak alınmasını sağlayan süreç olarak düşünebiliriz. Bu süreçte aramanın gerçekleşeceği iki kullanıcı arasında; hangi IP ve port üzerinden haberleşileceği, hangi ses ve görüntü kodeklerin kullanılacağı gibi verileri içeren SDP (session description protocol) objelerinin alışverişi sağlanır.
</p>

<p class="graf graf--p">
  WebRTC sinyalleşmesi <a class="markup--anchor markup--p-anchor" href="https://tools.ietf.org/html/draft-ietf-rtcweb-jsep-03#section-1.1" target="_blank" rel="noopener" data-href="https://tools.ietf.org/html/draft-ietf-rtcweb-jsep-03#section-1.1">JSEP</a> (Javascript Session Establishment Protocol)’nin getirdiği offer/answer mekanizmasına dayanır ve sizin sinyalleşme sunucunuzun da bu mantığı baz alarak çalışması gerekir. Offer/Answer mekanizması dediğimiz, iki eş arasında arama ile ilgili herhangi bir işlem (arama başlatılması, beklemeye alma, sessize alma ya da aramanın sonlandırılması gibi işlemlerden bahsediyoruz) gerçekleştirileceğinde WebRTC kütüphanesi tarafından üretilen offer ve bu offer’a karşı üretilen answer SDP paketlerinin alışverişidir.
</p>

<p class="graf graf--p">
  Örnek olarak, bir arama başlama işleminde gerçekleşecek olan offer/answer sürecini ele alalım :
</p><figure class="graf graf--figure">

<img class="aligncenter size-full wp-image-68" src="http://busradeniz.com/wp-content/uploads/2017/07/webrtc_signalling-1024x513.png" alt="" width="1024" height="513" srcset="https://www.busradeniz.com/wp-content/uploads/2017/07/webrtc_signalling-1024x513.png 1024w, https://www.busradeniz.com/wp-content/uploads/2017/07/webrtc_signalling-1024x513-300x150.png 300w, https://www.busradeniz.com/wp-content/uploads/2017/07/webrtc_signalling-1024x513-768x385.png 768w, https://www.busradeniz.com/wp-content/uploads/2017/07/webrtc_signalling-1024x513-798x400.png 798w" sizes="(max-width: 1024px) 100vw, 1024px" /> </figure> 

<ol class="postList">
  <li class="graf graf--li">
    Aramayı başlatacak olan tarafta WebRTC kütüphanesi arama başlatacak olan offer SDP paketini üretip uygulama katmanına verir. Uygulama katmanı bu SDP’yi sinyalleşme sunucusuna iletmekle yükümlüdür.
  </li>
  <li class="graf graf--li">
    Sinyalleşme sunucusu “arayan” tarafından gönderilen SDP paketini ilgili diğer istemciye (“aranan”) iletir.
  </li>
  <li class="graf graf--li">
    Offer SDP’sini alan aranan taraf bu SDP’yi WebRTC kütüphanesine verir ve karşılığı olan answer SDP’sini sinyalleşme sunucusuna gönderir.
  </li>
  <li class="graf graf--li">
    Sinyalleşme sunucusu answer SDP’yi “arayan” tarafa iletir ve “arayan” tarafta gelen SDP WebRTC kütüphanesine bildirir.
  </li>
  <li class="graf graf--li">
    Offer/answer süreci başarıyla tamamlandıktan ve eşler arasındaki uzlaşma (negotiation) sağlandıktan sonra iki eş arasında medya iletimi peer-to-peer olarak başlar.
  </li>
</ol>

<p class="graf graf--p">
  Görüldüğü gibi medya iletiminden ve medya ile ilgili kısımlardan WebRTC sorumlu, uygulama katmanında yapılması gereken işlem ise yine WebRTC tarafından üretilen SDP paketlerinin karşı tarafa gönderilmesi ve alınmasını sağlamak.
</p>

### SDP {.graf.graf--h3}

<p class="graf graf--p">
  Sinyalleşmeden bahsederken SDP objelerinin alışverişinden bahsettik, peki ama SDP nedir? <a class="markup--anchor markup--p-anchor" href="https://en.wikipedia.org/wiki/Session_Description_Protocol" target="_blank" rel="noopener" data-href="https://en.wikipedia.org/wiki/Session_Description_Protocol">SDP (Session Description Protocol)</a> bir oturumu tanımlamak için kullanılan bir formattır. Özellikle multi-medya iletişimi için kullanılır ve medyayı kendi iletmez, sadece JSON, XML gibi bir format olarak düşünebilirsiniz. SIP, RTSP, HTTP gibi farklı iletişim protokolleri ile çalışabilir.
</p>

<p class="graf graf--p">
  SDP içerisinde temel olarak sırayla genel oturum bilgileri, oturum zamanı ve medya bilgilerini içerir. Haberleşilecek IP, port, medya türü (video, ses ya da ikisi birden olabilir), her medya satırı için gerekli özellikler gibi daha detaylı bilgileri içeren bir SDP’nin aşağıdaki gibi bir görünümü vardır.
</p><figure class="graf graf--figure">

<img class="aligncenter size-full wp-image-69" src="http://busradeniz.com/wp-content/uploads/2017/07/webrtc_sdp_sample-1024x410.png" alt="" width="1024" height="410" srcset="https://www.busradeniz.com/wp-content/uploads/2017/07/webrtc_sdp_sample-1024x410.png 1024w, https://www.busradeniz.com/wp-content/uploads/2017/07/webrtc_sdp_sample-1024x410-300x120.png 300w, https://www.busradeniz.com/wp-content/uploads/2017/07/webrtc_sdp_sample-1024x410-768x308.png 768w, https://www.busradeniz.com/wp-content/uploads/2017/07/webrtc_sdp_sample-1024x410-940x376.png 940w" sizes="(max-width: 1024px) 100vw, 1024px" /> </figure> 

<p class="graf graf--p">
  SDP formatının daha ayrıntılı bilgisini, hangi etiketin ne anlama geldiği ve sıralamasını <a class="markup--anchor markup--p-anchor" href="http://www.slideshare.net/BuraDenizCSM/sdp-session-descriptionprotokol" target="_blank" rel="noopener" data-href="http://www.slideshare.net/BuraDenizCSM/sdp-session-descriptionprotokol">burdaki sunumumdan</a> edinebilirsiniz.
</p>

### STUN {.graf.graf--h3}

<p class="graf graf--p">
  Şimdiye kadarki üzerinde konuştuğumuz senaryo; arayan taraf kendi bilgilerini aranan tarafa iletir, aranan tarafta kendi bilgilerini aranan tarafa iletir ve medya peer-to-peer olarak gönderilir. Ama burda dikkat edilmesi gereken nokta peer-to-peer için eşlerin kendi public IP’lerini biliyor olması ve SDP’nin bu IP yi içeriyor olmasıdır ve gerçek dünyayı göz önünde bulundurup NAT’lar arkasında olduğumuzu düşündüğümüzde eşlerin kendi public IP’lerini bilmeme gibi bir sorunları olduğunu fark ediyoruz. Bu problemin çözümü olarak WebRTC <a class="markup--anchor markup--p-anchor" href="https://en.wikipedia.org/wiki/STUN" target="_blank" rel="noopener" data-href="https://en.wikipedia.org/wiki/STUN">STUN (Session Traversal Utilities for NAT)</a> sunucuları kullanılıyor.
</p><figure class="graf graf--figure">

<img class="aligncenter size-full wp-image-70" src="http://busradeniz.com/wp-content/uploads/2017/07/webrtc_stun-1024x592.png" alt="" width="1024" height="592" srcset="https://www.busradeniz.com/wp-content/uploads/2017/07/webrtc_stun-1024x592.png 1024w, https://www.busradeniz.com/wp-content/uploads/2017/07/webrtc_stun-1024x592-300x173.png 300w, https://www.busradeniz.com/wp-content/uploads/2017/07/webrtc_stun-1024x592-768x444.png 768w, https://www.busradeniz.com/wp-content/uploads/2017/07/webrtc_stun-1024x592-692x400.png 692w" sizes="(max-width: 1024px) 100vw, 1024px" /> </figure> 

<p class="graf graf--p">
  Kendisine istek gönderen tarafın public IP ve port bilgisini göndererek istemci tarafın bu bilgilere sahip olmasını sağlar. İstemci kendi public IP sini öğrenmek için STUN ile iletişime geçer ve aldığı IP bilgisiyle birlikte sinyalleşmeye normal olarak devam eder.Burdaki önemli noktalardan bir tanesi medyanın hala <strong class="markup--strong markup--p-strong">peer-to-peer</strong> olmasıdır. Bu nedenle STUN basit ve ucuz bir çözümdür, Google’ın ücretsiz sağlamış olduğu STUN sunucularını ya da açık kaynak olarak yayınlanmış STUN çözümlerini kendi sunucunuzda kurarak kullanabilirsiniz.
</p>

<p class="graf graf--p">
  Yine WebRTC akışını düşündüğümüzde STUN ile iletişimden WebRTC sorumlu, uygulama tarafı olarak sizin, kullanılacak olan STUN sunucu bilgilerini WebRTC kütüphanesine vermeniz gerekir.
</p>

### TURN {.graf.graf--h3}

<p class="graf graf--p">
  STUN çözümünden sonra yapacağımız aramaların çok büyük bir kısmının başarılı olmasını sağlayabildik ama hala problem oluşturan durumların mevcut olduğunu fark edeceksiniz. Mesela, firewall ya da traversal NAT arkasındaki istemciler arasındaki aramalar başarısız olacaktır. STUN bu tip durumlarda problemi çözemeyecek ve <a class="markup--anchor markup--p-anchor" href="https://en.wikipedia.org/wiki/Traversal_Using_Relays_around_NAT" target="_blank" rel="noopener" data-href="https://en.wikipedia.org/wiki/Traversal_Using_Relays_around_NAT">TURN (Traversal Using Relays around NAT)</a> çözümüne başvurmanız gerekecektir.
</p><figure class="graf graf--figure">

<img class="aligncenter size-full wp-image-71" src="http://busradeniz.com/wp-content/uploads/2017/07/webrtc_turn-1024x567.png" alt="" width="1024" height="567" srcset="https://www.busradeniz.com/wp-content/uploads/2017/07/webrtc_turn-1024x567.png 1024w, https://www.busradeniz.com/wp-content/uploads/2017/07/webrtc_turn-1024x567-300x166.png 300w, https://www.busradeniz.com/wp-content/uploads/2017/07/webrtc_turn-1024x567-768x425.png 768w, https://www.busradeniz.com/wp-content/uploads/2017/07/webrtc_turn-1024x567-722x400.png 722w" sizes="(max-width: 1024px) 100vw, 1024px" /> </figure> 

<p class="graf graf--p">
  TURN kullanımıyla birlikte <strong class="markup--strong markup--p-strong">peer-to-peer iletişimi kırıyor</strong> ve medyayı turn sunucuları üzerinden göndermeye başlıyoruz. Medya iletiminin bir sunucu üzerinden olması ve kullanıcıların sunucunun bandwidth ini kullanması nedeniyle STUN a göre daha pahalı bir çözümdür ama TURN sunucusunun bulunduğu bir WebRTC çözümünde tüm durumlarda aramalarınızın başarılı olmasını sağlanır. <a class="markup--anchor markup--p-anchor" href="https://github.com/coturn/rfc5766-turn-server/" target="_blank" rel="noopener" data-href="https://github.com/coturn/rfc5766-turn-server/">Google’ın tavsiye ettiği TURN </a>sunucusunu kendi ortamınıza deploy edip, kullanabilirsiniz.
</p>

### ICE {.graf.graf--h3}<figure class="graf graf--figure">

<img class="aligncenter size-full wp-image-72" src="http://busradeniz.com/wp-content/uploads/2017/07/webrtc_ice-1024x823.png" alt="" width="1024" height="823" srcset="https://www.busradeniz.com/wp-content/uploads/2017/07/webrtc_ice-1024x823.png 1024w, https://www.busradeniz.com/wp-content/uploads/2017/07/webrtc_ice-1024x823-300x241.png 300w, https://www.busradeniz.com/wp-content/uploads/2017/07/webrtc_ice-1024x823-768x617.png 768w, https://www.busradeniz.com/wp-content/uploads/2017/07/webrtc_ice-1024x823-498x400.png 498w" sizes="(max-width: 1024px) 100vw, 1024px" /> </figure> 

<p class="graf graf--p">
  WebRTC bu karmaşıklığı aşmak ve hangi durumda nasıl davranacağına kullandığı ICE framework ile karar veriyor. ICE birbiriyle konuşacak iki eş arasındaki en iyi yolu bulup WebRTC’nin kullanmasını sağlıyor. ICE çalışma mantığında; eğer çiftler peer-to-peer olarak konuşabiliyorsa ilk tercih her zaman bu seçenek oluyor. Eğer peer-to-peer seçeneği olumsuz ise STUN çözümünü, o da olmazsa TURN çözümünü seçerek aramanın gerçekleşmesini sağlıyor. Bu kontrolleri paralel olarak yapıp, iki eş arasındaki en iyi yolu bulmaya çalışır.
</p>

<p class="graf graf--p">
  Peki uygulama tarafı olarak bize düşen nedir? Uygulama tarafında kullanılacak ICE sunucularının (STUN ve TURN sunucularının) bilgilerini WebRTC’ye belirterek arama sırasında bu seçimi yapabilmesini sağlamamız gerekiyor.
</p>

<p class="graf graf--p">
  TURN durumunun olabileceğinden bahsettikten sonra akıllara WebRTC’nin peer-to-peer olması ile ilgili sorular gelebilir. En başta da dediğimiz gibi hala WebRTC’nin en büyük söylemlerinden biri peer-to-peer iletişim. Bunu da büyük bir oranda başardığını Google ve <a class="markup--anchor markup--p-anchor" href="http://webrtcstats.com/first-webrtc-statistics/" target="_blank" rel="noopener" data-href="http://webrtcstats.com/first-webrtc-statistics/">Bistri’nin</a> yayınladığı istatistiklerden görebiliyoruz.
</p><figure class="graf graf--figure">

<img class="aligncenter size-full wp-image-73" src="http://busradeniz.com/wp-content/uploads/2017/07/webrtc_turn_vs_p2p-1024x306.png" alt="" width="1024" height="306" srcset="https://www.busradeniz.com/wp-content/uploads/2017/07/webrtc_turn_vs_p2p-1024x306.png 1024w, https://www.busradeniz.com/wp-content/uploads/2017/07/webrtc_turn_vs_p2p-1024x306-300x90.png 300w, https://www.busradeniz.com/wp-content/uploads/2017/07/webrtc_turn_vs_p2p-1024x306-768x230.png 768w, https://www.busradeniz.com/wp-content/uploads/2017/07/webrtc_turn_vs_p2p-1024x306-940x281.png 940w" sizes="(max-width: 1024px) 100vw, 1024px" /> </figure> 

### Son {.graf.graf--h3}

<p class="graf graf--p">
  En basit haliyle WebRTC’nin beraberinde getirdiği protokollere ve teknolojilere değinmeye çalıştım. Tabiki, ciddi anlamda kaliteli bir gerçek zamanlı haberleşme uygulaması yazmak istediğinizde her bileşen kritik rol oynuyor ve her biri hakkında çok daha derin bilgi edinmek zorunda kalıyorsunuz :)
</p>