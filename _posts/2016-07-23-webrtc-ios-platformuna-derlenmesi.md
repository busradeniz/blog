---
id: 76
title: WebRTC iOS Platformuna Derlenmesi
date: 2016-07-23T11:57:13+01:00
author: Busra Deniz
layout: post
guid: http://busradeniz.com/?p=76
permalink: /webrtc-ios-platformuna-derlenmesi/
asalah_show_meta:
  - "0"
asalah_show_share:
  - "0"
asalah_show_title:
  - "0"
show_author_box:
  - "0"
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
  - "40"
social_aggregate_score_detail:
  - 'a:4:{s:5:"total";d:40;s:13:"social_points";i:0;s:11:"view_points";d:0;s:14:"comment_points";i:40;}'
social_aggregate_score_decayed:
  - "1.02322422325E-291"
social_aggregate_score_decayed_last_updated:
  - "1528391484"
socialcount_LAST_UPDATED:
  - "1528391484"
image: /wp-content/uploads/2017/07/webrtc_ios_title-825x510.png
categories:
  - iOS
  - WebRTC
tags:
  - ios
  - ios webrtc compile
  - ios webrtc derleme
  - native ios webrtc application
  - native webrtc ios
  - realtime ios application
  - webrtc
  - webrtc build
  - webrtc derleme
  - webrtc ios derleme
  - webrtc mac os build
  - webrtc mac os derleme
  - webrtc mobile
  - webrtc nasıl derlenir
  - webrtc türkçe
  - webrtc türkçe döküman
  - webrtc türkçe kaynak
---
<img class="aligncenter size-full wp-image-77" src="http://busradeniz.com/wp-content/uploads/2017/07/webrtc_ios_title.png" alt="" width="960" height="640" srcset="https://www.busradeniz.com/wp-content/uploads/2017/07/webrtc_ios_title.png 960w, https://www.busradeniz.com/wp-content/uploads/2017/07/webrtc_ios_title-300x200.png 300w, https://www.busradeniz.com/wp-content/uploads/2017/07/webrtc_ios_title-768x512.png 768w, https://www.busradeniz.com/wp-content/uploads/2017/07/webrtc_ios_title-600x400.png 600w" sizes="(max-width: 960px) 100vw, 960px" />WebRTC tarayıcılar içinde gömülü olarak geldiği için bir web uygulaması yazarken WebRTC’nin build edilmesi ile uğraşmıyoruz fakat durum native mobil uygulamalar için böyle değil. iOS ve Android için bir native WebRTC uygulaması geliştirmek istiyorsak kütüphanenin kodunu indirip ilgili platformlar için derlememiz gerekiyor. Bu yazımda sadece iOS platformunun derlenmesinden bahsedeceğim. WebRTC kodunu Xcode ile ya da direk komut satırından derleyebilirsiniz. Ben ikinci yöntem ile ilerleyeceğim.

### Ortam Gereklilikleri {.graf.graf--h3}

<p class="graf graf--p">
  İlk olarak WebRTC kodunu iOS platformuna derlenemeniz için bir OS X barındıran makineye ihtiyacınız olacak ve tabiki WebRTC versiyon kontrol sistemi olarak Git kullandığı için makinenizde Git’in kurulu olduğundan emin olmanız gerekiyor. Google kaynaklarında Git 2.2.1 ve üstü versiyonlar tavsiye ediliyor.
</p>

<pre name="cd90" class="graf graf--pre">$ git --version
git version 2.8.1</pre>

### WebRTC kodunu alma {.graf.graf--h3}

<p class="graf graf--p">
  Geliştirme ortamımız hazır olduktan sonra WebRTC kodunu kendi makinemize alabiliriz. Fakat direk WebRTC kodunu çekmeden önce build adımlarının daha kolaylaşması için <strong class="markup--strong markup--p-strong"><em class="markup--em markup--p-em">depot_tools</em></strong> adı verilen script paketini indirmemiz gerekiyor.
</p>

<pre name="7b45" class="graf graf--pre">$ git clone <a class="markup--anchor markup--pre-anchor" href="https://chromium.googlesource.com/chromium/tools/depot_tools.git" target="_blank" rel="noopener" data-href="https://chromium.googlesource.com/chromium/tools/depot_tools.git">https://chromium.googlesource.com/chromium/tools/depot_tools.git</a></pre>

<p class="graf graf--p">
  <strong class="markup--strong markup--p-strong"><em class="markup--em markup--p-em">depot_tools</em></strong> u lokalimize başarılı bir şekilde çektikten sonra PATH olarak ekliyoruz.
</p>

<pre name="dac1" class="graf graf--pre">$ export PATH=`pwd`/depot_tools:"$PATH"</pre>

<p class="graf graf--p">
  Benim PATH değişkenimi yazdırdığımda şöyle bir sonuç elde ediyorum :
</p>

<p class="graf graf--p">
  <em class="markup--em markup--p-em">/Users/busradeniz/Development/WebRTC/iOS/depot_tools:/Users/busradeniz/Development/WebRTC/depot_tools/:/usr/local/bin:/usr/bin:/bin:/usr/sbin:/sbin</em>
</p>

<p class="graf graf--p">
  Ardından target işletim sistemini iOS olarak belirtiyoruz :
</p>

<pre name="b50e" class="graf graf--pre">$ export GYP_DEFINES="OS=ios"</pre>

<p class="graf graf--p">
  WebRTC kodunu indireceğimiz klasörün içerisine girip aşağıdaki komutları çalıştırıyoruz.
</p>

<pre name="c651" class="graf graf--pre">$ fetch --nohooks webrtc_ios
$ gclient sync</pre>

<p class="graf graf--p">
  <strong class="markup--strong markup--p-strong"><em class="markup--em markup--p-em">gclient sync</em></strong> komutunu çalıştırdıktan sonra uzun bir süre beklemeniz gerekecek. Benim kodu çekmem yaklaşık 3 saat sürdü ve işlem sonunda kodu çektiğim dosyanın boyutu 12 GB civarındaydı. Bu nedenle bilgisayarınızda yeterli yer olduğunuzdan da emin olmanız yararınıza olabilir. Bu süre tabiki WebRTC kodunu ilk kez çektiğimiz için bu kadar uzun, bundan sonrakilerde sadece güncellemeleri alacağımızdan çok daha kısa sürede tamamlanacak.
</p>

### iOS için kod derleme {.graf.graf--h3}

<p class="graf graf--p">
  WebRTC kodunu derlemeye başlamadan önce hangi tip cihaz için derleyeceğimizi ve build edilmiş kodun klasörünü vermemiz yani <strong class="markup--strong markup--p-strong"><em class="markup--em markup--p-em">GYP_DEFINES</em></strong> ve <strong class="markup--strong markup--p-strong"><em class="markup--em markup--p-em">GYP_GENERATOR_FLAGS</em></strong> değişkenlerini belirtmemiz gerekiyor. <strong class="markup--strong markup--p-strong"><em class="markup--em markup--p-em">output_dir</em></strong> ‘e herhangi bir isim yazabilirsiniz.
</p>

<p class="graf graf--p">
  <strong class="markup--strong markup--p-strong">iOS cihazlar için :</strong>
</p>

<pre name="038d" class="graf graf--pre">$ export GYP_DEFINES="OS=ios target_arch=arm"
$ export GYP_GENERATOR_FLAGS="output_dir=out_ios"</pre>

<p class="graf graf--p">
  <strong class="markup--strong markup--p-strong">iOS 64-bit cihazlar için :</strong>
</p>

<pre name="4fcc" class="graf graf--pre">export GYP_DEFINES="OS=ios target_arch=arm64"
export GYP_GENERATOR_FLAGS="output_dir=out_ios64"</pre>

<p class="graf graf--p">
  <strong class="markup--strong markup--p-strong">iOS Simulator için :</strong>
</p>

<pre name="e115" class="graf graf--pre">$ export GYP_DEFINES="OS=ios target_arch=ia32"
$ export GYP_GENERATOR_FLAGS="output_dir=out_sim"</pre>

<p class="graf graf--p">
  <strong class="markup--strong markup--p-strong">iOS 64-bit Simulator için :</strong>
</p>

<pre name="71be" class="graf graf--pre">$ export GYP_DEFINES="OS=ios target_arch=x64"
$ export GYP_GENERATOR_FLAGS="output_dir=out_sim64"</pre>

<p class="graf graf--p">
  şeklinde tanımladıktan sonra <strong class="markup--strong markup--p-strong"><em class="markup--em markup--p-em">src</em></strong> klasörünün içerisine girip <strong class="markup--strong markup--p-strong"><em class="markup--em markup--p-em">gyp_webrtc</em></strong> scriptini çalıştırıyoruz :
</p>

<pre name="c62c" class="graf graf--pre">$ webrtc/build/gyp_webrtc.py</pre>

<p class="graf graf--p">
  Scripti çalıştırdıktan sonra <strong class="markup--strong markup--p-strong"><em class="markup--em markup--p-em">src</em></strong> klasörü altında <strong class="markup--strong markup--p-strong"><em class="markup--em markup--p-em">output_dir</em></strong> olarak verdiğiniz isimde klasörün oluşturulduğunu göreceksiniz. Gyp değişkenlerinde herhangi bir değişiklik yaptıktan sonra <strong class="markup--strong markup--p-strong"><em class="markup--em markup--p-em">gyp_webrtc</em></strong> scriptini tekrar çalıştırdığınızdan emin olmalısınız. Aksi taktirde derlemeye çalışırken böyle bir dosya bulunamadı gibi bir hata alacaksınızdır.
</p>

<p class="graf graf--p">
  Tüm bu adımlardan sonra artık derleme zamanı! İstediğiniz konfigurasyona uygun olarak aşağıdaki örneklerdeki gibi WebRTC kodunu derleyebilirsiniz.
</p>

<pre name="d053" class="graf graf--pre">$ ninja -C out_ios/Release-iphoneos AppRTCDemo
$ ninja -C out_ios64/Debug-iphoneos AppRTCDemo
$ ninja -C out_sim64/Debug-iphonesimulator AppRTCDemo</pre>

<p class="graf graf--p">
  En sonunda elinizde şöyle bir görüntü oluşacak :
</p><figure class="graf graf--figure">

<img class="graf-image" src="https://cdn-images-1.medium.com/max/1600/0*c7eyyryxfEywQeDG.png" data-image-id="0*c7eyyryxfEywQeDG.png" data-width="783" data-height="1024" /> </figure> <figure class="graf graf--figure"><img class="graf-image" src="https://cdn-images-1.medium.com/max/1600/0*F2JBD3BZE2lC2y00.png" data-image-id="0*F2JBD3BZE2lC2y00.png" data-width="248" data-height="300" /></figure> 

<p class="graf graf--p">
  AppRTCDemo’yu çalıştırdığınızda da ilk aramanızı yapabilirsiniz
</p>

<p class="graf graf--p">
  Aslında gördüğünüz gibi WebRTC’nin iOS için kolay bir derleme süreci var fakat özellikle ilk checkout işleminin uzun sürmesi nedeniyle biraz vakit alıyor diyebiliriz. Derlediğimiz WebRTC kütüphanesini native bir iOS uygulamasına nasıl entegre edeceğimizi de diğer yazımda paylaşacağım.
</p>

### Olası Hatalar {.graf.graf--h3}

<p class="graf graf--p">
  Benim build sırasında yaşadığım iki sorunu da buraya eklemek istiyorum.
</p>

<ol class="postList">
  <li class="graf graf--li">
    PATH değişkenini doğru tanımlayamamak, dikkatsizliğine gelip bir karakteri unutabilirsiniz.
  </li>
  <li class="graf graf--li">
    GYP değişkenini tanımladıktan sonra gyp_webrtc scriptini çalıştırmayı unuttuğum için build sırasında hata aldım. Şurdaki cevaplardan hata nedenini bulup düzeltebilmiştim. <a class="markup--anchor markup--li-anchor" href="https://bugs.chromium.org/p/webrtc/issues/detail?id=5425" target="_blank" rel="noopener" data-href="https://bugs.chromium.org/p/webrtc/issues/detail?id=5425">https://bugs.chromium.org/p/webrtc/issues/detail?id=5425</a>
  </li>
</ol>